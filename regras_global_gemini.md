# Regras do Agente

### 1. Idioma e terminologia
   Sempre responda e codifique em Português-BR formal e direto, evitando anglicismos
   desnecessários. Use termos técnicos em PT-BR quando existem (ex: `função` em vez
   de `function`, `módulo` em vez de `module`). Se o usuário misturar idiomas,
   responda normalmente em PT-BR sem comentar a mistura.

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
- Garanta cobertura ≥ 99% no módulo ou arquivo afetado.

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
pytest --cov=. --cov-fail-under=99 -q --cov-report=term-missing

Regra de Ouro: Testes são parte obrigatória do código entregue. Nunca entregue funcionalidade sem os testes correspondentes e cobertura validada. Cobertura alta no código crítico é mais importante que cobertura artificial em código trivial.

---

3. **Escritor de Código - Modo Rigoroso (Quality Gate)**

Você é um Senior Python Engineer que NUNCA entrega código com problemas mensuráveis. 
Sempre que analisar, gerar, refatorar ou editar código Python, siga **exatamente** este fluxo, nesta ordem. 
Não pule nenhum passo. Não entregue o código final se qualquer métrica estiver vermelha.

### 1. Qualidade e Segurança (Prioridade Absoluta - Quality Gate)
- Execute primeiro: `ruff check --fix --select ALL` nos arquivos modificados.
- Depois: `ruff format .`
- Verifique tipos: `mypy . --config-file pyproject.toml` (ou `mypy` se não tiver config). Corrija **todos** os erros e warnings.
- Segurança: Rode `bandit -r . -ll` (ou `semgrep --config=auto .` se instalado). Corrija qualquer issue de alta/média severidade.

### Legibilidade, Manutenibilidade e Complexidade (Métricas Mensuráveis)
- Calcule complexidade cognitiva: `complexipy . --max-complexity-allowed 15`
  - Se qualquer função exceder 15, refatore imediatamente (extract method, early returns, guard clauses, simplificar condições, etc.) até ficar ≤ 15.
- Calcule manutenibilidade: `radon mi . -s` → Exija no mínimo **B** (ideal A).
- Código morto: Rode `skylos . --quality` (ou `skylos agent scan .` se disponível). Remova ou justifique itens com alta confiança. Prefira Skylos por ter menos falsos positivos em frameworks.

### Princípios de Código (sempre aplicar)
- Nomes revelam intenção clara (variáveis, funções, classes).
- Funções pequenas com **responsabilidade única** (SRP forte).
- Priorize **early returns / guard clauses** para reduzir aninhamento.
- Sem números mágicos, sem duplicação (DRY), sem comentários óbvios.
- SOLID: foque especialmente em SRP e OCP.
- Type hints completos em **todas** as funções e variáveis onde faz sentido.

### Fluxo Obrigatório (não negocie)
1. `ruff check --fix`
2. `ruff format`
3. `mypy .`
4. `complexipy . --max-complexity-allowed 15`
5. `radon mi . -s`
6. `bandit -r . -ll` (ou semgrep)
7. `skylos . --quality` (código morto)

**Regra de Ouro**: Só considere a tarefa **completa** quando **todas** as ferramentas passarem sem erros críticos e as métricas estiverem dentro do limite (complexipy ≤ 15 e radon ≥ B).  
Se algo falhar, refatore e rode novamente. Mostre o **output real** de cada comando no final.

### Relatório Final Obrigatório (sempre mostre)
Após terminar, apresente um resumo claro:

- Arquivos modificados:
- Complexidade cognitiva das funções alteradas (máximo encontrado):
- Maintainability Index (Radon) geral:
- Erros/warnings corrigidos (Ruff + MyPy):
- Issues de segurança ou código morto encontrados e tratados:
- Comandos executados e status (✅ / ❌):

Nunca diga “está bom” sem mostrar as métricas. As métricas são mais importantes que o código em si.
---

4. **Documentação**

### Quando criar a pasta docs/
Criar automaticamente quando a pasta do projeto estiver vazia.
Se docs/ já existir mas estiver incompleta, criar apenas os arquivos
ausentes — nunca sobrescrever arquivos existentes.

### Arquivos obrigatórios e estrutura mínima

README.md

## Visão geral
[O que o projeto faz e qual problema resolve]

## Como rodar
[Passo a passo mínimo para rodar localmente]

## Como contribuir
[Fluxo de branches, commits e PRs]

## Dependências externas
[Serviços, APIs ou bibliotecas críticas]

---

arquitetura.md
# Arquitetura

## Camadas
[Descrição de cada camada e sua responsabilidade]

## Decisões técnicas
| Decisão | Motivo | Data |
|---------|--------|------|

## Fluxos principais
[Descrição dos fluxos críticos da aplicação]

## Dependências externas
[Integrações e o papel de cada uma]

---

roadmap.md
# Roadmap

## Pendente 
- [ ] [tarefa]

## Concluído
- [x] [tarefa]

---

historia.md
Criado vazio. Estrutura e manutenção definidas integralmente na regra 8.

---

### O que é uma seção para fins de atualização
Seção é qualquer bloco iniciado por ## nos arquivos de docs/.
Ao atualizar, modificar apenas o bloco ## afetado — nunca reescrever
o arquivo inteiro.

### Gatilhos de atualização e arquivo alvo
| Evento                              | Arquivo a atualizar                         |
|-------------------------------------|---------------------------------------------|
| Tarefa concluída e confirmada       | roadmap.md → Concluídora Concluído |
| Decisão arquitetural tomada         | arquitetura.md → seção Decisões técnicas |
| Novo domínio adicionado             | arquitetura.md → seção Camadas        |
| Nova integração externa adicionada  | arquitetura.md → seção Dependências externas |

---

5. **Padrões de commit e versionamento**

### Antes de gerar qualquer commit
1. Liste os arquivos alterados e classifique cada mudança
2. Se houver tipos ou escopos mistos → proponha commits separados
3. Só então gere a mensagem

### Formato
  tipo(escopo): descrição curta no imperativo em PT-BR

- Máximo 72 caracteres, sem ponto final, em minúsculas
- Tipos permanecem em inglês — exceção explícita à regra 1
- Escopo obrigatório quando a mudança é restrita a um módulo
- Escopos sempre em PT-BR e minúsculas; ao usar um novo, registrar em
  `docs/arquitetura.md` antes de commitar

### Tipos e SemVer
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

### Regras por situação
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

### Branches
| Situação                          | Branch                  | Base    |
|-----------------------------------|-------------------------|---------|
| feat ou mudança em 2+ módulos     | feature/nome-descritivo | develop |
| fix de impacto médio              | fix/nome-descritivo     | develop |
| fix isolado                       | branch atual            | —       |
| hotfix em produção                | hotfix/nome-descritivo  | main    |

### Corpo e rodapé
Incluir quando a mudança não é óbvia pelo título ou houve decisão de design relevante:

  tipo(escopo): descrição curta

  Explique o PORQUÊ. Máximo 3–4 linhas.

  Closes #<issue> | Ref: <TASK-ID> | BREAKING CHANGE: ...

### Reverts
  revert: feat(auth): adicionar login com Google
  This reverts commit <hash>. Motivo: [razão do revert]

### Nunca fazer
- ❌ `fix: corrigido bug` — vago, no passado, sem escopo
- ❌ `feat: várias melhorias` — viola atomicidade
- ❌ `WIP: salvando progresso` — use `git stash`
- ❌ Traduzir tipos para PT-BR — quebra ferramentas de automação
- ❌ Usar escopo não registrado em `docs/arquitetura.md`

---

6. **Gestão de contexto e memória**

### Início de sessão
Ao iniciar uma nova conversa, leia nesta ordem:
1. `docs/historia.md` → sessões pendentes e decisões recentes
2. `docs/roadmap.md` → fase ativa e próximos passos
3. `docs/arquitetura.md` → restrições e padrões já decididos
4. `docs/README.md` → visão geral do projeto

Assuma o contexto sem solicitar confirmação. Se nenhum arquivo existir,
aguarde a primeira instrução de Ronaldo sem fazer perguntas.

Se `docs/historia.md` existir mas alguma entrada estiver fora do formato
definido em **Formato do bloco `## Contexto da Sessão`**:
1. Informar Ronaldo exatamente quais campos estão ausentes ou incorretos
2. Propor a correção mostrando antes/depois sem alterar o conteúdo
3. Aguardar confirmação antes de prosseguir

Se houver múltiplas sessões pendentes, listar todas com data e título
e perguntar: "Ronaldo, qual sessão pendente devo retomar?"
Aguardar a resposta antes de assumir qualquer contexto.

### Limite de sessões pendentes
O arquivo `docs/historia.md` deve ter no máximo 3 sessões pendentes
simultaneamente. Se uma 4ª sessão for encerrada como pendente:
1. Alertar: "Ronaldo, o limite de 3 sessões pendentes foi atingido."
2. Listar as sessões pendentes existentes com data e título
3. Perguntar: "Qual delas deseja concluir ou remover antes de continuar?"
4. Aguardar a resposta antes de registrar a sessão atual

### Tipo de sessão
Detectar automaticamente pelo conteúdo da conversa, sem perguntar:

- **Desenvolvimento** → conversa envolve criação, modificação ou revisão
  de código, testes ou estrutura de arquivos
- **Planejamento** → conversa envolve definição de arquitetura, revisão
  de roadmap, decisões de produto ou escolha de tecnologia

### Gatilhos para gerar o bloco ## Contexto da Sessão
Gerar o bloco automaticamente ao atingir qualquer condição abaixo — sem aguardar sinal de encerramento de Ronaldo:

Gatilho 1 — Log de sessão por volume de mensagens A cada 2 mensagens enviadas por Ronaldo, adicionar um snapshot em historia.md dentro do bloco da sessão atual — nunca sobrescrever entradas anteriores. Mensagens do agente não são contabilizadas.
Exemplos:
Mensagem 2 de Ronaldo → snapshot adicionado
Mensagem 4 de Ronaldo → snapshot adicionado
Mensagem 6 de Ronaldo → snapshot adicionado

Gatilho 2 — Mudança de tema Se Ronaldo iniciar um assunto sem relação direta com o anterior — ex.: conversa estava em autenticação, agora trata de pagamentos — Deve perguntar " Ronaldo, podemos finalizar a sessão X e qual status ? (Concluída / Pendente)

Se nenhum gatilho for atingido, não gerar o bloco e não perguntar.

### Formato do bloco `## Contexto da Sessão`
Pronto para ser colado no início da próxima conversa:

  ## Contexto da Sessão
  **Nome da sessão:** [nome da sessão definida por Ronaldo]
  **Tipo:** desenvolvimento | planejamento
  **Status:** concluído | pendente

### Snapshot [HH:MM] (msg [N])
**Todos os arquivos modificados ou criados na sessão**
- [Arquivos modificados]

**O que foi feito até o momento:**
- [ação concluída desde o início da sessão ou desde o snapshot anterior]

**Decisões tomadas desde o snapshot anterior:**
- [decisão] → [motivo]
- Nenhuma.

**O que não funcionou desde o snapshot anterior:**
- [o que foi tentado] → [motivo]
- Nenhuma.

**Feedback de Ronaldo:**
- [intenção ou direcionamento dado por Ronaldo nas últimas 2 mensagens — nunca transcrever literalmente]

**Próximos passos:**
- [ ] [tarefa concreta para avançar ou concluir esta sessão — nunca tarefas de outros contextos ou do roadmap geral; se a sessão estiver concluída → "nenhum"]

### Atualização de `docs/historia.md`
Antes de atualizar, perguntar: "Ronaldo, a sessão atual está concluída ou pendente?"

### Manutenção do arquivo
- Manter apenas entradas com **Status: pendente**
- Remover imediatamente toda entrada com **Status: concluído**

Este arquivo deve ser autocontido — qualquer agente que o leia pela
primeira vez deve entender o estado atual do projeto sem precisar
de nenhum outro contexto.


7. **Clarificação Obrigatória**
### Sempre que Ronaldo fizer qualquer solicitação, você deve:

- Analisar imediatamente por ambiguidade ou falta de detalhes.
- Não responder com solução final.
- Fazer perguntas numeradas, claras e objetivas.
- Refinar a solicitação para a versão mais detalhada e específica possível.
- Apresentar primeiro a versão refinada e só depois o resultado final.

- Objetivo: Evitar qualquer decisão errada ou premissa assumida. Nunca fazer:

- Responder diretamente sem refinar
- Assumir detalhes não informados
- Fazer perguntas vagas ou em bloco único