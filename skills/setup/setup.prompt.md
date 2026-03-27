Quando o usuário pedir para instalar ou conectar o marketplace ai-rodrigues no projeto:

## Passo 1 — Encontrar o marketplace

Procure o diretório do marketplace ai-rodrigues. Verifique:
- ~/ai-rodrigues
- ~/Documents/personal/ai-rodrigues
- Se não encontrar, pergunte ao usuário

## Passo 2 — Atualizar o marketplace

Rode no terminal:
```bash
cd <caminho-do-marketplace> && git pull
```

## Passo 3 — Identificar o projeto alvo

Pergunte ao usuário o caminho do projeto, ou use o projeto aberto no editor.

## Passo 4 — Detectar ferramentas

Verifique o que existe no projeto:
- .claude/ ou CLAUDE.md → Claude Code
- .cursor/ → Cursor
- .github/ → Copilot
- Se nenhum for encontrado, pergunte qual ferramenta o usuário usa

## Passo 5 — Criar symlinks

Rode os comandos no terminal para cada ferramenta detectada:

### Claude Code:
```bash
mkdir -p <projeto>/.claude/skills
for skill in <marketplace>/skills/*/; do
  nome=$(basename "$skill")
  [ ! -e "<projeto>/.claude/skills/$nome" ] && ln -s "$skill" "<projeto>/.claude/skills/$nome"
done
```

### Cursor:
```bash
mkdir -p <projeto>/.cursor/rules
for skill in <marketplace>/skills/*/; do
  nome=$(basename "$skill")
  [ ! -e "<projeto>/.cursor/rules/$nome.mdc" ] && ln -s "$skill/$nome.mdc" "<projeto>/.cursor/rules/$nome.mdc"
done
```

### Copilot:
```bash
mkdir -p <projeto>/.github/prompts
for skill in <marketplace>/skills/*/; do
  nome=$(basename "$skill")
  [ ! -e "<projeto>/.github/prompts/$nome.prompt.md" ] && ln -s "$skill/$nome.prompt.md" "<projeto>/.github/prompts/$nome.prompt.md"
done
```

## Passo 6 — Confirmar

Mostre o que foi feito e lembre: "Para atualizar no futuro, rode este comando de novo."
