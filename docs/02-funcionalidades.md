# 02 — Funcionalidades e requisitos funcionais

> Todos os itens `RF-*` abaixo são extraídos do enunciado. Os identificadores são introduzidos nesta documentação, não constam do texto original.

## 1. Onboarding e perfis (`RF-PER`)

| ID | Requisito |
|---|---|
| RF-PER-01 | Na primeira utilização, apresentar um fluxo de configuração do perfil por omissão. |
| RF-PER-02 | Permitir configurar o número habitual de porções. |
| RF-PER-03 | Permitir configurar estilos alimentares (ex.: vegetariano, vegan). |
| RF-PER-04 | Permitir configurar alergias alimentares. |
| RF-PER-05 | Permitir configurar ingredientes excluídos. |
| RF-PER-06 | Permitir criar e gerir múltiplos perfis. |
| RF-PER-07 | Permitir trocar o perfil ativo no cabeçalho do dashboard, a qualquer momento. |
| RF-PER-08 | Manter inventário, lista de compras e livro de receitas partilhados entre perfis. |
| RF-PER-09 | Aplicar automaticamente preferências e porções do perfil ativo à pesquisa de receitas e às sugestões de IA. |
| RF-PER-10 | Nas definições, permitir criar, editar e eliminar perfis, incluindo as respetivas restrições e porções. |

**Fluxo:** primeira abertura → configuração do perfil por omissão → dashboard → seleção/troca de perfil → pesquisas e geração de receitas respeitam o perfil ativo.

## 2. Despensa inteligente (`RF-PAN`)

| ID | Requisito |
|---|---|
| RF-PAN-01 | Registar cada produto com nome, categoria de armazenamento, quantidade, unidade e data de validade. |
| RF-PAN-02 | Disponibilizar categorias alimentares comuns. |
| RF-PAN-03 | Permitir criar uma categoria personalizada diretamente no modal de produto. |
| RF-PAN-04 | Destacar numa área de alertas os ingredientes cuja validade ocorre nas próximas 48 horas. |

**Fluxo:** abrir formulário → introduzir/selecionar dados → opcionalmente criar categoria → guardar → produto aparece no inventário e, se aplicável, nos alertas.

## 3. Inserção e consulta de produtos (`RF-PROD`)

| ID | Requisito |
|---|---|
| RF-PROD-01 | Ler códigos de barras de produtos embalados através da câmara do dispositivo. |
| RF-PROD-02 | Consultar bases de dados públicas de produtos e pré-preencher nome, categoria e tamanho padrão. |
| RF-PROD-03 | Permitir ajustar os campos pré-preenchidos antes de guardar. |
| RF-PROD-04 | Oferecer imediatamente upload de imagem ou inserção manual quando a câmara estiver bloqueada, indisponível ou o código não constar da base consultada. |

**Fluxo:** abrir inserção → digitalizar código → consultar base de produtos → rever e ajustar formulário → guardar na despensa. **Alternativa:** upload de imagem ou entrada manual. O processamento de imagem após upload está por definir (`Q-06`).

## 4. Descoberta de receitas (`RF-DESC`)

| ID | Requisito |
|---|---|
| RF-DESC-01 | Pesquisar receitas de catálogo através de APIs públicas, cruzando-as com o stock. |
| RF-DESC-02 | Calcular e mostrar a percentagem de sobreposição de ingredientes por receita. |
| RF-DESC-03 | Identificar claramente ingredientes disponíveis e em falta. |
| RF-DESC-04 | Priorizar receitas que aproveitam ingredientes próximos da validade. |
| RF-DESC-05 | Filtrar automaticamente receitas incompatíveis com estilos alimentares, alergias ou ingredientes excluídos do perfil ativo. |
| RF-DESC-06 | Permitir adicionar à lista de compras, com um clique, os ingredientes em falta apresentados nos cartões das receitas. |

**Fluxo:** selecionar perfil → pesquisar catálogo → aplicar restrições → calcular correspondência com despensa → ordenar/priorizar → consultar disponíveis e em falta → adicionar ingredientes em falta à lista de compras, se desejado.

## 5. Livro de receitas (`RF-LIB`)

| ID | Requisito |
|---|---|
| RF-LIB-01 | Guardar como favoritas receitas de catálogo e receitas criadas por IA. |
| RF-LIB-02 | Consultar os detalhes de receitas guardadas. |
| RF-LIB-03 | Organizar receitas guardadas em coleções e pastas personalizadas. |
| RF-LIB-04 | Registar e apresentar quantas vezes cada receita guardada foi preparada. |
| RF-LIB-05 | Permitir acesso offline às receitas guardadas. |

**Fluxo:** selecionar receita → guardar → organizar numa coleção/pasta → abrir futuramente, incluindo sem ligação de rede → consultar contador de preparações.

## 6. GenAI Sous-Chef (`RF-AI`)

| ID | Requisito |
|---|---|
| RF-AI-01 | Permitir selecionar ingredientes/sobras para usar numa receita original. |
| RF-AI-02 | Enviar os ingredientes selecionados, restrições alimentares e porções do perfil ativo a uma API de GenAI. |
| RF-AI-03 | Receber uma receita estruturada com tempos de preparação, porções, ingredientes e quantidades, e instruções passo a passo. |

**Fluxo:** selecionar sobras → reunir preferências do perfil ativo → pedir receita à IA → apresentar receita estruturada → opção de cozinhar e/ou guardar (a ligação a estas funcionalidades é suportada pelo enunciado).

## 7. Cook Mode (`RF-COOK`)

| ID | Requisito |
|---|---|
| RF-COOK-01 | Apresentar instruções sequenciais num carrossel passo a passo. |
| RF-COOK-02 | Destacar apenas os ingredientes e medidas necessários no passo ativo. |
| RF-COOK-03 | Disponibilizar temporizadores decrescentes para ações temporizadas. |
| RF-COOK-04 | Permitir iniciar, pausar e repor cada temporizador. |
| RF-COOK-05 | Apresentar um alerta visual quando um temporizador chega ao fim. |

**Fluxo:** abrir receita → iniciar Cook Mode → avançar/recuar entre passos → operar temporizadores nos passos relevantes → concluir receita.

## 8. Conclusão da refeição (`RF-MEAL`)

| ID | Requisito |
|---|---|
| RF-MEAL-01 | No final do Cook Mode, apresentar resumo das quantidades consumidas. |
| RF-MEAL-02 | Permitir confirmar ou ajustar as quantidades realmente utilizadas. |
| RF-MEAL-03 | Permitir optar por não descontar os ingredientes do inventário. |
| RF-MEAL-04 | Quando o desconto é confirmado, reduzir quantidades, atualizar existências e remover os produtos esgotados. |
| RF-MEAL-05 | Permitir guardar uma receita ainda não guardada no Livro de Receitas aquando da conclusão. |
| RF-MEAL-06 | Incrementar automaticamente o contador de preparações quando a conclusão da refeição é confirmada. |

**Fluxo:** terminar Cook Mode → rever/alterar consumos → escolher atualizar ou não o stock → confirmar conclusão → atualizar contador → opcionalmente guardar receita.

## 9. Lista de compras (`RF-SHOP`)

| ID | Requisito |
|---|---|
| RF-SHOP-01 | Disponibilizar a lista de compras a partir do cabeçalho superior das vistas principais. |
| RF-SHOP-02 | Permitir adicionar artigos manualmente. |
| RF-SHOP-03 | Permitir receber diretamente ingredientes em falta de receitas. |
| RF-SHOP-04 | Permitir assinalar os artigos comprados. |
| RF-SHOP-05 | Transferir em lote os artigos assinalados para a despensa, definindo categorias, quantidades e validades. |

**Fluxo:** adicionar produtos → marcar os comprados → iniciar transferência em lote → preencher dados para inventário → transferir.

## 10. Portabilidade de dados (`RF-DATA`)

| ID | Requisito |
|---|---|
| RF-DATA-01 | Exportar o estado completo da aplicação num ficheiro JSON estruturado. |
| RF-DATA-02 | Incluir, pelo menos, perfis, inventário, categorias personalizadas, lista de compras e livro de receitas na exportação. |
| RF-DATA-03 | Restaurar dados por importação de ficheiro. |
| RF-DATA-04 | Permitir importar com substituição (overwrite) ou fusão (merge) do estado. |

**Fluxo:** definições → exportar JSON **ou** escolher ficheiro JSON → selecionar substituição/fusão → importar.

## Cadeias funcionais transversais

- **Perfil → receitas:** `RF-PER-09` afeta `RF-DESC-05` e `RF-AI-02`.
- **Despensa → receitas → compras:** `RF-PAN-01` alimenta `RF-DESC-02/03`; `RF-DESC-06` alimenta `RF-SHOP-03`.
- **Compras → despensa:** `RF-SHOP-05` cria/atualiza stock na despensa; a operação concreta sobre duplicados não está definida (`Q-11`).
- **Receitas → Cook Mode → despensa/livro:** `RF-COOK-*` conduz a `RF-MEAL-*`, afetando `RF-PAN-*` e `RF-LIB-04`.
- **Portabilidade:** `RF-DATA-*` abrange todo o estado persistido dos módulos anteriores.
