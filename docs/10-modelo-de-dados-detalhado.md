# 10 — Candidatos a entidades persistidas e políticas de dados

> **Proposta técnica a validar.** Complementa `04-modelo-de-dados.md` e `diagramas/02-modelo-entidade-relacao.md`. O ER descreve um esquema relacional **possível**; pode ser mapeado para uma base local relacional ou para objetos/documentos.

## Núcleo: dados persistidos

| Entidade | Campos principais propostos | Finalidade / observações |
|---|---|---|
| `AppSettings` | `id`, `activeProfileId`, `schemaVersion` | Preferências globais e perfil ativo; um registo lógico. |
| `HouseholdProfile` | `id`, `name`, `defaultServings` | Perfis alimentares **sem duplicar** inventário/compras. |
| `ProfileRestriction` | `id`, `profileId`, `kind`, `value` | Dieta, alergénio, ingrediente excluído (`kind` enum). |
| `PantryCategory` | `id`, `name`, `isCustom` | Categorias comuns e criadas pelo utilizador. |
| `PantryItem` | `id`, `displayName`, `ingredientId?`, `categoryId`, `quantity`, `unit`, `expiryDate`, `barcode?` | Entrada/lote de stock, com validade independente. |
| `ShoppingItem` | `id`, `name`, `ingredientId?`, `desiredQuantity?`, `unit?`, `checked`, `sourceRecipeRef?` | Itens da lista e origem opcional. |
| `Recipe` | `id`, `source`, `externalId?`, `title`, `servings`, `prepMinutes?`, `cookMinutes?`, `sourceUrl?` | Modelo canónico. **Não persistir automaticamente todos os resultados remotos**; só conteúdo permitido pela licença e necessário ao livro de receitas. |
| `RecipeIngredient` | `id`, `recipeId`, `ingredientId?`, `displayName`, `quantity`, `unit` | Medidas e ingredientes da receita. |
| `RecipeStep` | `id`, `recipeId`, `position`, `instruction`, `timerSeconds?` | Passos ordenados para Cook Mode. |
| `StepIngredient` | `recipeStepId`, `recipeIngredientId`, `quantity`, `unit` | Associação entre passo e ingrediente, com medida específica do passo. |
| `SavedRecipe` | `recipeId`, `savedAt`, `folderId?` | Marcador no livro. O conteúdo associado tem de ser consultável offline. |
| `RecipeFolder` | `id`, `name` | Organização em pastas, cardinalidade pendente. |
| `RecipeCollection` | `id`, `name` | Organização em coleções. |
| `CollectionMembership` | `collectionId`, `recipeId` | N:N entre coleções e receitas guardadas. |
| `CookingRecord` | `id`, `recipeId?`, `sourceRef?`, `titleSnapshot`, `completedAt`, `stockDecremented` | Histórico mínimo para contar preparações, incluindo receitas não guardadas. |
| `ConsumptionLine` | `id`, `cookingId`, `pantryItemId?`, `quantity`, `unit` | Consumo confirmado, referência a lote quando ainda existe. |

## Entidades/estruturas opcionais que podem surgir mais tarde

| Entidade | Quando faz sentido |
|---|---|
| `Ingredient` | Se for útil normalizar nomes usados pelas receitas, despensa e compras (`tomato`, `tomate`). |
| `IngredientAlias` | Se houver necessidade de sinónimos/idiomas por ingrediente. |
| `StockMovement` | Se for necessário um ledger/auditoria para desfazer consumos e importações. |
| `ImportHistory` | Se a equipa necessitar de auditar restauros e conflitos JSON. |

**Não considerar como tabelas por defeito:** `ProductLookupResult`, `RecipeMatch`, `GenerationRequest`, `CookingSession`, `TimerState` e `AppSnapshot`. São DTOs, estados transitórios ou ficheiros de exportação. `TimerState` só requer persistência se a equipa decidir suportar reinício do temporizador após encerramento.

## Semântica e integridade

### Inventário

- Cada `PantryItem` pode representar um lote separado (mesmo produto, validades diferentes). **Hipótese recomendada**, ainda por validar com o PO.
- Unidades devem distinguir massa, volume e unidades; conversão só se existir regra confiável. Não somar quantidades de dimensões incompatíveis.
- Alerta de validade: aplicar regra funcional de **48 horas**; se existir apenas uma data de validade (sem hora), documentar uma convenção explícita.
- Quantidade de stock não pode ficar negativa. Quando é zero, o item pode ser removido do inventário ativo.

### Receitas

- `Recipe.source` pode ser `CATALOG` ou `AI`. Guardar `externalId` e atribuição de origem quando se aplicarem.
- `RecipeIngredient` é o nível de quantidade total; `StepIngredient` (tabela de junção no ER) permite quantidades/ingredientes do passo ativo.
- A decisão de persistir receitas de catálogo depende dos termos do fornecedor. Uma API pode permitir consultar uma receita e proibir que se guarde offline a sua cópia.
- Contador de preparação: derivar `COUNT(CookingRecord)` por identificador de receita ou manter um contador sincronizado. Definir tratamento de receitas sem ID estável.

### Importação e exportação

- `AppSnapshot` sugerido: `{schemaVersion, exportedAt, appSettings, profiles, pantryCategories, pantryItems, shoppingItems, savedRecipes, recipeFolders, recipeCollections, cookingRecords?}`.
- `overwrite`: validar o JSON e as referências primeiro; substituir os dados **numa transação**; nunca perder o estado anterior por falha parcial.
- `merge`: definir identidade e resolução de conflitos por ID; especialmente `activeProfileId`, receitas duplicadas, categorias com nomes iguais e linhas de consumo.
- `schemaVersion` e migrações são importantes para que snapshots de diferentes versões não corrompam dados.

## Regra geral de arquitetura

A entidade `HouseholdProfile` **não tem FK** em `PantryItem`, `ShoppingItem` ou `SavedRecipe`. Os perfis são preferências de consumo e não contas/households separados. O `AppSettings.activeProfileId` aponta para um perfil existente.
