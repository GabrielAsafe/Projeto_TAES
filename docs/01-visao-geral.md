# 01 — Visão geral

## Problema

**[EXPLÍCITO]** A gestão ineficiente das compras e dos alimentos em casa contribui para desperdício alimentar. O SmartPantry pretende facilitar o controlo dos produtos disponíveis e ajudar a escolher refeições que os aproveitem.

## Objetivo do produto

**[EXPLÍCITO]** Criar uma aplicação **mobile-first**, autónoma no dispositivo e sem necessidade de backend obrigatório que permita:

- Registar produtos/ingredientes e respetivas quantidades e prazos de validade.
- Destacar ingredientes que vão expirar nas próximas **48 horas**.
- Descobrir receitas de catálogos externos de acordo com o inventário e o perfil ativo.
- Gerar receitas originais com IA a partir de sobras selecionadas.
- Acompanhar a preparação passo a passo e gerir temporizadores.
- Atualizar opcionalmente o inventário ao concluir refeições.
- Gerir lista de compras e livro pessoal de receitas.
- Exportar e importar o estado da aplicação em **JSON**.

## Atores e conceitos principais

| Conceito | Significado no enunciado |
|---|---|
| Utilizador | Pessoa que interage com a aplicação no dispositivo. Não é exigido sistema de contas. |
| Perfil doméstico | Conjunto selecionável de preferências alimentares, alergénios, exclusões e número habitual de porções. |
| Perfil ativo | Perfil usado para condicionar pesquisa e geração de receitas. |
| Estado partilhado | Inventário, lista de compras e livro de receitas comuns aos perfis. |
| Receita de catálogo | Receita encontrada por API pública de receitas. |
| Receita IA | Receita original estruturada produzida pelo GenAI Sous-Chef. |

**Nota:** “vários perfis” **não** implica “várias despensas independentes”. O texto é explícito em indicar inventário, compras e livro de receitas partilhados.

## Âmbito funcional

O âmbito inclui dez blocos: perfis, inventário, leitura/consulta de produtos, descoberta de receitas, livro de receitas, geração por IA, Cook Mode, conclusão da refeição, lista de compras e portabilidade dos dados.

## Restrições e dependências

- **[EXPLÍCITO]** Foco em dispositivos móveis, com uso da câmara quando disponível.
- **[EXPLÍCITO]** Funciona sem backend **obrigatório**.
- **[EXPLÍCITO]** Receitas guardadas acessíveis offline.
- **[EXPLÍCITO]** Consultas a bases públicas de produtos, APIs públicas de receitas e API de GenAI.
- **[PROPOSTA]** Distinguir capacidades locais das dependentes de rede. O enunciado não exige disponibilidade offline universal.

## Fora do âmbito confirmado (não assumir como requisito)

Autenticação, partilha entre dispositivos, sincronização cloud, pagamentos, notificações push, histórico de refeições, calendário alimentar, reconhecimento automático de ingredientes por fotografia e suporte a múltiplos utilizadores autenticados **não são descritos** no enunciado.

## Referências internas

- Funcionalidades: [`02-funcionalidades.md`](02-funcionalidades.md)
- Domínios: [`03-dominios.md`](03-dominios.md)
- Pontos em aberto: [`09-duvidas-e-decisoes.md`](09-duvidas-e-decisoes.md)
