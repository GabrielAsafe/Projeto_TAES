# 09 — Dúvidas, decisões pendentes e pressupostos

> **Estado inicial:** não existem decisões de implementação aprovadas além do que está explícito no enunciado.

## Questões pendentes

| ID | Prioridade | Tema | Pergunta a decidir | Impacto |
|---|---|---|---|---|
| Q-01 | Alta | Ingredientes e unidades | Como normalizar nomes/sinónimos, alergénios, quantidades e unidades entre despensa, catálogos e IA? | Correspondência, filtros, consumo |
| Q-02 | Alta | Inventário | Podem existir lotes separados do mesmo produto com validades diferentes? Como descontar consumo nesses casos? | Modelo de dados, stock, alertas |
| Q-03 | Alta | Receita canónica | Quais os campos mínimos para representar uniformemente receitas de catálogo e IA, incluindo passos e informação offline? | Modelo, APIs, Cook Mode |
| Q-04 | Média | Validades | Data vs. data/hora, limite exato das 48 h, tratamento de produtos já expirados e fusos horários? | Alertas |
| Q-05 | Alta | Descoberta | Qual a fórmula da percentagem de correspondência e a estratégia de priorização por validade? | Relevância das receitas |
| Q-06 | Média | Imagem | O que se espera após o upload de imagem no fallback: anexo, leitura de código da fotografia ou reconhecimento de produto? | UX, integrações |
| Q-07 | Alta | Fornecedores | Quais as APIs públicas de produtos/receitas e de GenAI? Como gerir chaves, quotas, licenças e formatos? | Integrações e viabilidade |
| Q-08 | Alta | Persistência | Que dados são persistidos localmente e qual o alcance do modo offline além das receitas guardadas? | Arquitetura local |
| Q-09 | Média | Organização | Coleções e pastas são conceitos distintos? Há hierarquia? Uma receita pode estar em várias? | Livro de receitas, modelo |
| Q-10 | Média | Contador | Como contar preparações de receitas ainda não guardadas? A confirmação conta mesmo quando se ignora o desconto de stock? | Conclusão de refeição |
| Q-11 | Alta | Movimento de stock | Como lidar com insuficiência de stock, conversão de unidades, lotes duplicados e compras repetidas ao transferir em lote? | Integridade do inventário |
| Q-12 | Alta | Importação/merge | Como definir identidade, duplicados, conflitos, contadores, perfil ativo e versão do JSON durante importação? | Portabilidade, dados |
| Q-13 | Média | Timers | Os temporizadores devem continuar em segundo plano ou com ecrã bloqueado? Ecrã desligado? | Cook Mode e plataforma |
| Q-14 | Alta | Alergénios/IA | Que validação será aplicada às receitas geradas para evitar ingredientes incompatíveis? | Segurança alimentar e confiança |
| Q-15 | Média | Rede | Qual a experiência quando APIs estão indisponíveis, falham ou devolvem dados incompletos? | UX e resiliência |
| Q-16 | Média | Perfis | O que acontece ao apagar o perfil ativo/último perfil e como se escolhe o perfil por omissão após importação? | Gestão de perfis |
| Q-17 | Média | Dados da lista | Quando uma receita envia ingredientes em falta para compras, quantidade e unidade são transportadas? Como resolver duplicados? | Compras, receitas |
| Q-18 | Baixa | Escala de porções | É necessário reajustar quantidades de receitas de catálogo às porções do perfil? Como calcular? | Receita, consumo |

## Distinções que não devemos perder

- **Requisito:** existem vários perfis que partilham despensa, compras e receitas.
- **Não decidido:** modelo de autenticação ou partilha de dados entre dispositivos.
- **Requisito:** receitas guardadas acessíveis offline.
- **Não decidido:** execução offline de pesquisas ou da IA.
- **Requisito:** fallback com upload de imagem ou inserção manual.
- **Não decidido:** análise automática da imagem.
- **Requisito:** importação JSON com substituição e fusão.
- **Não decidido:** algoritmo de fusão nem esquema JSON.
- **Requisito:** percentagem de correspondência entre ingredientes da receita e da despensa.
- **Não decidido:** fórmula, normalização e tratamento de quantidade insuficiente.

## Registo de decisões (a preencher)

| Data | ID | Decisão | Alternativas consideradas | Justificação | Estado |
|---|---|---|---|---|---|
| — | — | Nenhuma decisão técnica registada nesta fase | — | — | Pendente |

## Ordem sugerida de esclarecimento

1. **Definir o ingrediente e a receita canónica:** `Q-01`, `Q-03`, `Q-05`.
2. **Definir a semântica do stock e da sua movimentação:** `Q-02`, `Q-11`, `Q-17`.
3. **Escolher APIs e estratégia de armazenamento local:** `Q-07`, `Q-08`, `Q-12`.
4. **Fechar os restantes detalhes de fluxo:** `Q-04`, `Q-06`, `Q-09`, `Q-10`, `Q-13`, `Q-14`, `Q-16`, `Q-18`.

---

### Template para nova decisão

```md
#### DEC-XXX — Título
- Data:
- Questões relacionadas: Q-...
- Opções consideradas:
- Decisão:
- Motivo:
- Consequências:
- Estado: proposta | aprovada | substituída
```
