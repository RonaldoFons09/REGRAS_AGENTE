# REGRAS_AGENTE

## Visão geral
Este repositório armazena as regras globais para o agente Antigravity (Gemini), garantindo que todas as interações e desenvolvimentos sigam padrões específicos de codificação, documentação e comunicação.

## Decisões Arquiteturais Principais
| Decisão | Motivo | Data |
|---------|--------|------|
| Centralização | Documentação concentrada no README.md e roadmap.md na raiz para reduzir manutenção. | 2026-04-30 |
| Regras Modulares | Regras do agente movidas para `.agent/rules` para facilitar o carregamento dinâmico. | 2026-04-30 |

## Regras do Projeto
As diretrizes fundamentais estão localizadas em [.agent/rules/](.agent/rules/).

## Escopos de Commit
| Escopo | Descrição |
|--------|-----------|
| global | Mudanças que afetam as regras fundamentais do repositório. |
| .agent | Alterações em workflows ou regras do agente. |

## Como rodar
Não há necessidade de execução local. O conteúdo deste repositório serve como base de conhecimento para o agente de IA configurar o ambiente de trabalho.

## Roadmap
O planejamento futuro e status das tarefas podem ser consultados em [roadmap.md](roadmap.md).
