Indices

```
db.Task.createIndex({ start_date: 1 });
db.Task.createIndex({ status: 1 });
```

Estatísticas de desempenho

Não consegui chegar em uma melhora significativa no tempo de resposta das queries, pela quantidade de dados inputados, mesmo colocando até 300 documentos no banco não houve diminuição ou aumento no tempo.
