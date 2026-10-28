# BDD — exemplo de especificações de aceitação

> Exemplos demonstrativos, **não são testes executados nem cenários aprovados pelo Product Owner**. Os ficheiros `.feature` reais e os passos Groovy deverão ser implementados com Katalon Studio.

```gherkin
Feature: Alertas de produtos próximos da validade
  As a household user
  I want to see food expiring soon
  So that I can plan meals and reduce waste

  Scenario: Highlight a product expiring within 48 hours
    Given the pantry contains a product expiring in 24 hours
    When I open the Smart Pantry dashboard
    Then the product is visible in the expiration alert tray

  Scenario: Do not highlight a product expiring after 48 hours
    Given the pantry contains a product expiring in 72 hours
    When I open the Smart Pantry dashboard
    Then the product is not visible in the expiration alert tray
```

```gherkin
Feature: Completing a cooked meal
  As a household user
  I want to confirm ingredient consumption
  So that pantry stock reflects what I used

  Scenario: Confirm consumption and decrement stock
    Given I have 500 grams of rice in the pantry
    And the selected recipe requires 200 grams of rice
    When I complete the recipe and confirm stock depletion
    Then the pantry contains 300 grams of rice
    And the recipe cooking counter increases by one

  Scenario: Complete a meal without changing stock
    Given I have 500 grams of rice in the pantry
    When I complete the recipe and skip stock depletion
    Then the pantry still contains 500 grams of rice
    And the recipe cooking counter increases by one
```

## Testabilidade

- Usar relógio controlado/mocks para testes de **48 h**; não depender do tempo real do dispositivo.
- Usar APIs simuladas e respostas conhecidas no teste de regra de negócio; complementar com *spike* de integração real.
- Asserções Groovy devem verificar o efeito real (quantidade, contador, alerta), não apenas o clique.
- Guardar relatórios Katalon junto das evidências da sprint.

Referência: [Katalon BDD Cucumber integration](https://docs.katalon.com/katalon-studio/bdd-testing/bdd-testing-framework-cucumber-integration).
