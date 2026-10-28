# 05 — APIs e contratos lógicos

> **[EXPLÍCITO]** A aplicação usa **bases públicas de produtos**, **APIs públicas de receitas** e **uma API GenAI**.  
> **[POR DEFINIR]** Fornecedores, URLs, endpoints HTTP, métodos, autenticação, quotas, formatos e tratamento detalhado de erros.  
> Os nomes de operações abaixo são **interfaces conceptuais propostas**, não endpoints exigidos pelo enunciado.

## 1. Consulta de produto por código de barras

**Origem:** base de dados pública de produtos.  
**Operação conceptual [PROPOSTA]:** `lookupProduct(barcode)`.

| Entrada | Saída necessária | Usado por |
|---|---|---|
| Código de barras lido na câmara | Nome do produto, categoria, tamanho padrão | Formulário de introdução na despensa (`RF-PROD-02/03`) |

- O resultado **pré-preenche** campos, que o utilizador pode corrigir.
- Sem câmara, câmara bloqueada/não suportada ou produto inexistente: **upload de imagem ou inserção manual** (`RF-PROD-04`).
- O enunciado **não** estabelece que uma imagem carregada deva ser analisada por IA ou OCR (`Q-06`).

## 2. Pesquisa de receitas de catálogo

**Origem:** API pública de receitas.  
**Operação conceptual [PROPOSTA]:** `searchCatalogRecipes(criteria)`.

| Entrada relevante para a aplicação | Saída relevante para a aplicação | Usado por |
|---|---|---|
| Critérios de pesquisa + perfil ativo + informação de despensa necessária à correspondência | Receitas, listas de ingredientes e informação suficiente para apresentar/preparar pratos | Descoberta (`RF-DESC-*`) e Cook Mode (`RF-COOK-*`) |

- A aplicação tem de obter dados suficientes para calcular correspondência, distinguir ingredientes em falta, filtrar restrições e aproveitar artigos próximos da validade.
- **[POR DEFINIR]** Se os filtros podem ser feitos no fornecedor ou se têm de ser aplicados localmente.
- **[POR DEFINIR]** Se o fornecedor devolve instruções, porções e medidas necessárias ao Cook Mode; escolher fonte ou normalização que satisfaça o fluxo.
- **[POR DEFINIR]** Fórmula de correspondência de ingredientes (`Q-01`, `Q-05`).

## 3. Geração de receita por IA

**Origem:** API GenAI.  
**Operação conceptual [PROPOSTA]:** `generateRecipe(selectedIngredients, dietaryConstraints, servings)`.

| Entrada explícita | Saída exigida |
|---|---|
| Sobras/ingredientes selecionados; restrições do perfil ativo; número de porções | Receita original estruturada com tempos de preparação, porções, ingredientes e respetivas medidas, e instruções por passos |

- A aplicação deve interpretar a resposta num modelo de receita utilizável pelo Cook Mode e passível de ser guardado no livro.
- **[PROPOSTA]** Validar estrutura e campos obrigatórios após receber a resposta; a validação técnica concreta não é detalhada no enunciado.
- **[POR DEFINIR]** Garantias de respeito por alergénios, estratégia de validação, erros da API e tentativa de nova geração (`Q-14`).

## 4. Interfaces entre módulos da aplicação (não necessariamente APIs HTTP)

| Contrato conceptual [PROPOSTA] | Responsabilidade | Requisitos que suporta |
|---|---|---|
| `getActiveProfile()` | Obter porções e restrições correntes | `RF-PER-09` |
| `getPantryStock()` | Disponibilizar produtos e validades | `RF-DESC-01/04` |
| `calculateRecipeMatch(recipe, stock)` | Calcular percentagem, disponíveis/em falta | `RF-DESC-02/03` |
| `addMissingIngredients(recipe)` | Acrescentar ingredientes à lista de compras | `RF-DESC-06` |
| `transferCheckedShoppingItems(details)` | Transferir compras selecionadas para a despensa | `RF-SHOP-05` |
| `completeMeal(consumption, decrementStock)` | Confirmar quantidades, descontar se autorizado e contar preparação | `RF-MEAL-*` |
| `exportState()` / `importState(file, mode)` | Portabilidade JSON com overwrite/merge | `RF-DATA-*` |

**Importante:** estas assinaturas ilustram responsabilidades e fluxos de dados. **Não** constituem uma obrigação de criar estes métodos, rotas REST, serviços remotos ou estes nomes exatos.

## Decisões futuras da camada de integração

- Fornecedores e permissões/licenças de utilização das APIs (`Q-07`).
- Modelo de ingrediente e normalização das unidades (`Q-01`).
- Persistência offline de receitas e modelo canónico (`Q-03`, `Q-08`).
- Credenciais/chaves e armazenamento seguro, caso exigidas pelos fornecedores (`Q-07`).
- Tratamento de indisponibilidade/limites de APIs externas (`Q-15`).
