---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:22:59 am
date modified: sexta-feira, novembro 15º 2024, 12:27:02 am
---
A função collate no EF.Functions do EF Core permita que utilizemos uma collate diferente da default previamente especificada na coluna.

Todavia temos que ficar muito atento, trocar uma collate da coluna para uma busca especifica tem que ter um proposito muito especifico e bem justificado, pois a priori pode onerar a performance, inclusivamente em grandes volumes de dados, e em alguns casos pode impedir inclusive que o banco utilize indices para retornar a query mais rapidamente.

Exemplo:

```cs
var result = _context.Products
    .Where(p => EF.Functions.Collate(p.Name, "SQL_Latin1_General_CP1_CI_AS") == "test")
    .ToList();
```