---
name: setup
description: Atualiza o marketplace e conecta as skills no projeto via symlinks
argument-hint: [caminho do projeto]
---

O usuário quer instalar ou atualizar as skills do marketplace ai-rodrigues no projeto dele.

## Passo 1 — Encontrar o marketplace

Procure o diretório do marketplace ai-rodrigues. Ele pode estar em:
- `~/ai-rodrigues`
- `~/Documents/personal/ai-rodrigues`
- O diretório atual (se tiver a pasta `skills/` na raiz com SKILL.md dentro)
- Se não encontrar, pergunte ao usuário

## Passo 2 — Atualizar o marketplace

Rode `git pull` dentro da pasta do marketplace para pegar as últimas novidades.

## Passo 3 — Identificar o projeto alvo

- Se $ARGUMENTS tem um caminho, use esse
- Se não, pergunte ao usuário qual projeto quer conectar

## Passo 4 — Detectar ferramentas do projeto

Verifique o que existe no projeto:
- `.claude/` ou `CLAUDE.md` → Claude Code
- `.cursor/` → Cursor
- `.github/` → Copilot
- Se nenhum for encontrado, pergunte qual ferramenta o usuário usa

## Passo 5 — Criar symlinks

Para cada ferramenta detectada, crie os symlinks. Pule arquivos que já existem.

### Claude Code:
```bash
mkdir -p <projeto>/.claude/skills
# Para cada skill no marketplace:
ln -s <marketplace>/skills/<nome> <projeto>/.claude/skills/<nome>
```

### Cursor:
```bash
# Skills (formato SKILL.md — compartilhado)
mkdir -p <projeto>/.cursor/skills
ln -s <marketplace>/skills/<nome> <projeto>/.cursor/skills/<nome>

# Rules (.mdc — para rules sempre ativas e condicionais)
mkdir -p <projeto>/.cursor/rules
ln -s <marketplace>/skills/<nome>/<nome>.mdc <projeto>/.cursor/rules/<nome>.mdc
```

### Copilot:
```bash
# Skills (formato SKILL.md — compartilhado)
mkdir -p <projeto>/.github/skills
ln -s <marketplace>/skills/<nome> <projeto>/.github/skills/<nome>
```

## Passo 6 — Confirmar

Mostre o que foi feito:
- Quantas skills foram linkadas
- Para quais ferramentas
- Lembre o usuário: "Para atualizar no futuro, é só rodar /setup de novo"
