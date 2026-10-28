# UML/Estados — Sessão Cook Mode

```mermaid
stateDiagram-v2
    [*] --> Ready
    Ready --> Cooking : iniciar
    Cooking --> Cooking : próximo/anterior passo
    Cooking --> TimerRunning : iniciar temporizador
    TimerRunning --> TimerPaused : pausar
    TimerPaused --> TimerRunning : retomar
    TimerRunning --> Cooking : terminou / reset
    TimerPaused --> Cooking : reset
    Cooking --> ReviewConsumption : concluir passos
    TimerRunning --> ReviewConsumption : concluir passos
    ReviewConsumption --> Cooking : voltar/editar
    ReviewConsumption --> Completed : confirmar com desconto
    ReviewConsumption --> Completed : confirmar sem desconto
    Completed --> [*]
    Ready --> Abandoned : sair
    Cooking --> Abandoned : cancelar
    Abandoned --> [*]
```

`TimerRunning` é um estado UI temporário. Se os timers devem sobreviver ao fecho/reabertura da aplicação é uma decisão de requisitos ainda pendente (Q-13). O registo de conclusão só acontece ao entrar em `Completed`.
