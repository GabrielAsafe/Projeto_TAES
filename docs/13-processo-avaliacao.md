# 13 — Regras do projeto, processo e avaliação

## Requisitos explícitos do enunciado

- Aplicação **mobile-first**; a equipa escolhe tecnologia (web mobile-first, nativo Android/iOS, cross-platform, etc.).
- Trabalho em **equipa de quatro alunos**.
- Scrum combinado com práticas XP; sprints e demonstração **funcional e testada** em cada Sprint Review.
- Jira para backlog, sprints e acompanhamento; GitHub ou Bitbucket para código com branches, PRs/reviews, Smart Commits quando aplicável e disciplina de integração.
- Mentalidade **test-first**. Especificações de aceitação em **Gherkin (.feature)** e testes automáticos em **Katalon Studio**, com definições dos passos em **Groovy**.
- Spikes técnicos iniciais são fortemente encorajados: leitura de barcode e fallbacks, validação de APIs de produtos/receitas, GenAI e estratégia de integração.
- Requisitos do backlog dividem-se em **core** e **nice-to-have**, mas a classificação e Business Value de cada US **ainda serão divulgadas/discutidas com o Product Owner**.
- Implementar o conjunto core conforme Definition of Done é suficiente para os **2000 BV** do Product Grade. Extras não aumentam o teto de 2000 BV.

## Avaliação (transcrição estruturada das regras fornecidas)

`Final Grade = (0.70 × Process Grade + 0.30 × Product Grade) × Public Presentation`

> A variável `Public Presentation` é apresentada no enunciado como 0–100%; a forma exata de normalização na fórmula deverá ser confirmada com o docente. Evitar calcular notas sem essa definição.

**Process Grade (70% da fórmula antes do multiplicador da apresentação):**

- **35% — Project Planning and Execution:** objetivos dos sprints; planeamento; backlog grooming; critérios de aceitação com PO; retrospectivas com ações; qualidade de User Stories/Cenários; estimativas Story Points; acompanhamento do Scrum board.
- **35% — Agile Practices and Project Control:** evidências de dailies, pair programming, collective ownership, rotação do Scrum Master, testes escritos antes ou durante implementação, definições Groovy robustas, relatórios de testes, Git workflow e Smart Commits.
- O Process Grade é escalado proporcionalmente pela razão de BV entregue.

**Product Grade (30%):** funcionalidades implementadas e testes automatizados correspondentes. Uma User Story só conta se satisfizer integralmente a DoD: código completo, layout mobile-first funcional, integrações externas quando aplicáveis, **todos** os cenários BDD aprovados, validação/aceitação formal pelo PO em Sprint Review.

**Public Presentation (0–100%):** defesa individual, demonstração de software funcional, suites de testes e práticas ágeis.

## Definition of Done operacional sugerida

Uma história só pode marcar-se `Done` quando:

1. Tem cenários de aceitação Gherkin identificados e revistos.
2. Implementação, layout mobile-first e tratamento de casos limite estão concluídos.
3. Integrações/contratos externos envolvidos estão demonstráveis (com tratamento de falhas).
4. Os testes BDD correspondentes passam no Katalon e o relatório foi preservado.
5. Pull Request foi revisto e integrado; commits/reviews/questões estão rastreáveis no Jira.
6. O PO validou e aceitou a história na Sprint Review.

**Atenção:** a lista acima formaliza práticas concretas a partir do enunciado, não substitui a DoD oficial que a equipa/PO aprovar.
