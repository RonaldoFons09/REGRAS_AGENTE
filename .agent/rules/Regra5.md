---
trigger: always_on
---

### 5. Padrões de commit e versionamento

**Antes de gerar qualquer commit**
1. Liste os arquivos alterados e classifique cada mudança
2. Se houver tipos ou escopos mistos → proponha commits separados
3. Só então gere a mensagem

**Formato** tipo(escopo): descrição curta no imperativo em PT-BR

- Máximo 72 caracteres, sem ponto final, em minúsculas
- Tipos permanecem em inglês — exceção explícita à regra 1
- Escopo obrigatório quando a mudança é restrita a um módulo
- Escopos sempre em PT-BR e minúsculas; ao usar um novo

**Tipos e SemVer**
| Tipo / situação     | Quando usar                                    | Versão        |
|---------------------|------------------------------------------------|---------------|
| BREAKING CHANGE (!) | Quebra compatibilidade                         | MAJOR (x.0.0) |
| feat                | Nova funcionalidade                            | MINOR (0.x.0) |
| fix / perf          | Correção ou melhoria de performance            | PATCH (0.0.x) |
| refactor            | Reestruturação sem mudança de comportamento    | sem bump      |
| test                | Testes isolados, sem código de produção        | sem bump      |
| docs                | Apenas documentação                            | sem bump      |
| chore               | Build, CI, dependências, configuração          | sem bump      |

Breaking change:
  feat(api)!: remover suporte ao endpoint /v1/legacy
  BREAKING CHANGE: clientes devem migrar para /v2/users até 2025-06.

**Regras por situação**
| Situação                                  | Tipo       | Observação                              |
|-------------------------------------------|------------|-----------------------------------------|
| Código + testes gerados automaticamente   | feat/fix/… | Testes sempre no mesmo commit           |
| Testes adicionados de forma isolada       | test       | Único caso para o tipo `test`           |
| Modularização de múltiplas responsáveis   | refactor   | Um commit único, escopo do módulo atual |
| Clean Code / SOLID isolado                | refactor   | Nunca misturar com feat ou fix          |
| Criação inicial de estrutura de pastas    | chore      | —                                       |
| Reorganização de módulos existentes       | refactor   | —                                       |
| Inicialização de docs/                    | docs       | —                                       |
| Encerramento de sessão (historia.md)      | docs       | docs(historia): sessão [DD/MM/AAAA]     |

**Branches**

| Situação                          | Branch                  | Base    |
|-----------------------------------|-------------------------|---------|
| feat ou mudança em 2+ módulos     | feature/nome-descritivo | develop |
| fix de impacto médio              | fix/nome-descritivo     | develop |
| fix isolado                       | branch atual            | —       |
| hotfix em produção                | hotfix/nome-descritivo  | main    |

**Corpo e rodapé**

Incluir quando a mudança não é óbvia pelo título ou houve decisão de design relevante:

  tipo(escopo): descrição curta

  Explique o PORQUÊ. Máximo 3–4 linhas.

  Closes #<issue> | Ref: <TASK-ID> | BREAKING CHANGE: ...

**Reverts**

  revert: feat(auth): adicionar login com Google
  This reverts commit <hash>. Motivo: [razão do revert]

**Nunca fazer**
- ❌ `fix: corrigido bug` — vago, no passado, sem escopo
- ❌ `feat: várias melhorias` — viola atomicidade
- ❌ `WIP: salvando progresso` — use `git stash`
- ❌ Traduzir tipos para PT-BR — quebra ferramentas de automação
- ❌ Usar escopo não registrado em `docs/arquitetura.md`