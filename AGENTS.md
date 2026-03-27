# AGENTS.md

Instruções para qualquer agente de IA trabalhando neste repositório (Claude Code, Cursor, Copilot).

## O que é este repo

Marketplace de skills e rules de IA para compartilhar entre a família/amigos. O formato principal é `SKILL.md` — padrão aberto que funciona no Claude Code, Cursor e Copilot. Arquivos `.mdc` (Cursor Rules) e `.prompt.md` (Copilot Prompts) são mantidos para rules e compatibilidade. Tudo em português brasileiro.

## Estrutura

- `skills/<nome>/` — cada skill tem `SKILL.md` (formato principal) + `<nome>.mdc` (Cursor Rules) + `<nome>.prompt.md` (Copilot Prompts)
- `docs/` — documentação de referência (comparações, guias)
- `glossario.md` — glossário de termos de IA

## Regra principal

Toda skill criada deve funcionar nas 3 ferramentas (Claude Code, Cursor e Copilot). O `SKILL.md` é o formato principal e compartilhado — as três ferramentas o reconhecem nativamente. Os arquivos `.mdc` e `.prompt.md` são necessários apenas para rules (instruções sempre ativas ou condicionais).

Skills podem ser usadas localmente ou como remote skills importadas via GitHub.

## Convenções para criar skills

### SKILL.md (formato principal — Claude Code, Cursor, Copilot)
```yaml
---
name: nome-da-skill
description: descrição curta
argument-hint: [o que o usuário passa como argumento]
---
```
- Use `$ARGUMENTS` para referenciar a entrada do usuário
- Instruções numeradas e diretas
- Este é o formato padrão aberto reconhecido pelas 3 ferramentas
- Cursor carrega de `.cursor/skills/` ou `.agents/skills/`
- Copilot carrega de `.github/skills/`, `.claude/skills/` ou `.agents/skills/`

### .mdc (Cursor Rules — apenas para rules)
```yaml
---
description: mesma descrição
globs: padrões de arquivo (só para rules condicionais)
alwaysApply: false   # true se for uma Rule (ativa sempre)
---
```
- Sem `$ARGUMENTS` — use "Quando o usuário pedir..." no lugar
- `alwaysApply: true` para rules, `false` para skills
- Adicione `globs` se for uma rule condicional (ex: `**/*.test.*`)
- Para skills invocáveis, prefira o `SKILL.md` — o Cursor agora suporta nativamente

### .prompt.md (Copilot Prompts — legado)
- Sem frontmatter
- Texto direto com as instruções completas
- Sem `$ARGUMENTS`
- Para skills invocáveis, prefira o `SKILL.md` — o Copilot agora suporta nativamente

## Tipos de conteúdo

- **Skill** — invocada sob demanda com `/nome` (ex: `/traduzir`)
- **Rule** — fica ativa o tempo todo no projeto (ex: `portugues-direto`)
- **Rule condicional** — ativa só em certos arquivos via `globs` (ex: `testes-claros` só em arquivos de teste)

## Idioma

Todo conteúdo deve ser escrito em português brasileiro. Termos técnicos sem tradução consagrada ficam em inglês (deploy, commit, merge, skill, rule).
