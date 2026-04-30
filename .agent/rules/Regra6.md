---
trigger: always_on
---

### 6. Gestão de contexto e memória
Ao iniciar uma nova conversa, leia nesta ordem (apenas os arquivos que existirem):

**README.md (raiz do projeto)** 
 Visão geral completa do projeto, propósito, decisões arquiteturais principais (à prova do tempo), estrutura de pastas, tecnologias, regras fundamentais, diagrama de arquitetura (Mermaid) e instruções de como rodar o projeto.
Este é o arquivo principal de contexto. O README deve ser rico em informações estáveis que raramente mudam.
roadmap.md (raiz do projeto) → Fase atual, implementações futuras planejadas e ideias pendentes para este projeto específico.
Ele funciona como o “segundo cérebro” de Ronaldo para lembrar o que quer fazer.

Assuma o contexto imediatamente sem solicitar confirmação adicional.
Se algum arquivo não existir, use o que estiver disponível e aguarde a primeira instrução de Ronaldo.
Remoção de arquivos obsoletos

Não leia nem mantenha mais o arquivo docs/historia.md (ou qualquer equivalente de histórico manual de sessões).
Não crie blocos automáticos de “Contexto da Sessão”, snapshots por mensagem ou registros detalhados de “o que foi feito / decisões / o que não funcionou”.
O histórico natural do Git (commits bem escritos) + testes automatizados + o README.md atualizado já fornecem contexto suficiente.

Decisões arquiteturais importantes
Se durante a conversa surgir uma decisão arquitetural significativa (ex: escolha de padrão, tecnologia, trade-off importante ou mudança na estrutura), sugira atualizar a seção correspondente no README.md (na parte “Decisões Arquiteturais Principais”).
Mantenha essa seção curta, clara e focada no “por quê”.
Tipo de sessão
Detecte automaticamente pelo conteúdo da conversa (sem perguntar):

Desenvolvimento: envolve criação, modificação ou revisão de código, testes ou estrutura de arquivos.
Planejamento: envolve revisão de roadmap, definição de arquitetura, escolha de tecnologia ou decisões de produto.

**Atualização do README.md**

Ao final de uma conversa que envolve mudanças relevantes na arquitetura, estrutura ou regras fundamentais, sugira uma atualização leve na seção apropriada do README.md.
Mantenha o README escaneável, com headings claros, Mermaid para diagramas e seções bem separadas (Sobre o Projeto, Decisões Arquiteturais, Estrutura de Pastas, Como Rodar, etc.).
Evite adicionar itens que mudam com frequência (use o roadmap.md para isso).

**Manutenção geral**

Priorize sempre a simplicidade: menos arquivos e menos manutenção manual.
O objetivo é que qualquer agente (ou Ronaldo no futuro) consiga entender rapidamente o projeto apenas lendo o README.md + roadmap.md.
Se o projeto crescer significativamente no futuro, podemos reavaliar a adição de uma pasta docs/adr/ para decisões individuais, mas por enquanto mantenha tudo concentrado no README.md.