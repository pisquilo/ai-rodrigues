# ai-rodrigues

Marketplace de skills e rules de IA para a família/amigos. Tudo que criamos juntos para usar com Claude Code, Cursor e Copilot fica aqui.

---

## Como funciona

Todas as skills usam o formato `SKILL.md` — um padrão aberto reconhecido pelo Claude Code, Cursor e Copilot. Uma skill escrita uma vez funciona nas três ferramentas.

Skills podem ser usadas de duas formas:
- **Local** — copie a pasta para o diretório de skills do seu projeto
- **Remota** — importe direto deste repo no GitHub

| Ferramenta | Diretório de skills | Remote skills |
|---|---|---|
| Claude Code | `.claude/skills/` | — |
| Cursor | `.cursor/skills/` | Settings → Rules → Remote Rule (GitHub) |
| Copilot | `.github/skills/` | Reconhece repos no GitHub automaticamente |

---

## Skills disponíveis

| Skill | O que faz | Tipo |
|---|---|---|
| [resumir-texto](skills/resumir-texto/) | Resume textos longos em bullet points | Skill |
| [traduzir](skills/traduzir/) | Traduz entre português e inglês | Skill |
| [explicar-codigo](skills/explicar-codigo/) | Explica código para quem está aprendendo | Skill |
| [setup](skills/setup/) | Conecta o marketplace no seu projeto via symlinks | Skill |
| [publicar](skills/publicar/) | Publica uma skill nova no marketplace | Skill |
| [testes-claros](skills/testes-claros/) | Convenções para testes legíveis | Rule condicional |
| [portugues-direto](skills/portugues-direto/) | Respostas em PT-BR, diretas e sem enrolação | Rule |
| [codigo-limpo](skills/codigo-limpo/) | Boas práticas de código | Rule |

---

## Como usar

### Opção 1 — Remote skill (mais simples)

No Cursor ou Copilot, aponte para este repo no GitHub. A ferramenta importa as skills automaticamente.

### Opção 2 — Local via symlink

```bash
# Claude Code
mkdir -p .claude/skills
ln -s ~/ai-rodrigues/skills/* .claude/skills/

# Cursor
mkdir -p .cursor/skills
ln -s ~/ai-rodrigues/skills/* .cursor/skills/

# Copilot
mkdir -p .github/skills
ln -s ~/ai-rodrigues/skills/* .github/skills/
```

### Diferença entre Skill e Rule

- **Skill** — Você invoca quando quiser (ex: `/traduzir olá mundo`)
- **Rule** — Fica ativa o tempo todo no projeto (ex: sempre responder em português)
- **Rule condicional** — Ativa só em certos tipos de arquivo (ex: `testes-claros` só em arquivos de teste)

---

## Estrutura de cada skill

```
skills/nome-da-skill/
└── SKILL.md              ← Formato único (Claude Code, Cursor, Copilot)
```

---

## Documentação

- [Glossário de IA](glossario.md) — Termos e conceitos explicados de forma simples
- [Claude Code vs Cursor](docs/comparacao-claude-code-vs-cursor.md) — Comparação entre as ferramentas

---

## Como contribuir

1. Crie uma pasta em `skills/<nome>/`
2. Adicione um `SKILL.md` com frontmatter (`name`, `description`)
3. Atualize este README
