---
aliases: 
tags: 
date created: sexta-feira, novembro 8º 2024, 4:57:28 pm
date modified: sexta-feira, novembro 8º 2024, 5:09:13 pm
---
É importante salientar acima de tudo que em ambientes de produção não é aconselhável habilitar logs sensitivos, portanto essa feature é mais útil para debugging em ambientes de teste e desenvolvimento.

Exemplo:

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Logging;

public class MyDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder
            .UseSqlServer("YourConnectionString")
            .EnableSensitiveDataLogging() // Enable sensitive data logging
            .LogTo(Console.WriteLine, LogLevel.Information); // Configure logging output
    }

    // DbSets and other configurations
}
```

---

