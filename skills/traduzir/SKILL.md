---
name: traduzir
description: Traduzir texto entre português e inglês mantendo o tom original
argument-hint: [texto para traduzir]
---

Traduza o seguinte conteúdo: $ARGUMENTS

Regras:
1. Se o texto estiver em português, traduza para inglês
2. Se o texto estiver em inglês, traduza para português
3. Mantenha o tom original (formal, informal, técnico)
4. Preserve formatação markdown se houver
5. Não traduza nomes próprios, nomes de ferramentas ou termos técnicos consagrados (ex: deploy, commit, pull request)
6. Apresente o resultado assim:

**Idioma detectado:** [idioma original]

**Tradução:**
[texto traduzido]
