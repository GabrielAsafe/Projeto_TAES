# SmartPantry — Documentação do projeto

> Estado: **análise e modelação inicial** (outubro de 2026). Nenhuma stack, API ou modelo físico foi formalmente aprovado.  
> Idioma: PT-PT; o enunciado inicial está preservado em inglês.

## Ordem de trabalho acordada

1. Modelar o domínio e os fluxos (classes, ER, componentes, sequência, estados).
2. Validar as entidades, os contratos de dados e a viabilidade de APIs reais com *spikes*.
3. Comparar as stacks sem tomar já uma decisão.
4. Preparar a entrega intermédia com **evidências reais**, recolhidas sprint a sprint.

## Documentação da fase inicial

| Ficheiro | Propósito |
|---|---|
| [00-enunciado-original.md](00-enunciado-original.md) | Introdução e funcionalidades originais do enunciado |
| [01-visao-geral.md](01-visao-geral.md) | Visão do projeto |
| [02-funcionalidades.md](02-funcionalidades.md) | Requisitos funcionais `RF-*` |
| [03-dominios.md](03-dominios.md) | Limites lógicos e responsabilidades |
| [04-modelo-de-dados.md](04-modelo-de-dados.md) | Conceitos e atributos iniciais |
| [05-apis.md](05-apis.md) | Contratos lógicos entre componentes |
| [06-integracoes.md](06-integracoes.md) | Integrações e fallbacks |
| [07-regras-de-negocio.md](07-regras-de-negocio.md) | Regras, validações e políticas por fechar |
| [08-requisitos-nao-funcionais.md](08-requisitos-nao-funcionais.md) | Restrições técnicas |
| [09-duvidas-e-decisoes.md](09-duvidas-e-decisoes.md) | Perguntas `Q-*` e decisões futuras |

## Novos documentos de aprofundamento

| Ficheiro | Propósito |
|---|---|
| [10-modelo-de-dados-detalhado.md](10-modelo-de-dados-detalhado.md) | Tabelas/entidades candidatas, campos, integridade e portabilidade |
| [11-apis-candidatas.md](11-apis-candidatas.md) | Provedores reais, endpoints oficiais, limites, licenças e spikes |
| [12-stack-opcoes.md](12-stack-opcoes.md) | Comparação de PWA, Flutter, React Native e nativo, **sem decisão** |
| [13-processo-avaliacao.md](13-processo-avaliacao.md) | Scrum/XP/BDD/Katalon, DoD, BV e avaliação |
| [14-entrega-intermedia.md](14-entrega-intermedia.md) | Formato do PDF, estrutura de 4 páginas, apêndices e evidências |
| [15-matriz-rastreabilidade.md](15-matriz-rastreabilidade.md) | Requisitos -> dados -> diagramas -> integrações -> testes |

## Diagramas editáveis em Mermaid

| Diagrama | Questão que ajuda a responder |
|---|---|
| [01-diagrama-classes.md](diagramas/01-diagrama-classes.md) | Que objetos existem e como se relacionam? |
| [02-modelo-entidade-relacao.md](diagramas/02-modelo-entidade-relacao.md) | Quais dados podem ser persistidos localmente? |
| [03-arquitetura-componentes.md](diagramas/03-arquitetura-componentes.md) | Quais são os módulos e as dependências externas? |
| [04-sequencia-scan-produto.md](diagramas/04-sequencia-scan-produto.md) | Como funciona a leitura de barcode e os fallbacks? |
| [05-sequencia-cozinhar.md](diagramas/05-sequencia-cozinhar.md) | Como se chega ao desconto de stock e contador? |
| [06-estados-cozinha.md](diagramas/06-estados-cozinha.md) | Que estados existem numa sessão Cook Mode? |

Cada `.md` inclui Mermaid renderizável em GitHub/visualizadores compatíveis; a pasta também contém o `.mmd` correspondente, para edição ou exportação por Mermaid CLI.

## Processos e evidências

| Ficheiro | Propósito |
|---|---|
| [planeamento/01-evidencias-checklist.md](planeamento/01-evidencias-checklist.md) | Checklist por sprint e índice de anexos |
| [planeamento/02-exemplo-bdd.md](planeamento/02-exemplo-bdd.md) | Exemplos didáticos de cenários Gherkin |

## Regras de interpretação

- **[EXPLÍCITO]:** conteúdo exigido no enunciado.
- **[PROPOSTA]:** decisão ou organização candidata, ainda não aceite.
- **[POR DEFINIR]:** dúvida não resolvida com PO/docente.
- `RF-*`: requisitos funcionais rastreáveis.
- `Q-*`: perguntas/ambiguidades rastreáveis.
- Os nove domínios são **módulos de negócio**, não nove microserviços.
- Perfis partilham despensa, lista de compras e livro de receitas.
- APIs encontradas na pesquisa **não são seleções finais**.
- A divisão **core / nice-to-have e valores BV** depende do Product Owner.
- Diagramas de classes e ER representam hipóteses, não código implementado.

## Critérios de revisão sugeridos

1. Validar o modelo de ingrediente, lotes e unidades (`Q-01`, `Q-02`, `Q-11`).
2. Validar a receita canónica para catálogo/IA/Cook Mode (`Q-03`, `Q-05`).
3. Validar licenças de armazenamento offline das receitas e segurança de chaves de IA (`Q-07`).
4. Testar automatização real com Katalon na stack candidata antes de escolher tecnologia.
5. Confirmar os limites da entrega intermédia e começar a recolher evidências em cada sprint.
