---
title: "Emulador Android invisível após desligar monitores externos"
date: 2026-05-02
tags:
  - android-studio
  - windows
  - powershell
  - android-emulator
status: draft
slug: emulador-android-invisivel-apos-desligar-monitores-externos
description: "Como recuperar uma janela perdida fora do ecrã usando PowerShell e a Win32 API quando o emulador Android fica invisível após desligar monitores externos."
---

# Emulador Android invisível após desligar monitores externos

### Como recuperar uma janela perdida fora do ecrã usando PowerShell e a Win32 API

*2 de Maio, 2026 · Android Studio · Windows*

---

## O problema

Ao trabalhar com múltiplos monitores no escritório, o Android Studio memoriza a posição de cada janela — incluindo o emulador Android (AVD). Quando voltamos para casa com apenas o portátil, a janela do emulador fica posicionada nas coordenadas do monitor externo, que já não existe. O resultado: o processo está em execução, aparece na barra de tarefas, mas é completamente invisível.

**Sintoma:** O emulador aparece na barra de tarefas e no Task Manager como processo ativo, mas não é visível em nenhum ecrã. Ao ligar os monitores externos, a janela reaparece normalmente noutro monitor.

---

## A causa

O Windows guarda a posição de cada janela e restaura-a na próxima abertura. Quando o emulador foi fechado pela última vez com o monitor externo ligado, as coordenadas salvas apontam para além dos limites do ecrã do portátil.

O ficheiro `emulator-user.ini` dentro da pasta do AVD guarda estas coordenadas:

```
C:\Users\<utilizador>\.android\avd\<nome_do_avd>.avd\emulator-user.ini
```

Pode verificar o conteúdo com:

```powershell
type "C:\Users\<utilizador>\.android\avd\<nome_do_avd>.avd\emulator-user.ini"
```

Se os valores `window.x` e `window.y` forem muito grandes (ex: `2560`, `1440`), a janela está fora do ecrã. Nesse caso, feche o emulador, edite o ficheiro e mude para `0`, depois reabra.

No entanto, se o emulador já estiver em execução com a janela em memória, editar o ficheiro não resolve — é preciso manipular a janela diretamente.

---

## A solução passo a passo

### Passo 1 — Confirmar que o emulador está mesmo em execução

```powershell
Get-Process | Where-Object {$_.Name -like "*emulator*" -or $_.Name -like "*qemu*"}
```

Se aparecer um processo na lista, o emulador está ativo mas invisível.

---

### Passo 2 — Descobrir o título exato da janela

O `FindWindow` com o título genérico "Android Emulator" não funciona — o título real inclui o nome do AVD e a porta. Liste todas as janelas visíveis e filtre:

```powershell
Add-Type @"
  using System;
  using System.Collections.Generic;
  using System.Runtime.InteropServices;
  using System.Text;
  public class WinList {
    public delegate bool EnumDelegate(IntPtr hwnd, IntPtr lParam);
    [DllImport("user32.dll")] public static extern bool EnumWindows(EnumDelegate f, IntPtr lParam);
    [DllImport("user32.dll")] public static extern int GetWindowText(IntPtr h, StringBuilder s, int max);
    [DllImport("user32.dll")] public static extern bool IsWindowVisible(IntPtr h);
    public static List<string> GetTitles() {
      var list = new List<string>();
      EnumWindows((h, l) => {
        var sb = new StringBuilder(256);
        GetWindowText(h, sb, 256);
        if (IsWindowVisible(h) && sb.Length > 0) list.Add(sb.ToString());
        return true;
      }, IntPtr.Zero);
      return list;
    }
  }
"@
[WinList]::GetTitles() | Where-Object { $_ -match "pixel|emulator|avd|android" }
```

O resultado será algo como:

```
Emulator
Android Emulator - Pixel_9_Pro_XL:5554
```

Note o nome do seu AVD — vai precisar dele no passo seguinte.

---

### Passo 3 — Mover a janela para o ecrã principal

Com o nome do AVD identificado, use o comando abaixo substituindo `Pixel_9_Pro_XL` pelo nome do seu AVD:

```powershell
Add-Type @"
  using System;
  using System.Collections.Generic;
  using System.Runtime.InteropServices;
  using System.Text;
  public class WinMover {
    public delegate bool EnumDelegate(IntPtr hwnd, IntPtr lParam);
    [DllImport("user32.dll")] public static extern bool EnumWindows(EnumDelegate f, IntPtr lParam);
    [DllImport("user32.dll")] public static extern int GetWindowText(IntPtr h, StringBuilder s, int max);
    [DllImport("user32.dll")] public static extern bool SetWindowPos(IntPtr h, IntPtr i, int x, int y, int cx, int cy, uint f);
    [DllImport("user32.dll")] public static extern bool ShowWindow(IntPtr h, int cmd);
    public static void MoveAll() {
      EnumWindows((h, l) => {
        var sb = new StringBuilder(256);
        GetWindowText(h, sb, 256);
        string title = sb.ToString();
        if (title == "Emulator" || title.Contains("Pixel_9_Pro_XL")) {
          ShowWindow(h, 9);
          SetWindowPos(h, IntPtr.Zero, 100, 100, 420, 860, 0);
        }
        return true;
      }, IntPtr.Zero);
    }
  }
"@
[WinMover]::MoveAll()
```

O emulador aparecerá imediatamente no canto superior esquerdo do ecrã principal.

---

## Dica para o futuro

Antes de desligar os monitores externos, feche sempre o emulador primeiro. Assim o Windows não guarda a posição no monitor externo e o emulador abre normalmente no ecrã do portátil.

---

## Resumo

| Passo | O que faz |
|---|---|
| Verificar `emulator-user.ini` | Confirma se a posição está errada no ficheiro de configuração |
| `Get-Process` | Confirma que o emulador está em execução mas invisível |
| `EnumWindows` + filtro | Descobre o título exato da janela do emulador |
| `ShowWindow` + `SetWindowPos` | Restaura e move a janela para o ecrã principal |
