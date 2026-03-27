---
name: publicar
description: Publica uma skill nova no marketplace ai-rodrigues a partir de um arquivo local
argument-hint: [caminho do arquivo da skill]
---

O usuário criou uma skill e quer adicionar no marketplace ai-rodrigues.

## Passo 1 — Ler o arquivo original

Leia o arquivo em $ARGUMENTS. Ele pode ser:
- Um `SKILL.md` (formato Claude Code)
- Um `.mdc` (formato Cursor)
- Um `.prompt.md` (formato Copilot)
- Um arquivo markdown genérico com instruções

Identifique o formato pelo frontmatter ou extensão.

## Passo 2 — Encontrar o marketplace

Procure o diretório do marketplace ai-rodrigues:
- `~/ai-rodrigues`
- `~/Documents/personal/ai-rodrigues`
- Se não encontrar, pergunte ao usuário

## Passo 3 — Extrair informações

Do arquivo original, extraia:
- **nome**: do campo `name` do frontmatter, ou do nome do arquivo (sem extensão), em kebab-case
- **descrição**: do campo `description` do frontmatter, ou peça ao usuário
- **tipo**: skill (`alwaysApply: false`) ou rule (`alwaysApply: true`), ou pergunte ao usuário
- **conteúdo**: as instruções (tudo depois do frontmatter)

Se for uma rule condicional, pergunte quais `globs` usar (ex: `**/*.test.*`).

Confirme o nome e a descrição com o usuário antes de continuar.

## Passo 4 — Criar a pasta e os arquivos

Crie `<marketplace>/skills/<nome>/`:

### SKILL.md (formato principal — Claude Code, Cursor, Copilot)
```yaml
---
name: <nome>
description: <descrição>
argument-hint: <hint se for skill, omita se for rule>
---
```
- Adapte o conteúdo para usar `$ARGUMENTS` se for uma skill invocável
- Este é o formato padrão reconhecido pelas 3 ferramentas

### <nome>.mdc (só se for uma rule)
Crie apenas se o tipo for rule ou rule condicional:
```yaml
---
description: <descrição>
globs: <padrões se for rule condicional>
alwaysApply: <true se rule, false se skill>
---
```
- Adapte o conteúdo sem `$ARGUMENTS`

## Passo 5 — Atualizar o README

Abra o `README.md` do marketplace e adicione a nova skill na tabela "Skills disponíveis", na posição correta pelo tipo (Skills primeiro, depois Rules condicionais, depois Rules).

## Passo 6 — Confirmar

Mostre ao usuário:
- "Skill `<nome>` publicada no marketplace!"
- Liste os 3 arquivos criados
- Lembre: "Faça commit e push para compartilhar com o time"
