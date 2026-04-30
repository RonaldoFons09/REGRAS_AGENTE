---
trigger: always_on
---

### 4. Documentação (Versão Atualizada)

Priorizar simplicidade e manutenção mínima. Para projetos pequenos (< 10 mil linhas) desenvolvidos por Ronaldo sozinho, o foco deve ser concentrar o máximo de informações úteis e “à prova do tempo” no arquivo README.md (raiz do projeto). Evitar criação excessiva de arquivos de documentação que gerem overhead.


**Gestão da pasta docs/**

Só criar a pasta docs/ se realmente necessário (ex: para ADRs futuros ou documentos mais longos).
Não criar automaticamente a pasta docs/ em novos projetos.
Se a pasta docs/ já existir, não criar arquivos automaticamente dentro dela, exceto se Ronaldo solicitar explicitamente.

Arquivos recomendados e estrutura mínima
Na raiz do projeto (obrigatórios ou fortemente recomendados):

**README.md** ← Arquivo principal de documentação e contexto
Deve conter:
Visão geral do projeto (o que faz e qual problema resolve)
Decisões Arquiteturais Principais (à prova do tempo, com motivos e trade-offs)
Diagrama de arquitetura (usando Mermaid)
Regras fundamentais do projeto
Estrutura de pastas
Como rodar o projeto (passo a passo completo e copiável)
Como executar os testes
Link para o roadmap.md

**roadmap.md** ← Mantido como “segundo cérebro” de Ronaldo
Contém implementações futuras, ideias e prioridades específicas deste projeto.
Manter curto, priorizado e revisado periodicamente (Próximos 1–2 meses + Nice-to-have).

**Arquivos que não devem mais ser usados/criados por padrão:**

**docs/arquitetura.md** → Removido. Suas informações foram migradas para a seção “Decisões Arquiteturais Principais” dentro do README.md.
**docs/historia.md** → Removido completamente (conforme regra 6 atualizada). Não ler, não criar e não manter mais este arquivo.
Qualquer outro arquivo dentro de docs/ só deve ser criado se Ronaldo pedir explicitamente (ex: pasta docs/adr/ no futuro para decisões mais complexas).

Atualização de documentação

O agente deve sugerir atualizações leves no README.md quando:
Uma decisão arquitetural significativa for tomada (ex: escolha de tecnologia, padrão de arquitetura, trade-off importante).
A estrutura de pastas mudar de forma relevante.
Regras fundamentais do projeto forem definidas ou alteradas.

Ao sugerir atualização, mostrar apenas o bloco ## afetado (antes/depois) e aguardar confirmação de Ronaldo antes de propor o texto final.
Nunca reescrever o arquivo inteiro. Modificar apenas a seção necessária.

Gatilhos de atualização

Decisão arquitetural importante → Sugerir atualização na seção Decisões Arquiteturais Principais do README.md
Mudança relevante na estrutura de pastas → Sugerir atualização na seção Estrutura de Pastas do README.md
Final de uma conversa de desenvolvimento → Perguntar se deseja atualizar alguma seção do README.md (apenas se houver algo relevante para documentar)

Regra de ouro
Menos arquivos = menos manutenção.
O README.md deve ser rico o suficiente para que qualquer agente ou Ronaldo no futuro entenda rapidamente o propósito, a arquitetura e como rodar o projeto, sem precisar consultar múltiplos arquivos.
