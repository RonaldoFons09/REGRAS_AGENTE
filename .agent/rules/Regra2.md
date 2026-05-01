---
trigger: always_on
---

# 2. Testes Automatizados (TDD + Cobertura)

Você deve sempre seguir o ciclo **TDD (Red → Green → Refactor)** de forma disciplinada. Nunca escreva código de produção antes de ter um teste falhando que valide o comportamento esperado.

---

## 🔴 Para funcionalidades novas

1. Escreva primeiro os testes **(Red)** que descrevem claramente o comportamento esperado, incluindo casos de sucesso, borda e erro.
2. Implemente o **mínimo de código necessário** para fazer os testes passarem **(Green)**.
3. Refatore o código e os testes mantendo todos os testes verdes **(Refactor)**.

---

## 🔁 Para refatorações ou alterações em código existente

- Mantenha os testes existentes verdes.
- Atualize ou adicione testes para cobrir as mudanças realizadas.
- Garanta cobertura 100% de **linhas e branches** no módulo ou arquivo afetado.

---

## 🐛 Para correção de bugs

1. Escreva primeiro um teste que **reproduza o bug** (Red) — antes de qualquer correção.
2. Corrija o código para fazer o teste passar (Green).
3. Verifique que nenhum teste existente foi quebrado (Refactor).

> Isso garante rastreabilidade e impede regressões futuras.

---

## ✅ Em todos os casos

### Framework e execução

- Use **pytest** como framework principal.
- Execute sempre com cobertura de linhas **e branches**:

```bash
pytest --cov=. --cov-fail-under=100 --cov-branch -q --cov-report=term-missing
```

### Qualidade dos testes

- Escreva testes pequenos, focados, com nomes descritivos:
  - ✅ `test_calcula_desconto_cliente_vip`
  - ✅ `test_rejeita_pedido_com_estoque_zerado`
  - ❌ `test_1`, `test_funcao`
- Priorize testes de **comportamento e lógica de negócio**, não de implementação interna.
- Testes não devem depender de **ordem de execução** — cada teste deve ser completamente isolado.
- Proibido `time.sleep` real — use mocks de tempo (`freezegun`, `unittest.mock.patch`).
- Proibido chamadas reais a APIs externas, LLMs ou bancos de dados em testes unitários — use mocks (`unittest.mock`, `pytest-mock`, `respx`, `httpx`).

### Organização

- Use **fixtures** para setup reutilizável e **factories** (ex: `factory_boy`) para criação de objetos complexos.
- Separe testes unitários de testes de integração com markers:

```toml
# pyproject.toml
[tool.pytest.ini_options]
markers = [
    "unit: testes unitários isolados (sem I/O real)",
    "integration: testes que envolvem I/O real (banco, APIs, LLMs)",
]
```

```python
# Exemplo de uso
@pytest.mark.unit
def test_calcula_desconto_cliente_vip():
    ...

@pytest.mark.integration
def test_salva_pedido_no_banco():
    ...
```

- Testes de integração devem rodar em ambiente controlado (ex: banco em Docker, APIs em sandbox).

---

## 🚫 Exclusões permitidas (não exigem cobertura)

| Tipo                              | Exemplos                              |
|-----------------------------------|---------------------------------------|
| Arquivos de configuração          | `settings.py`, `config.py`            |
| DTOs / models simples             | Apenas campos, sem lógica             |
| Getters, setters e propriedades triviais | `@property` sem lógica          |
| Entrypoints de aplicação          | `main.py`, `app.py` sem lógica        |

Exclusões devem ser declaradas explicitamente no `pyproject.toml`:

```toml
[tool.coverage.report]
omit = [
    "*/config/*",
    "*/settings*",
    "*/migrations/*",
    "main.py",
]
```

---

## 📋 Informe explicitamente ao entregar

- Módulos/arquivos testados
- Casos de borda relevantes cobertos
- Se algum módulo foi excluído da cobertura e por quê
- Output do pytest com cobertura

---

> **Regra de Ouro:** Testes são parte obrigatória do código entregue. Nunca entregue funcionalidade sem os testes correspondentes e cobertura validada. Cobertura alta no código crítico é mais importante que cobertura artificial em código trivial. Um teste que não pode falhar não tem valor.