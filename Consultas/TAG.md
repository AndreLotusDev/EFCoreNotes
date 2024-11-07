---
aliases: 
tags: 
date created: quinta-feira, outubro 24º 2024, 1:22:17 am
date modified: quinta-feira, outubro 24º 2024, 1:23:43 am
---
É possível enviar consultas com tag utilizando o EF Core.

Exemplo:

```csharp
var departamento = await context.Departamentos
    .TagWith("Esta é uma consulta de exemplo.")
    .FirstOrDefaultAsync();
```

O método `TagWith` adiciona um comentário SQL à consulta gerada. Isso pode ser útil para depuração ou para identificar consultas em logs de banco de dados.
