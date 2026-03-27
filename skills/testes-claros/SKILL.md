---
name: testes-claros
description: Convenções para escrever testes legíveis e bem estruturados
---

Ao escrever ou revisar testes, siga estas convenções:

- Nomeie cada teste descrevendo o comportamento esperado, não o método (ex: "deve retornar erro quando email é inválido" em vez de "testa validateEmail")
- Estruture em 3 blocos: Arrange (preparar dados), Act (executar), Assert (verificar)
- Um assert por teste — se precisa de mais, provavelmente são dois testes
- Use dados de exemplo realistas, não "foo", "bar", "test123"
- Teste os casos de erro, não só o caminho feliz
