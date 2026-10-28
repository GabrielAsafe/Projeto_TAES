# 14 — Entrega intermédia: requisitos e estratégia de recolha de provas

> **Não é o relatório final.** Este documento organiza o que a equipa deverá demonstrar, sem inventar atividades, screenshots ou aceitações. Todos os materiais anexados devem ser **extraídos de ferramentas reais**.

## Regras de submissão

- **Um único PDF**.
- **Corpo principal: máximo de quatro páginas**.
- **Apêndices opcionais, sem limite de páginas**, com screenshots de boa resolução e registos completos.
- Corpo principal = síntese e evidências representativas; detalhes extensos nos apêndices, citados no texto com identificadores `A1`, `A2`, etc.

## Estrutura recomendada do corpo principal (até 4 páginas)

| Página | Informação prioritária | Evidências curtas sugeridas |
|---|---|---|
| **1 — Equipa e planeamento** | Grupo, 4 nomes/números/emails institucionais; stack e APIs escolhidas; links Jira e GitHub/Bitbucket acessíveis ao PO; sumário de backlog refinado, US com BV/SP (se definidos) | Screenshot Jira/backlog e ligação para tabela integral nos apêndices |
| **2 — Progresso por sprint** | Sprint Goal, Scrum Master do sprint (rotação), USs selecionadas com BV/SP, Product Increment efetivamente demonstrado, PO feedback | Capturas da aplicação e 1 excerto representativo do Katalon com Pass/Fail; detalhes por sprint em apêndices |
| **3 — Controlo Scrum e testes** | Planeamento/review/retrospectiva (ação e responsável), board e fecho do sprint, dailies e blockers, sequência test-first | Print de board fechado; link/identificador de `.feature`, commit e relatório de execução |
| **4 — Engenharia XP, riscos, próximos passos** | Pair programming, ownership partilhado, branching/PR reviews/Smart Commits, spikes, principais riscos e ações corretivas | PR revisto, commits ligados ao Jira, resumo de spike e referência aos apêndices |

Se houver vários sprints concluídos, usar **tabela-resumo por sprint** no corpo principal e colocar evidência integral de **cada um** nos apêndices; não dedicar automaticamente uma página a cada sprint.

## Formato de cada User Story no backlog

```text
US-XXX — <Title>
As a <role>, I want <feature>, so that <value>.
Acceptance Criteria (apenas títulos de cenários BDD):
- Scenario: ...
- Scenario: ...
BV: <valor atribuído pelo PO ou TBD>
SP: <estimativa da equipa ou TBD>
Jira: <issue URL>
Estado: <status atual>
```

**Não atribuir BV nem distinguir core/nice-to-have sem informação do PO.** Para Acceptance Criteria no relatório, a regra especifica **apenas títulos dos cenários**, não passos Given/When/Then no corpo do backlog. Os passos completos devem ficar nos `.feature` e, se necessário, nos apêndices.

## Registo por sprint (preencher com provas reais)

| Campo | O que guardar durante cada sprint | Onde obter |
|---|---|---|
| Scrum Master | Membro responsável, datas | Jira / ata de planeamento |
| Goal e Backlog | Objetivo, USs, tarefas, BV e SP | Sprint Jira (início) |
| Review e Product Increment | Funcionalidades integradas, captura no telemóvel, feedback PO | App, Review, Jira |
| Katalon | Nome da suite, execução, data, cenários Pass/Fail | Relatório Katalon |
| Board | Transição e encerramento oficial do sprint | Jira antes/depois e sprint report |
| Daily Scrum | Progressos e impedimentos por dia | Mensagens de equipa/notas/board |
| Retrospective | O que correu bem, problemas, ação/owner/data | Notas de reunião |
| Spikes | Pergunta, experiências, evidências, resultado e decisão | PR/Issue/notas/test logs |

## XP / prova rastreável

- **Test-first:** commit com `.feature`/Groovy criado antes ou em conjunto com a implementação, seguido por PR; incluir hashes e datas.
- **Pair programming:** data, participantes, assunto/tarefa, duração opcional, resultado, evidência de sessão/documento.
- **Collective ownership:** mostrar contribuições de vários membros em UI, lógica, Gherkin e Groovy; não exigir todos os membros em todos os ficheiros.
- **PR + review:** branch e issue key Jira, conversa, aprovação e merge.
- **Smart Commits:** registar comentários de commit que referenciam issues Jira, se integração configurada.
- **Test reports:** referenciar execução associada ao incremento demonstrado, com Pass/Fail visível; não ocultar falhas — explicar diagnóstico e decisão.

## Índice de apêndices sugerido

- `A1` — Backlog completo e refinamento por US (narrativa, título de cenários, BV/SP).
- `A2` — Sprint 1: planning, board, review, retrospective, dailies, Katalon.
- `A3` — Sprint 2 (e subsequentes): estrutura repetida por sprint concluído.
- `A4` — Gherkin completo e amostras de Groovy.
- `A5` — Git log, branches, PRs e reviews.
- `A6` — Pair programming, rotação SM e ownership partilhado.
- `A7` — Spikes técnicos, diagramas UML, ER e UI mockups.

## Rastreabilidade mínima

`US-XXX (Jira) -> Scenario title -> ficheiro .feature -> step definition Groovy -> relatório Katalon -> Pull Request -> Sprint Review -> PO acceptance`

Criar um pequeno índice de evidências com IDs estáveis (`EV-001`) e URLs/capturas; colocar as evidências no momento em que acontecem em vez de reconstruir tudo na véspera da entrega.
