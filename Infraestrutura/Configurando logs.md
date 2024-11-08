---
aliases: 
tags: 
date created: quinta-feira, novembro 7º 2024, 3:57:58 pm
date modified: sexta-feira, novembro 8º 2024, 4:27:28 pm
---
Podemos na hora de configurar o sinkink de logging da aplicação configurar o level que podera ser dumpado e para onde ele poderá ser dumpado.

Exemplo:

```csharp
const string strConnection = "Data Source=.;Initial Catalog=Log;Integrated Security=True";

optionsBuilder.UseSqlServer(strConnection, x => x.CommandTimeout(60).EnableRetryOnFailure(5).MigrationsHistoryTable("LogMigration"))
.LogTo(Console.WriteLine, LogLevel.Information);
```

Com essa configuração, todos os logs do tipo informations produzidos pelo EF Core serão dumbados na aba de console de sua aplicação.

---

Há também a possibilidade de dumpar/sinking de log de multiplos levels ao mesmo tempo.

```csharp
optionsBuilder.UseSqlServer(strConnection, x => x.CommandTimeout(60).EnableRetryOnFailure(5).MigrationsHistoryTable("LogMigration"))
.LogTo(Console.WriteLine, new[] { LogLevel.Information, LogLevel.Error });
```


Com isso podemos receber os logs de informação e também os logs de erro.

---

Também é possível logar por tipo de log ID

```csharp
optionsBuilder.UseSqlServer(strConnection, x => x.CommandTimeout(60).EnableRetryOnFailure(5).MigrationsHistoryTable("LogMigration"))
.LogTo(Console.WriteLine, new[] { RelationalEventId.CommandExecuted, RelationalEventId.CommandError });
```

---

É também possível de configurar durante o sinking que eu posso formatar o log com a hora local e em linha unica.

```csharp
var SimpleLoggingFormatter = (eventId, state) =>
{
    var log = $"[{DateTime.Now.ToLocalTime()}] {eventId}: {state}";
    return log;
};

optionsBuilder.UseSqlServer(strConnection, x => x.CommandTimeout(60).EnableRetryOnFailure(5).MigrationsHistoryTable("LogMigration"))
.LogTo(Console.WriteLine, new[] { RelationalEventId.CommandExecuted, RelationalEventId.CommandError }, LogLevel.Information, SimpleLoggingFormatter);
```
