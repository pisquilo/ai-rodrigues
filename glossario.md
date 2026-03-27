# Glossário de IA

Guia de termos e conceitos para entender como usar inteligência artificial de forma avançada.

---

## Conceitos Fundamentais

### LLM (Large Language Model)

Modelo de linguagem treinado com grandes quantidades de texto da internet. É o "cérebro" por trás de ferramentas como ChatGPT, Claude e Gemini. Ele não "pensa" — ele prevê qual é a próxima palavra mais provável dado o texto que recebeu.

**Analogia:** Imagine alguém que leu todos os livros do mundo e consegue continuar qualquer frase que você começar. Não significa que ele entende tudo, mas ele é muito bom em gerar texto coerente.

### Token

A unidade básica que o LLM processa. Não é exatamente uma palavra — pode ser uma palavra inteira, parte de uma palavra, ou um caractere especial. Em português, uma palavra comum como "casa" é 1 token, mas "desenvolvimento" pode ser 2-3 tokens.

**Por que importa:** Você paga por token (entrada + saída), e existe um limite de quantos tokens cabem em uma conversa.

### Contexto (Context Window)

A "memória de trabalho" do LLM durante uma conversa. Tudo que o modelo consegue "ver" ao mesmo tempo — sua pergunta, o histórico da conversa, arquivos anexados, instruções do sistema.

**Analogia:** Imagine uma mesa de trabalho. Quanto maior a mesa, mais documentos você consegue espalhar e consultar ao mesmo tempo. Modelos atuais têm mesas que cabem de 128K a 1M+ tokens.

**Detalhe importante:** Quando o contexto enche, as informações mais antigas começam a ser descartadas ou resumidas. Por isso conversas muito longas podem "esquecer" o que foi dito no início.

### Prompt

O texto que você envia para o LLM. Pode ser uma pergunta simples ou um conjunto elaborado de instruções. A qualidade do prompt influencia diretamente a qualidade da resposta.

---

## Ferramentas e Extensões

### Agent (Agente)

Um LLM que consegue tomar ações no mundo real — ler arquivos, executar código, navegar na web, chamar APIs. Em vez de só responder perguntas, ele planeja e executa tarefas em múltiplos passos.

**Exemplos:** Claude Code e Cursor são agentes. Eles leem seu código, entendem o problema, editam arquivos, rodam testes. Você dá a tarefa, eles executam.

**Diferença chave:** Um chatbot responde. Um agente age.

### Modos do Agente

A maioria dos agentes opera em modos diferentes dependendo de quanta autonomia você dá para eles.

**Plan (Planejar)** — O agente analisa o problema, lê o código e monta um plano do que pretende fazer, mas não executa nada. Você revisa o plano, ajusta se precisar, e só então autoriza. É o melhor modo para começar qualquer tarefa complexa.

**Ask (Perguntar)** — O agente só responde perguntas. Não edita arquivos, não roda comandos. É o modo mais seguro, bom para tirar dúvidas e explorar código sem risco de mudanças acidentais.

**Edit (Editar)** — O agente pode sugerir e fazer mudanças em arquivos, mas pede confirmação antes. Você revisa cada alteração antes de aceitar. É o modo padrão na maioria das ferramentas.

**Agent (Autônomo)** — O agente tem liberdade total. Ele planeja, executa, lê arquivos, roda testes, edita código — tudo sem pedir permissão a cada passo. É o modo mais poderoso, mas exige mais confiança.

| Modo | Lê código | Edita código | Roda comandos | Pede permissão |
|---|---|---|---|---|
| Plan | Sim | Não | Não | — (só mostra o plano) |
| Ask | Sim | Não | Não | — |
| Edit | Sim | Sim | Não | Antes de cada edição |
| Agent | Sim | Sim | Sim | Só quando configurado |

**Dica:** Comece no modo de planejamento — peça para o agente montar um plano antes de executar. Assim você entende o que ele vai fazer, corrige a rota se precisar, e só depois deixa ele agir.

### Sessão

Cada vez que você abre uma conversa nova com um agente, é uma sessão. O agente daquela sessão tem seu próprio contexto e não sabe o que aconteceu em outras sessões (a não ser que tenha memória configurada).

**Detalhe importante:** Cada sessão é um agente independente. Você pode abrir várias sessões ao mesmo tempo — cada uma trabalha separada, com seu próprio contexto. No Claude Code, por exemplo, você pode ter um agente refatorando código em um terminal enquanto outro roda testes em outro terminal. No Cursor, cada janela de chat é uma sessão diferente.

**Analogia:** É como contratar vários assistentes temporários. Cada um sabe só o que você falou para ele. Eles não conversam entre si, mas podem trabalhar ao mesmo tempo em coisas diferentes.

### MCP (Model Context Protocol)

Protocolo aberto criado pela Anthropic que padroniza como LLMs se conectam a ferramentas e fontes de dados externas. É como um "USB-C para IA" — um padrão universal de conexão.

**Exemplo prático:** Em vez de cada ferramenta (Slack, Google Drive, Jira) ter sua própria integração com cada modelo de IA, o MCP define um formato único. Você cria um servidor MCP uma vez e qualquer agente compatível consegue usar.

### Tool Use (Function Calling)

A capacidade do modelo de chamar funções/ferramentas durante uma conversa. O modelo decide quando precisa de uma ferramenta, monta os parâmetros corretos, e usa o resultado para continuar respondendo.

**Exemplo:** Você pergunta "qual a previsão do tempo em SP?". O modelo não sabe a resposta, mas sabe que tem uma ferramenta de clima disponível. Ele chama a ferramenta, recebe os dados, e responde com a informação atualizada.

### Plugin

Extensão que dá uma capacidade nova ao modelo. Por exemplo, um plugin de busca permite que o modelo pesquise na internet, um plugin de calculadora permite cálculos precisos.

**No nosso contexto:** Os plugins que vamos criar neste repositório são pacotes reutilizáveis que adicionam funcionalidades específicas a agentes de IA.

---

## Customização e Regras

### Rules (Regras)

Instruções persistentes que definem como o agente deve se comportar em um projeto. Ficam em arquivos como `CLAUDE.md` ou `.cursorrules` e são carregadas automaticamente em toda conversa.

**Uso prático:** "Sempre escreva código em TypeScript", "Use aspas simples", "Responda em português". Coisas que você não quer repetir toda vez.

### Skills (Habilidades)

Comandos reutilizáveis que encapsulam um fluxo de trabalho completo. Em vez de explicar passo a passo o que fazer, você invoca uma skill com um comando curto.

**Formato padrão:** O arquivo `SKILL.md` é um padrão aberto suportado por Claude Code, Cursor e Copilot. Uma skill escrita uma vez funciona nas três ferramentas.

**Onde ficam:** `.claude/skills/`, `.cursor/skills/`, `.github/skills/` ou `.agents/skills/` (genérico). Podem ser locais no projeto ou remotas (importadas de um repositório GitHub).

**Exemplo:** Em vez de explicar como fazer um commit semântico toda vez, você usa `/smart-commit` e a skill cuida de tudo — analisa mudanças, agrupa por contexto, gera mensagens descritivas.

### Memory (Memória)

Sistema que permite ao agente lembrar informações entre conversas. Preferências do usuário, decisões do projeto, feedback sobre abordagens — tudo fica salvo para que o agente não comece do zero toda vez.

---

Este glossário vai crescer conforme formos criando plugins e skills juntos. Termos novos serão adicionados conforme surgirem na prática.
