# Como Instalar

## Passo 1 — Clonar o marketplace (uma vez só)

```bash
cd ~
git clone <url> ai-rodrigues
```

A partir de agora, `~/ai-rodrigues` é a sua cópia local do marketplace.

---

## Passo 2 — Conectar no seu projeto

Escolha a ferramenta que você usa e rode os comandos dentro da pasta do seu projeto.

### Claude Code

```bash
# Criar a pasta se não existir
mkdir -p .claude/skills

# Linkar todas as skills de uma vez
ln -s ~/ai-rodrigues/skills/* .claude/skills/
```

Agora você pode usar `/resumir-texto`, `/traduzir`, etc. no Claude Code.

### Cursor

**Opção A — Skills via symlink (local):**
```bash
# Linkar as skills (usa o mesmo SKILL.md do Claude Code)
mkdir -p .cursor/skills
ln -s ~/ai-rodrigues/skills/* .cursor/skills/
```

**Opção B — Skills remotas (GitHub):**
No Cursor, vá em Settings → Rules → Add Rule → Remote Rule e aponte para o repo no GitHub.

**Para rules (.mdc):**
```bash
mkdir -p .cursor/rules
for skill in ~/ai-rodrigues/skills/*; do
  nome=$(basename "$skill")
  [ -f "$skill/$nome.mdc" ] && ln -s "$skill/$nome.mdc" .cursor/rules/
done
```

### Copilot (VS Code)

**Opção A — Skills via symlink (local):**
```bash
# Linkar as skills (usa o mesmo SKILL.md)
mkdir -p .github/skills
ln -s ~/ai-rodrigues/skills/* .github/skills/
```

**Opção B — Skills remotas (GitHub):**
O Copilot reconhece skills de repos no GitHub automaticamente (`.github/skills/`, `.claude/skills/`, `.agents/skills/`).

---

## Passo 3 — Atualizar (quando tiver novidade)

Quando alguém adicionar uma skill nova no marketplace:

```bash
cd ~/ai-rodrigues
git pull
```

Como seus projetos apontam para o marketplace via symlink, tudo atualiza sozinho. Skills novas que foram adicionadas depois do link precisam ser linkadas de novo (repita o passo 2).

---

## Resumo

| Ação | Comando |
|---|---|
| Clonar (1x) | `git clone <url> ~/ai-rodrigues` |
| Linkar no projeto | Passo 2 acima |
| Atualizar | `cd ~/ai-rodrigues && git pull` |

---

## Dúvidas comuns

**O que é um symlink?**
É um atalho. Em vez de copiar o arquivo, o seu projeto aponta para o original no marketplace. Se o original muda, o seu projeto reflete automaticamente.

**E se eu quiser desconectar?**
Delete o symlink: `rm .cursor/rules/traduzir.mdc` (isso não apaga o original, só o atalho).

**Posso misturar ferramentas?**
Sim. Rode os comandos de cada ferramenta que você usa. Eles não conflitam.
