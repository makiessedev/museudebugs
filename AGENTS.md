# AGENTS.md

## Regra Crítica

**NUNCA executes comandos sem a permissão explícita do utilizador.**

Sempre que precisares de executar um comando (Bash, git, npm, etc.), deves:

1. Explicar qual comando pretendes executar e porquê
2. Perguntar explicitamente ao utilizador se podes executar
3. Aguardar pela confirmação antes de prosseguir

Esta regra aplica-se a **todos os comandos**, incluindo:
- `git commit`, `git push`, `git rebase`
- `npm install`, `npm run`
- Comandos de build, test, lint
- Quaisquer modificações ao sistema de ficheiros além de criar/editar ficheiros pedidos pelo utilizador
