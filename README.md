# ai-rodrigues

Marketplace de skills e rules de IA para a família/amigos. Tudo que criamos juntos para usar com Claude Code, Cursor e Copilot fica aqui.

---

## Onde cada ferramenta guarda suas configurações

| Feature | Claude Code | Cursor | Copilot |
|---|---|---|---|
| Rules sempre ativas | `CLAUDE.md` | `.mdc` com `alwaysApply: true` | `copilot-instructions.md` |
| Rules condicionais | — | `.mdc` com `globs` | — |
| Skills | `.claude/skills/` | `.cursor/skills/` | `.github/skills/` |

As três ferramentas usam o mesmo formato `SKILL.md` (padrão aberto). Skills podem ser locais ou remotas (importadas via GitHub).

---

## Skills disponíveis

Cada pasta tem os 3 formatos (Claude Code, Cursor, Copilot) — copie o que precisar para o seu projeto.

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

### Claude Code

1. Copie a pasta inteira da skill para `.claude/skills/` no seu projeto
2. Use `/<nome>` para invocar (ex: `/resumir-texto`)
3. Para rules, copie o conteúdo do `SKILL.md` para o `CLAUDE.md` do seu projeto

### Cursor

1. Copie a pasta da skill para `.cursor/skills/` no seu projeto (usa o mesmo `SKILL.md`)
2. Ou importe como remote skill via Settings → Rules → Add Rule → Remote Rule (GitHub)
3. Para rules, copie o `.mdc` para `.cursor/rules/`

### Copilot (VS Code)

1. Copie a pasta da skill para `.github/skills/` no seu projeto (usa o mesmo `SKILL.md`)
2. Ou referencie como remote skill a partir do repo no GitHub
3. Para rules, copie o conteúdo para `.github/copilot-instructions.md`

### Diferença entre Skill, Rule e Rule condicional

- **Skill** — Você invoca quando quiser (ex: `/traduzir olá mundo`)
- **Rule** — Fica ativa o tempo todo no projeto (ex: sempre responder em português)
- **Rule condicional** — Ativa só quando você está editando certo tipo de arquivo (ex: `testes-claros` ativa só em arquivos de teste)

---

## Estrutura de cada skill

```
skills/nome-da-skill/
├── SKILL.md              ← Formato padrão (Claude Code, Cursor, Copilot)
├── nome.mdc              ← Cursor Rules (para rules, não skills)
└── nome.prompt.md        ← Copilot Prompts (legado)
```

O `SKILL.md` é o formato principal e funciona nas 3 ferramentas. Os arquivos `.mdc` e `.prompt.md` são mantidos para rules e compatibilidade.

---

## Documentação

- [Glossário de IA](glossario.md) — Termos e conceitos explicados de forma simples
- [Claude Code vs Cursor](docs/comparacao-claude-code-vs-cursor.md) — Comparação entre as ferramentas

---

## Como contribuir

1. Crie uma pasta em `skills/<nome>/`
2. Adicione os 3 formatos: `SKILL.md`, `<nome>.mdc` e `<nome>.prompt.md`
3. Atualize este README
