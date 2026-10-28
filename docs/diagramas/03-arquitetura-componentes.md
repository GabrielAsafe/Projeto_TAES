# UML/Componentes — Arquitetura lógica (independente da stack)

```mermaid
flowchart TB
  subgraph DEV[Dispositivo móvel]
    UI[Interface mobile-first]
    subgraph APP[Aplicação modular]
      PROF[Perfis e restrições]
      PAN[Despensa e categorias]
      SHOP[Compras]
      REC[Receitas e correspondência]
      COOK[Cook Mode e conclusão]
      PORT[Exportação / importação]
      ADAP[Adaptadores para integrações]
    end
    DB[(Persistência local)]
    CAMERA[Câmara / ficheiros / temporizadores]
  end
  OFF[Open Food Facts]
  RECAPI[Fornecedor de receitas]
  AI[Fornecedor GenAI]
  SEC[Camada de proteção de credenciais, se necessária]
  UI --> PROF & PAN & SHOP & REC & COOK & PORT
  UI --> CAMERA
  PROF & PAN & SHOP & REC & COOK & PORT <--> DB
  PAN --> ADAP
  REC --> ADAP
  ADAP --> OFF
  ADAP --> RECAPI
  ADAP -. credencial protegida .-> SEC
  SEC -. opcional / a negociar .-> AI
  ADAP -. opção sem segredos embebidos .-> AI
  COOK --> PAN
  COOK --> REC
  SHOP --> PAN
```

## Interpretação

- O modelo **não obriga** à criação de microserviços, servidor próprio, REST API interna ou várias bases de dados.
- A aplicação deve continuar funcional em fluxos locais mesmo sem rede; pesquisa e IA dependem da disponibilidade dos respetivos fornecedores, salvo alternativas específicas.
- A camada `SEC` **não está decidida**. APIs de IA com chaves privadas exigem uma solução de segurança aprovada: pequeno proxy/serverless, integração disponibilizada institucionalmente, ou outro mecanismo compatível com as regras do projeto.
- Scanning de código de barras é uma capacidade de **dispositivo/biblioteca**, distinta da consulta HTTP ao catálogo de produtos.
- Adaptadores isolam as diferenças entre APIs para que o modelo de `Recipe` seja estável.
