# Museu de Bugs

Diário técnico em Markdown (frontmatter YAML), versionado no GitHub — mais para registar o meu dia a dia do que para um «blog de autoridade», mas aberto ao público para quem quiser aprender com a minha experiência.

## Objetivo

Documentar o meu dia a dia técnico: um caderno para mim — bugs, ferramentas, tecnologia, opiniões pessoais e o que mais me apetecer registar. O foco é utilidade para mim; quem chegar de fora aproveita o que fizer sentido. Repositório (e site, se houver) públicos, sem obrigação de actuar para o público.

## Como usar este repositório

1. Copia `templates/post-template.md` para `drafts/` ou para `posts/AAAA/` (ano do post).
2. Preenche o frontmatter: `title`, `date`, `tags`, `status`, `slug`, `description`.
3. Escreve o corpo nas secções **Introdução**, **Desenvolvimento** e **Conclusão**, ou muda os títulos se preferires.
4. Guarda imagens em `assets/images/` e referencia-as no Markdown com o caminho que o teu gerador de site esperar.
5. Quando quiseres «fechar» um post, move-o de `drafts/` para `posts/AAAA/` e ajusta `status` no frontmatter (por exemplo `published`).

### Convenção de nomenclatura de ficheiros

Usa **kebab-case** com a data no início:

`YYYY-MM-DD-titulo-do-post.md`

Exemplo: `2025-05-02-notas-sobre-um-bug-estranho.md`

### Posts recentes

| Data | Título | Tags | Status |
|------|--------|------|--------|
| | | | |

*(Atualiza a tabela manualmente quando publicares, ou deixa para um script futuro.)*

### Fluxo de branches (opcional, só tu no repositório)

- **main** — linha principal: o que consideras estado actual e fiável para o blog.
- **drafts** — branch opcional para experimentar vários rascunhos ou reorganizar pastas sem mexer em `main` até estares satisfeito.
- **review/nome-do-post** — branch opcional por texto: rever no GitHub (diff, preview) e depois fazer merge em `main`; podes apagar a branch depois do merge.

Se preferires simplicidade, usa só `main` e commits directos; as outras branches são conveniência, não obrigação.
