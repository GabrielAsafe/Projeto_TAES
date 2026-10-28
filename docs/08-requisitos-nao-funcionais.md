# 08 — Requisitos não funcionais e restrições

> Este ficheiro separa as **restrições explicitamente descritas** de atributos de qualidade que poderão ser desejáveis, mas **não constam do enunciado**.

## Confirmados no enunciado

| ID | Requisito/restrição | Implicação |
|---|---|---|
| RNF-01 | Aplicação **mobile-first**. | Interfaces desenhadas prioritariamente para dispositivos móveis. |
| RNF-02 | Aplicação **self-contained**, concebida para operar autonomamente em dispositivos móveis. | Os fluxos locais não dependem de um servidor próprio obrigatório. |
| RNF-03 | **Sem backend obrigatório**. | Não pressupor backend próprio para autenticação ou persistência. APIs externas continuam possíveis/exigidas. |
| RNF-04 | **Receitas guardadas acessíveis offline**. | Necessidade de disponibilidade local dos dados das receitas guardadas. |
| RNF-05 | **Portabilidade por JSON**. | Estado exportável e importável por ficheiros. |
| RNF-06 | **Fallback de introdução de produtos**. | Upload de imagem ou introdução manual quando scan indisponível/sem correspondência. |
| RNF-07 | **Feedback visual do temporizador**. | Alertar visualmente no fim de uma contagem. |
| RNF-08 | **Posse/controlo de dados pelo utilizador**. | Exportação do estado integral e importação em modos overwrite/merge. |

## Dependências e limites

- O acesso offline **explícito** refere-se ao livro de receitas. Não assumir que a descoberta de receitas, a consulta de códigos de barras ou a geração por IA funcionem offline.
- O facto de o projeto ser mobile-first **não especifica** Android/iOS, framework, PWA ou aplicação nativa.
- Não existe fornecedor de API, base de dados local, solução de autenticação ou serviço de sincronização imposto.

## Atributos de qualidade por especificar (não são requisitos fechados)

| Área | Perguntas para a fase técnica |
|---|---|
| Privacidade e segurança | Como proteger ficheiros exportados e eventuais chaves de API? |
| Robustez | Como responder a indisponibilidade das APIs externas? |
| Acessibilidade | Qual o nível de acessibilidade das vistas e alertas? |
| Desempenho | Quais os tempos máximos aceitáveis para abrir vistas, pesquisar e gerar receitas? |
| Persistência | Qual a tecnologia local e como garantir integridade em importações/descontos? |
| Compatibilidade | Que dispositivos, navegadores e versões serão suportados? |
| Internacionalização | Que idiomas, formatos de data, unidades e fusos serão suportados? |
| Testabilidade | Que testes de regras, integração, fluxos offline e importação serão exigidos? |

**Nota:** estas perguntas ajudam a futura especificação de qualidade e não devem ser tratadas como requisitos já aprovados.
