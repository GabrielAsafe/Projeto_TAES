# 11 — APIs, SDKs e integrações candidatas (verificadas em outubro de 2026)

> **Não selecionadas ainda.** São alternativas para *spikes* e comparação de viabilidade; não são dependências impostas pelo enunciado. Separar **biblioteca local** de **API de dados externa**.

## 1. Leitura de códigos de barras

| Opção | Plataforma | Pontos fortes | Limitações e provas necessárias |
|---|---|---|---|
| `@zxing/browser` | Web/PWA | Biblioteca JavaScript com suporte a vídeo, imagem e leitores multiformato; permite fallback por upload | Requer permissões de câmara, HTTPS e testes reais em Android/iOS; comparar performance com native. |
| `BarcodeDetector` | Browser | API nativa do browser; sem fornecedor remoto para leitura | Compatibilidade ainda limitada; não usar como única solução. |
| Google ML Kit Barcode Scanning | Android/iOS via integração nativa ou plugins | Deteção **offline** de códigos padrão | Exige integração mobile, validação do plugin/SDK e dispositivos alvo. |

Referências: [ZXing browser](https://github.com/zxing-js/browser), [MDN Barcode Detection API](https://developer.mozilla.org/en-US/docs/Web/API/Barcode_Detection_API), [ML Kit Barcode Scanning](https://developers.google.com/ml-kit/vision/barcode-scanning).

**Fluxo:** imagem/câmara -> descodificar texto do código -> consultar base de dados de produtos -> corrigir campos -> guardar. A leitura do código pode ocorrer offline; a consulta de produto normalmente exige internet.

## 2. Base de dados pública de produtos

### Opção principal para spike: Open Food Facts

- Endpoint de leitura **atual recomendado**: `GET https://world.openfoodfacts.org/api/v3/product/{barcode}`.
- Campos relevantes para mapeamento, quando disponíveis: `product.product_name`, `product.categories_tags`, `product.product_quantity`, `product.product_quantity_unit`, `product.quantity`, `product.code`.
- O fornecedor recomenda `User-Agent` identificável; no browser alguns cabeçalhos (como `User-Agent`) não podem ser definidos manualmente, pelo que deve ser **testada a integração real**.
- Limites documentados na página oficial: **15 consultas de produtos/min/IP** e **10 pesquisas/min/IP**. Não fazer consultas em cada tecla.
- **Atenção:** versões v2 e v3 têm endpoints diferentes; usar v3 para integrações novas, salvo incompatibilidade demonstrada.
- Produtos podem não existir ou conter metadados incompletos: campos permanecem editáveis, com fallback manual.

Documentação oficial: [introdução](https://openfoodfacts.github.io/documentation/docs/Product-Opener/api/), [GET v3 product](https://openfoodfacts.github.io/documentation/docs/Product-Opener/v3/products/get-api-v3-product-code/).

## 3. Catálogo de receitas — comparação

| API | Endpoints/capacidades relevantes | Adequação | Riscos |
|---|---|---|---|
| **TheMealDB** | `search.php?s=...`, `filter.php?i=...`, `lookup.php?i=...` | Muito simples de prototipar e testar; chave pública de testes `1` | Na API V1 gratuita o filtro por ingrediente é único; vários ingredientes requerem a V2 premium ou pesquisa/classificação local. Confirmação de termos de armazenamento offline obrigatória. |
| **Spoonacular** | `GET /recipes/findByIngredients`, pesquisa e detalhe de receita; dietas/intolerâncias em endpoints apropriados | Alinhamento funcional forte com *ingredientes disponíveis/em falta* | Plano gratuito documentado de **50 pontos/dia**; os termos publicados limitam cache de dados pedidos a **1 hora**, possível incompatibilidade com livro offline. Necessário avaliar contrato/licença antes de usar. |
| **Edamam Recipe Search** | `GET /api/recipes/v2`, filtros por saúde/dieta | Filtros alimentares detalhados | Receitas provenientes da web geralmente **não incluem instruções completas**, apenas ligação à origem; pode não servir Cook Mode/offline sem conteúdo licenciado. |

**Referências oficiais:** [TheMealDB](https://www.themealdb.com/docs_api_guide.php), [Spoonacular docs](https://spoonacular.com/food-api/docs), [Spoonacular preços e cache](https://spoonacular.com/food-api/pricing), [Edamam](https://developer.edamam.com/edamam-docs-recipe-api).

### Avaliação técnica obrigatória por API de receitas

1. Pesquisa com 2–5 ingredientes e retorno de receitas diversas.
2. Respostas completas: título, porções, lista de ingredientes com medidas, **instruções passo a passo**, tempo de preparação e imagem (quando aplicável).
3. Compatibilidade com vegan/vegetariano, alergénios e exclusões, incluindo **dados desconhecidos**.
4. Qualidade do mapeamento para o esquema `Recipe` e indicação de ingredientes em falta.
5. Termos para guardar o conteúdo **offline indefinidamente** e atribuição exigida.
6. Quotas, custos, estabilidade, CORS (se web), erros 401/404/429/500.

**Risco bloqueante:** a obrigação de receitas guardadas offline impede assumir que qualquer API comercial pode alimentar o livro de receitas. Se a licença não permitir cópias persistidas, procurar fornecedor alternativo, conteúdo licenciado ou confirmar outra solução com o Product Owner.

## 4. GenAI — opções a experimentar

| Opção | Adequação | Bloqueadores a resolver |
|---|---|---|
| **Gemini API** | Suporta saída estruturada baseada em JSON Schema | Credenciais secretas; preço/quotas/modelos; validação semântica dos alergénios. |
| **OpenAI API** | Suporta *structured outputs* para modelos/fluxos compatíveis | Credenciais secretas; preço/quotas/modelos; validação semântica dos alergénios. |

Referências: [Gemini structured output](https://ai.google.dev/gemini-api/docs/structured-output), [Gemini API key security](https://ai.google.dev/gemini-api/docs/api-key), [OpenAI structured outputs](https://developers.openai.com/api/docs/guides/structured-outputs), [OpenAI API key safety](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety).

**Pedido conceptual** (não é payload obrigatório de fornecedor):

```json
{
  "selectedIngredients": [{"name": "tomate", "quantity": 2, "unit": "unit"}],
  "profile": {"servings": 2, "lifestyles": ["vegetarian"], "allergens": ["peanut"], "excludedIngredients": ["mushroom"]},
  "outputFormat": "canonical-recipe-v1"
}
```

**Resposta mínima proposta:** `title`, `servings`, `prepMinutes`, `cookMinutes`, `ingredients[{name,quantity,unit}]`, `steps[{position,instruction,timerSeconds?,ingredientsUsed?}]`.

- Validar JSON por esquema **e** restrições do perfil; JSON válido não garante receita segura ou ausência de alergénios.
- Não enviar toda a despensa se só foram escolhidas sobras. Evitar informação pessoal desnecessária.
- Nunca incluir uma chave de equipa no código cliente, app distribuída ou repositório. Uma rota serverless/proxy muito pequena é opção, mas a arquitetura final depende da interpretação de “sem backend obrigatório” pelo Product Owner.
- Prever timeout, limites de custos, resposta recusada/incompleta e demonstrações/testes com respostas simuladas.

## 5. Adaptadores internos (não necessariamente HTTP)

| Porta lógica | Operação proposta | Entrada e saída |
|---|---|---|
| `BarcodeScanner` | `scanBarcode()` | Scanner/câmara -> `barcode` ou erro/fallback |
| `ProductCatalog` | `lookupProduct(barcode)` | Código -> `ProductLookupResult` |
| `RecipeCatalog` | `searchRecipes(criteria)`, `getRecipe(id)` | Critérios -> receitas de catálogo normalizadas |
| `RecipeAI` | `generateRecipe(context)` | Sobras + perfil -> `Recipe` normalizada |
| `RecipeMatcher` | `match(recipe, pantry)` | Receita + stock -> `RecipeMatch` |
| `LocalStore` | `transaction()`, `import()`, `export()` | Estado local, consistência, backup |

## Spikes prioritários (entregáveis verificáveis)

- **SPIKE-01 Barcode:** ler EAN-13 num Android e num iPhone real, testar acesso negado e upload de fotografia; registar vídeo ou screenshots.
- **SPIKE-02 Produtos:** consultar 5 códigos conhecidos e um desconhecido; registar campos disponíveis, limites e falhas.
- **SPIKE-03 Catálogo:** testar 2 APIs para 3 ingredientes e uma restrição alimentar, confirmar instruções e termos de persistência.
- **SPIKE-04 GenAI:** gerar 3 receitas estruturadas com exclusões e alergénios, medir validade de schema e propor segurança de credenciais.
- **SPIKE-05 Katalon:** validar um cenário Gherkin/Groovy no dispositivo/browser realmente pretendido, com relatório Pass/Fail.
