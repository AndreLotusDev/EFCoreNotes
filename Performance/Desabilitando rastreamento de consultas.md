---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 4:37:52 pm
date modified: sábado, novembro 16º 2024, 4:52:14 pm
---
Todas as consultas por padrão feitas no ef core são rastreadas, portanto se você quer que o comportamento padrão do EF Core seja diferente é necessário especificar e configurar o AppDbContext.

Para desabilitar o rastreamento de consultas no EF Core, você pode fazer o seguinte:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking);
    }
}
```

No EF Core 5 podemos configurar também o NoTrackingWithIdentityResolution:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseQueryTrackingBehavior(QueryTrackingBehavior.NoTrackingWithIdentityResolution);
    }
}
```
