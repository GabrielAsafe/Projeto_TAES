# 07 — Regras de negócio

## Regras explícitas do enunciado

| ID | Regra | Requisitos |
|---|---|---|
| RN-01 | Existe um perfil ativo usado nas pesquisas e sugestões de IA. | `RF-PER-07/09` |
| RN-02 | Inventário, lista de compras e livro de receitas são partilhados pelos perfis. | `RF-PER-08` |
| RN-03 | Receitas incompatíveis com estilo alimentar, alergénios ou ingredientes excluídos do perfil ativo não devem aparecer na descoberta. | `RF-DESC-05` |
| RN-04 | Ingredientes que estão a menos de, ou até, 48 horas de expirar são destacados numa área de alertas. A fronteira exata e o tratamento de expirados exigem decisão. | `RF-PAN-04` |
| RN-05 | A descoberta apresenta percentagem de correspondência e separa ingredientes disponíveis dos que faltam. | `RF-DESC-02/03` |
| RN-06 | Receitas que consomem ingredientes próximos da validade têm prioridade. | `RF-DESC-04` |
| RN-07 | A receita de IA é gerada a partir de ingredientes escolhidos e das restrições/porções do perfil ativo. | `RF-AI-01/02` |
| RN-08 | O Cook Mode mostra apenas os ingredientes e medidas pertinentes ao passo atual. | `RF-COOK-02` |
| RN-09 | A conclusão permite rever e corrigir quantidades antes de atualizar a despensa. | `RF-MEAL-01/02` |
| RN-10 | Descontar stock na conclusão é opcional; quando escolhido, reduzir quantidades, atualizar remanescentes e remover artigos esgotados. | `RF-MEAL-03/04` |
| RN-11 | Confirmar a conclusão incrementa o contador de preparações da receita. | `RF-MEAL-06` |
| RN-12 | Artigos de compras assinalados podem ser transferidos em lote, recolhendo categoria, quantidade e validade. | `RF-SHOP-04/05` |
| RN-13 | A importação de estado suporta substituição e fusão. | `RF-DATA-03/04` |

## Cálculos a especificar

### Alerta de validade (RN-04)

**[EXPLÍCITO]** Janela de alerta: **48 horas até à data de expiração**.  
**[POR DEFINIR]** Se a data inclui hora, a inclusão do instante exato das 48 h, tratamento de artigos já expirados e de datas sem hora (`Q-04`).

### Percentagem de correspondência (RN-05)

**[EXPLÍCITO]** Apresentar percentagem de ingredientes em comum com a despensa.  
**[POR DEFINIR]** Denominador, presença vs. quantidade suficiente, equivalência de nomes e conversão de unidades (`Q-01`, `Q-05`). **Não** fixar uma fórmula sem aprovação.

### Priorização de receitas (RN-06)

**[EXPLÍCITO]** Favorecer receitas que utilizem ingredientes perto da validade.  
**[POR DEFINIR]** Como combinar prioridade por validade com a percentagem de correspondência, filtros e outras ordenações (`Q-05`).

### Consumo e desconto de stock (RN-10)

**[EXPLÍCITO]** O utilizador confirma/ajusta o consumo e escolhe se desconta; artigos esgotados desaparecem do inventário.  
**[POR DEFINIR]** Conversão entre unidades, múltiplos lotes do mesmo ingrediente, consumo superior ao disponível e regras de arredondamento (`Q-02`, `Q-11`).

### Importação em modo merge (RN-13)

**[EXPLÍCITO]** O utilizador pode fazer overwrite ou merge.  
**[POR DEFINIR]** Chaves de correspondência, conflitos, duplicados, contadores, pastas e perfil ativo (`Q-12`).

## Regras de segurança de produto a validar

**[PROPOSTA — não exigido explicitamente como algoritmo]** Em receitas de terceiros ou geradas por IA, verificar de forma conservadora as restrições alimentares antes de apresentar uma sugestão como compatível. O enunciado **exige filtros** na descoberta de catálogo e **passagem das restrições** à geração por IA, mas não prescreve um processo técnico de validação independente da resposta do modelo (`Q-14`).

## Não adicionar silenciosamente

O enunciado não define notificações de expiração, dedução automática ao abrir a receita, movimentação automática de compras não assinaladas, histórico de consumos ou reposição automática de stock. Estas funcionalidades devem ser consideradas novas propostas, se vierem a ser discutidas.
