# ER — Modelo lógico candidato para persistência local

> **Proposta, não esquema final.** A tecnologia (SQLite, IndexedDB, outra) não foi escolhida. `PK` = chave primária; `FK` = chave estrangeira. A base de dados persiste **dados partilhados numa única instalação**, não bases separadas por perfil.

```mermaid
erDiagram
    APP_SETTINGS {
      string id PK
      string active_profile_id FK
      int schema_version
    }
    HOUSEHOLD_PROFILE {
      string id PK
      string name
      int default_servings
    }
    PROFILE_RESTRICTION {
      string id PK
      string profile_id FK
      string kind
      string value
    }
    PANTRY_CATEGORY {
      string id PK
      string name
      boolean is_custom
    }
    INGREDIENT {
      string id PK
      string canonical_name
    }
    INGREDIENT_ALIAS {
      string id PK
      string ingredient_id FK
      string alias
    }
    PANTRY_ITEM {
      string id PK
      string category_id FK
      string ingredient_id FK
      string display_name
      decimal quantity
      string unit
      date expiry_date
      string barcode
    }
    SHOPPING_ITEM {
      string id PK
      string ingredient_id FK
      string name
      decimal desired_quantity
      string unit
      boolean checked
    }
    RECIPE {
      string id PK
      string source
      string external_id
      string title
      int servings
      int prep_minutes
      int cook_minutes
    }
    RECIPE_INGREDIENT {
      string id PK
      string recipe_id FK
      string ingredient_id FK
      string display_name
      decimal quantity
      string unit
    }
    RECIPE_STEP {
      string id PK
      string recipe_id FK
      int position
      string instruction
      int timer_seconds
    }
    STEP_INGREDIENT {
      string recipe_step_id FK
      string recipe_ingredient_id FK
      decimal quantity
      string unit
    }
    SAVED_RECIPE {
      string recipe_id PK,FK
      string folder_id FK
      datetime saved_at
    }
    RECIPE_FOLDER {
      string id PK
      string name
    }
    RECIPE_COLLECTION {
      string id PK
      string name
    }
    COLLECTION_MEMBERSHIP {
      string collection_id PK,FK
      string recipe_id PK,FK
    }
    COOKING_RECORD {
      string id PK
      string recipe_id FK
      string source_ref
      string title_snapshot
      datetime completed_at
      boolean stock_decremented
    }
    CONSUMPTION_LINE {
      string id PK
      string cooking_id FK
      string pantry_item_id FK
      decimal quantity
      string unit
    }
    HOUSEHOLD_PROFILE ||--o{ PROFILE_RESTRICTION : tem
    HOUSEHOLD_PROFILE ||--o| APP_SETTINGS : pode_ser_ativo
    PANTRY_CATEGORY ||--o{ PANTRY_ITEM : categoriza
    INGREDIENT ||--o{ INGREDIENT_ALIAS : nomes
    INGREDIENT o|--o{ PANTRY_ITEM : corresponde
    INGREDIENT o|--o{ RECIPE_INGREDIENT : corresponde
    INGREDIENT o|--o{ SHOPPING_ITEM : corresponde
    RECIPE ||--|{ RECIPE_INGREDIENT : contem
    RECIPE ||--|{ RECIPE_STEP : contem
    RECIPE_STEP ||--o{ STEP_INGREDIENT : utiliza
    RECIPE_INGREDIENT ||--o{ STEP_INGREDIENT : indicado
    RECIPE ||--o| SAVED_RECIPE : guardada
    RECIPE_FOLDER o|--o{ SAVED_RECIPE : organiza
    RECIPE_COLLECTION ||--o{ COLLECTION_MEMBERSHIP : inclui
    SAVED_RECIPE ||--o{ COLLECTION_MEMBERSHIP : associada
    RECIPE o|--o{ COOKING_RECORD : regista
    COOKING_RECORD ||--o{ CONSUMPTION_LINE : consumo
    PANTRY_ITEM o|--o{ CONSUMPTION_LINE : lote_consumido
```

## Núcleo recomendado para um primeiro sprint

1. `HOUSEHOLD_PROFILE`, `PROFILE_RESTRICTION`, `APP_SETTINGS` (onboarding e seleção de perfil).
2. `PANTRY_CATEGORY`, `PANTRY_ITEM` (despensa, expirados, categorias personalizadas).
3. `SHOPPING_ITEM` (lista e transferência).
4. `RECIPE`, `RECIPE_INGREDIENT`, `RECIPE_STEP`, `SAVED_RECIPE` (apenas receitas cuja persistência é permitida).

Os restantes conjuntos de tabelas suportam fluxos mais avançados, e podem evoluir conforme a validação com o Product Owner. `INGREDIENT` e `INGREDIENT_ALIAS` são recomendados para normalização, mas inicialmente podem ser substituídos por um identificador/serviço local simples. `STEP_INGREDIENT` permite mostrar apenas as medidas do passo ativo.

## Restrições de integridade sugeridas

- Quantidades `>= 0` na despensa e `> 0` nas linhas de consumo/transação (a política de zero deve ser uniforme).
- `default_servings > 0`, `servings > 0`, durações de temporizador não negativas.
- `UNIQUE (recipe_id, position)` em `RECIPE_STEP`.
- `UNIQUE (collection_id, recipe_id)` em `COLLECTION_MEMBERSHIP`.
- Preservar relações na importação; nunca inserir associações com `FK` inexistente.
- Uso de transação local atómica para conclusão com desconto de stock.
- Importação/merge deve possuir versão de esquema e estratégia de conflitos.
- Não presumir que alergénios declarados por terceiros são completos; resultados incompletos devem ser tratados como **não verificados**.
