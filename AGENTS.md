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

## Git Commit Rules (MANDATORY)

**ALL commit messages MUST follow the Angular Conventional Commits specification in ENGLISH.**

### Format

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Types

| Type       | Description                                          |
|------------|------------------------------------------------------|
| `feat`     | A new feature                                        |
| `fix`      | A bug fix                                            |
| `docs`     | Documentation only changes                           |
| `style`    | Changes that do not affect the meaning of the code   |
| `refactor` | A code change that neither fixes a bug nor adds a feat |
| `perf`     | A code change that improves performance              |
| `test`     | Adding missing tests or correcting existing tests    |
| `chore`    | Changes to the build process or auxiliary tools      |
| `ci`       | Changes to CI configuration files and scripts        |
| `build`    | Changes that affect the build system or dependencies |

### Rules

- **ALWAYS use English** for type, scope, and description
- **Lowercase** for type and scope
- **No period** at the end of the description
- **Maximum 72 characters** in the subject line
- Use **present imperative** in the description (e.g., "add feature" NOT "added feature")

### Examples

```
feat(auth): add login with Google
fix(api): handle null user id gracefully
docs: update contributing guidelines
refactor(core): simplify event handler logic
test(utils): add edge cases for date parser
chore: bump node version to 22
```
