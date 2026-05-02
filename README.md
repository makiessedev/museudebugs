# Museu de Bugs

Diário técnico em Markdown, versionado aqui no GitHub. É sobretudo um registo do dia a dia de quem escreve; ao mesmo tempo, o repositório (e o site, se existir) ficam públicos para quem quiser folhear notas, erros, ferramentas e opiniões à medida que vão aparecendo.

## Sobre o blog

Textos informais sobre **bugs**, **ferramentas**, **tecnologia** e **opiniões pessoais** — o que fizer sentido documentar no momento.

## O que podes encontrar aqui

- Artigos em Markdown com frontmatter YAML (`title`, `date`, `tags`, `status`, etc.).
- **Rascunhos** em `drafts/`: é aqui que cada artigo **novo** deve ser criado primeiro.
- **Publicados** (ou prontos para a linha de `posts/`) em `posts/AAAA/MM/` — **ano** e **mês** (`MM` de `01` a `12`), normalmente depois de saírem de `drafts/`. No repositório mantém-se só a pasta do **mês corrente**; quando mudar o mês ou publicares fora dele, cria `posts/AAAA/MM/` conforme precisares.
- Imagens de apoio em `assets/images/`.
- Um modelo vazio em `templates/post-template.md` para quem quiser ver o formato típico de um post.

## Convenção dos nomes dos ficheiros

Os posts seguem **kebab-case** com a data no início, para ordenação e leitura no explorador de ficheiros:

`YYYY-MM-DD-titulo-do-post.md`

Exemplos de caminho:

- Ao **começar** o texto: `drafts/2026-05-02-notas-sobre-um-bug-estranho.md`
- Depois de **publicar** (ou mover para a árvore de posts): `posts/2026/05/2026-05-02-notas-sobre-um-bug-estranho.md`

## Estado do artigo

Sempre que **iniciares** um artigo novo:

1. Cria o ficheiro em **`drafts/`** (não o abras directamente em `posts/`).
2. No frontmatter, o `status` deve ser **`draft`**. Só mudas depois, por exemplo para `published`, quando o post estiver pronto; nessa altura podes mover o ficheiro para `posts/AAAA/MM/` se fizer sentido para o teu fluxo.

## Posts recentes

| Data | Título | Tags | Status |
|------|--------|------|--------|
| | | | |

Para ver o que já existe, começa por `drafts/` (ideias e textos em curso) e depois `posts/AAAA/MM/` para entradas já na pasta de publicação.

## Licença

Este repositório está sob [licença MIT](LICENSE).
