# 15 — Matriz inicial de rastreabilidade

> Esta tabela facilita a passagem de requisitos para histórias Jira, cenários `.feature`, módulos e dados. Os identificadores reais de Jira, BV, SP e core/nice-to-have ainda não estão definidos.

| Área / requisitos | Entidades / DTO principais | Diagrama(s) | API/integração | Cenários de aceitação a especificar |
|---|---|---|---|---|
| Onboarding/perfis (`RF-PER-*`) | `HouseholdProfile`, `ProfileRestriction`, `AppSettings` | Classes, ER, Componentes | Nenhuma externa | Criar perfil; selecionar; editar; apagar último/ativo |
| Despensa (`RF-PAN-*`) | `PantryItem`, `PantryCategory`, `Ingredient?` | Classes, ER | Persistência local | Criar categoria; alerta ≤48h; eliminar lote esgotado |
| Barcode (`RF-PROD-*`) | `ProductLookupResult` (DTO), `PantryItem` | Sequência scan, Componentes | Leitor barcode + Open Food Facts | Câmara negada; código desconhecido; prefill editável |
| Discovery (`RF-DESC-*`) | `RecipeMatch` (DTO), `Recipe`, `RecipeIngredient` | Classes, Componentes, Sequência cozinhar | Catálogo de receitas | Match; faltas; prioritizar validade; restrições |
| Livro (`RF-LIB-*`) | `SavedRecipe`, `RecipeFolder`, `RecipeCollection` | Classes, ER | Base local | Guardar; organizar; ver offline; contar preparações |
| GenAI (`RF-AI-*`) | `GenerationRequest` (DTO), `Recipe`, `RecipeStep` | Classes, Componentes | Gemini/OpenAI, por selecionar | Output schema; exclusões; falha de serviço |
| Cook Mode (`RF-COOK-*`) | `RecipeStep`, `StepIngredient`, `CookingSession` (temporário) | Estados Cook, Sequência cozinhar | Temporizadores do dispositivo | Passo ativo; timer start/pause/reset/fim |
| Meal completion (`RF-MEAL-*`) | `CookingRecord`, `ConsumptionLine`, `PantryItem` | Classes, ER, Sequência cozinhar | Transação local | Desconto; skip; quantidades editadas; contador |
| Compras (`RF-SHOP-*`) | `ShoppingItem`, `PantryItem` | Classes, ER | Base local | Adicionar; marcar; transferir lote; impedir duplicação |
| Portabilidade (`RF-DATA-*`) | `AppSnapshot` (JSON), entidades persistidas | ER, Componentes | Partilha/ficheiros no dispositivo | Export/import; overwrite; merge; JSON inválido |

## Ligação à entrega intermédia

Para cada história, recolher `US -> título do Scenario -> caminho .feature -> passos Groovy -> relatório Katalon -> PR/commit -> Jira sprint -> aceitação do PO`. A matriz pode tornar-se uma tabela viva quando o backlog receber os identificadores definitivos, BV e SP.
