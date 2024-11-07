---
aliases: 
tags: 
date created: quinta-feira, outubro 24º 2024, 1:08:39 am
date modified: quinta-feira, outubro 24º 2024, 1:17:46 am
---
Geralmente utilizamos consultas parametrizadas quando queremos extrair maxima performance ou quando o LINQ não nos permite traduzir para uma query nativa do banco de dados.

Independente de ambas situações é sempre bom se atentar para escrever queries com parametros, pois assim evita se ataques de SQL injection e torna suas consultas ao banco de dados mais seguras.

Exemplo:

```csharp
var departamentos = context.Departamentos.FromSqlRaw("SELECT * FROM Departamentos WHERE Nome = {0}", "TI").ToList();
```

Nessa consulta trazemos todos os departamentos que tem o nome TI.

---

É possível dentro dessa query transformar ela numa subquery para outras queries, assim como por exemplo:

```csharp
var departamentos = context.Departamentos.FromSqlRaw("SELECT * FROM Departamentos WHERE Nome = {0}", "TI")
.Where(w => w.Status == "ACTIVO")
.ToList();
```

Com essa query + subquery, trazemos todos departamentos que temo nome TI, todavia somente aqueles que estão ativos.