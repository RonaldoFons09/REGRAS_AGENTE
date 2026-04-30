---
trigger: always_on
---

### 2. Testes Automatizados (TDD + Cobertura)

Você deve sempre seguir o ciclo **TDD (Red → Green → Refactor)** de forma disciplinada. Nunca escreva código de produção antes de ter um teste falhando que valide o comportamento esperado.

**Para funcionalidades novas:**
1. Escreva primeiro os testes (Red) que descrevem claramente o comportamento esperado, incluindo casos de sucesso, borda e erro.
2. Implemente o mínimo de código necessário para fazer os testes passarem (Green).
3. Refatore o código e os testes mantendo todos os testes verdes (Refactor).

**Para refatorações ou alterações em código existente:**
- Mantenha os testes existentes verdes.
- Atualize ou adicione testes para cobrir as mudanças realizadas.
- Garanta cobertura 100% no módulo ou arquivo afetado.

**Em todos os casos:**
- Use **pytest** como framework principal.
- Escreva testes pequenos, focados, com nomes descritivos (ex: `test_calcula_desconto_cliente_vip`).
- Priorize testes de comportamento e lógica de negócio.
- **Exclusões permitidas** (não exigem cobertura):
  - Arquivos de configuração
  - DTOs / models simples
  - Getters, setters e propriedades triviais
- Informe explicitamente:
  - Módulos/arquivos testados
  - Casos de borda relevantes cobertos

**Execução obrigatória:**
pytest --cov=. --cov-fail-under=100 -q --cov-report=term-missing

Regra de Ouro: Testes são parte obrigatória do código entregue. Nunca entregue funcionalidade sem os testes correspondentes e cobertura validada. Cobertura alta no código crítico é mais importante que cobertura artificial em código trivial.