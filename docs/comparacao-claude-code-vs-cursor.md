# Claude Code vs Cursor

Comparação prática entre as duas ferramentas, mapeando features que cumprem o mesmo papel.

---

## O que são

| | Claude Code | Cursor |
|---|---|---|
| **Tipo** | CLI (terminal) + extensão de IDE | IDE completa (fork do VS Code) |
| **Modelo padrão** | Claude (Anthropic) | Usa vários (Claude, GPT, Gemini) |
| **Onde roda** | Terminal, VS Code, JetBrains | App próprio (substitui o VS Code) |

---

## Features equivalentes

### Regras de projeto

Instruções persistentes que o agente segue automaticamente em toda conversa.

| Claude Code | Cursor |
|---|---|
| `CLAUDE.md` | `.cursorrules` |
| Pode ter por pasta, projeto ou global (`~/.claude/CLAUDE.md`) | Arquivo único na raiz do projeto |
| Hierárquico — regras de subpastas complementam as da raiz | Flat — um arquivo só |

### Comandos reutilizáveis (Skills)

Fluxos de trabalho encapsulados que você invoca com um comando. Ambas as ferramentas usam o mesmo formato padrão aberto: uma pasta com `SKILL.md`.

| Claude Code | Cursor |
|---|---|
| `.claude/skills/<nome>/SKILL.md` | `.cursor/skills/<nome>/SKILL.md` ou `.agents/skills/` |
| Invocado com `/nome-da-skill` | Invocado com `/nome-da-skill` ou automático via Agent |
| Suporta argumentos (`$ARGUMENTS`), injeção de contexto dinâmico | Suporta scripts, references, assets |
| Skills locais ou compartilhadas via repo | Skills locais ou remotas (importadas via GitHub) |

O formato `SKILL.md` é o mesmo padrão aberto — uma skill funciona nas duas ferramentas (e no Copilot também).

### Chat com o código

Conversar com o agente sobre o projeto, pedir explicações, tirar dúvidas.

| Claude Code | Cursor |
|---|---|
| Conversa direto no terminal | Chat panel na sidebar |
| Acessa arquivos via tools (Read, Grep, Glob) | Acessa arquivos via `@file`, `@folder`, `@codebase` |
| Contexto é o diretório de trabalho | Contexto é o workspace aberto |

### Edição de código com IA

Pedir para o agente modificar código existente.

| Claude Code | Cursor |
|---|---|
| Tool `Edit` — aplica diffs no arquivo | Cmd+K — edição inline no editor |
| Mostra diff para aprovação | Mostra diff inline para aceitar/rejeitar |
| Pode editar múltiplos arquivos em sequência | Tab — autocomplete inteligente com contexto |

### Execução de comandos

Rodar comandos no terminal como parte do fluxo.

| Claude Code | Cursor |
|---|---|
| Tool `Bash` — executa qualquer comando | Terminal integrado (manual) |
| O agente decide quando rodar testes, builds, etc. | Precisa pedir explicitamente ou rodar você mesmo |

### Conexão com ferramentas externas (MCP)

Integrar com sistemas externos como Slack, Jira, banco de dados.

| Claude Code | Cursor |
|---|---|
| MCP servers configurados em `settings.json` | MCP servers configurados em settings |
| Suporte completo (tools, resources, prompts) | Suporte a MCP (tools) |

### Memória entre conversas

Lembrar preferências e decisões entre sessões.

| Claude Code | Cursor |
|---|---|
| Memory system (arquivos em `.claude/memory/`) | Notepads + Rules for AI |
| Agente lê e escreve memórias automaticamente | Precisa referenciar manualmente com `@` |

### Contexto de arquivos

Como cada ferramenta entende o código do projeto.

| Claude Code | Cursor |
|---|---|
| Lê arquivos sob demanda (Read, Glob, Grep) | Indexa o codebase inteiro automaticamente |
| Busca é precisa mas explícita | `@codebase` faz busca semântica |
| Agente decide o que ler | Você indica ou ele infere do contexto visual |

### Modelos disponíveis

| Claude Code | Cursor |
|---|---|
| Claude Opus, Sonnet, Haiku | Claude, GPT-4o, Gemini, modelos locais |
| Troca com `/model` | Troca no dropdown do chat |
| Subagentes podem usar modelos diferentes | Modelo único por conversa |

---

## Resumo rápido

| Feature | Claude Code | Cursor |
|---|---|---|
| Regras do projeto | `CLAUDE.md` | `.cursorrules` |
| Skills | `.claude/skills/` | `.cursor/skills/` |
| Chat | Terminal | Sidebar |
| Edição | Diffs via tool | Inline + Tab |
| Terminal | Bash tool (autônomo) | Terminal (manual) |
| MCP | Sim | Sim |
| Memória | Automática | Manual |
| Indexação do código | Sob demanda | Automática |
| Multi-modelo | Claude family | Vários providers |

---

## Quando usar cada um

- **Claude Code** — Quando você quer um agente autônomo que planeja e executa tarefas completas (refatorar, criar features, debugar). Melhor para quem gosta de terminal e quer controle fino.

- **Cursor** — Quando você quer assistência integrada no editor enquanto escreve código. Melhor para quem prefere uma experiência visual com autocomplete e edição inline.

- **Os dois juntos** — Claude Code roda como extensão dentro do Cursor/VS Code. Você pode usar o Cursor para edição rápida e o Claude Code para tarefas maiores.
