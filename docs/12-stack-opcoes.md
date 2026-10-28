# 12 — Opções de stack tecnológica (comparação inicial, sem decisão)

> O enunciado deixa a equipa escolher a stack. A decisão depende sobretudo de **offline-first**, câmara, testes end-to-end em **Katalon Studio com Gherkin/Groovy**, disponibilidade de dispositivos de teste e capacidade técnica dos quatro elementos.

| Estratégia | Exemplo de stack | Vantagens | Riscos/desvantagens | Testes Katalon |
|---|---|---|---|---|
| **Web mobile-first / PWA** | React + TypeScript + Vite; IndexedDB (Dexie); Service Worker; ZXing | Uma base de código; demonstração simples em browser e telemóvel; competências web reaproveitáveis | Câmara e timers sujeitos à compatibilidade do browser; armazenagem/offline PWA e reinstalação; sem chave de IA segura no cliente | Katalon WebUI/mobile web. Verificar teste real de câmara e browser mobile. |
| **Flutter** | Flutter/Dart; SQLite/Drift ou Isar; plugin scanner | UI consistente Android/iOS, bom acesso a capacidades mobile via plugins | Dart e tooling; testes/inspeção dos widgets no Katalon podem requerer estratégias específicas; builds iOS exigem ecossistema Apple | Katalon Mobile; fazer prova de conceito de reconhecimento de elementos. |
| **React Native / Expo** | React Native + TypeScript; Expo SQLite; módulos scanner | TS e capacidades nativas; possível reutilização de conhecimento React | Dependência de compatibilidade/versões de módulos e Expo; debugging e builds nativas | Katalon Mobile; confirmar IDs acessíveis e estabilidade de cenários. |
| **Android nativo** | Kotlin + Jetpack Compose; Room; ML Kit | Forte integração Android, SQLite madura, boa leitura de barcodes | Só Android se não criar também versão iOS; curva de aprendizagem Android/Compose | Katalon Mobile Android; confirmar suporte para componentes Compose e seletores de acessibilidade. |
| **iOS nativo** | Swift + SwiftUI; SwiftData/SQLite; Vision | Forte integração iOS | Só iOS; necessita macOS para compilar/testar; maior risco para equipa sem experiência Apple | Katalon Mobile iOS; preparar infraestrutura de teste adequada. |

## Matriz de decisão sugerida

Atribuir nota **1 a 5** por critério e multiplicar pelo peso após spikes, sem decidir só pela preferência pessoal:

| Critério | Peso proposto |
|---|---:|
| Viabilidade dos cenários Katalon BDD no dispositivo-alvo | 25% |
| Câmara e fallbacks (foto/manual) | 20% |
| Persistência offline + importação/exportação JSON | 20% |
| Capacidade real e experiência dos 4 alunos | 15% |
| Velocidade para demonstrar incrementos e corrigir falhas | 10% |
| Suporte multiplataforma e portabilidade | 10% |

Esta ponderação é **proposta** e pode ser adaptada. Não confundir “Katalon suporta mobile apps” com “Katalon já consegue automatizar a nossa implementação concreta”; validá-lo num spike. A documentação oficial menciona WebUI, Android, iOS e limitações em webviews híbridas: [Katalon Supported Technologies](https://docs.katalon.com/katalon-studio/supported-technologies-for-katalon-studio).

## Opções de persistência por estratégia

- Web/PWA: IndexedDB como mecanismo de dados locais estruturados, com controlo transacional e migrações; cache da shell com Service Worker, sem confundir cache HTTP com dados do utilizador.
- Flutter/React Native/Android: base de dados local SQLite através de biblioteca adequada; testar exportação/importação de ficheiros e migrações.
- Em todos os casos: definir IDs estáveis, esquema JSON versionado, backups e comportamento sem ligação à internet.

## Decisões que devem ser tomadas depois dos spikes

1. Público alvo obrigatório: Android apenas, iOS apenas, ou ambos? Como serão avaliados os testes?
2. Há dispositivos físicos e ambiente para executar testes Katalon repetidamente?
3. A aplicação deve ser instalável ou é suficiente web mobile-first no browser?
4. O Product Owner aceita uma função serverless **apenas para proteger o acesso à IA**? Se não, qual a solução prevista para credenciais de IA?
5. A API de receitas permite guardar instruções offline de acordo com a licença?

**Ponto de controlo:** a stack é aprovada num ADR (*Architecture Decision Record*) depois de uma pequena demo técnica que comprove leitura de barcode, armazenamento, uma chamada a API e pelo menos um teste BDD automático.
