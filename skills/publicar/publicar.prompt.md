Quando o usuário quiser publicar uma skill no marketplace:

## Passo 1 — Ler o arquivo original

Leia o arquivo indicado pelo usuário. Ele pode ser:
- Um SKILL.md (formato Claude Code)
- Um .mdc (formato Cursor)
- Um .prompt.md (formato Copilot)
- Um arquivo markdown genérico com instruções

Identifique o formato pelo frontmatter ou extensão.

## Passo 2 — Encontrar o marketplace

Procure o diretório do marketplace ai-rodrigues:
- ~/ai-rodrigues
- ~/Documents/personal/ai-rodrigues
- Se não encontrar, pergunte ao usuário

## Passo 3 — Extrair informações

Do arquivo original, extraia:
- nome: do campo name do frontmatter, ou do nome do arquivo (sem extensão), em kebab-case
- descrição: do campo description do frontmatter, ou peça ao usuário
- tipo: skill, rule, ou rule condicional
- conteúdo: as instruções (tudo depois do frontmatter)

Se for uma rule condicional, pergunte quais globs usar (ex: **/*.test.*).

Confirme o nome e a descrição com o usuário antes de continuar.

## Passo 4 — Criar a pasta e os 3 formatos

Crie skills/<nome>/ no marketplace com:

### SKILL.md (Claude Code)
Frontmatter com name, description, argument-hint (se for skill invocável).
Adapte o conteúdo para usar $ARGUMENTS se for uma skill.

### <nome>.mdc (Cursor)
Frontmatter com description, globs (se condicional), alwaysApply (true se rule, false se skill).
Adapte o conteúdo sem $ARGUMENTS.

### <nome>.prompt.md (Copilot)
Sem frontmatter. Conteúdo adaptado como texto direto.

## Passo 5 — Atualizar o README

Adicione a nova skill na tabela "Skills disponíveis" do README.md do marketplace.

## Passo 6 — Confirmar

Mostre os 3 arquivos criados e lembre: "Faça commit e push para compartilhar com o time."
