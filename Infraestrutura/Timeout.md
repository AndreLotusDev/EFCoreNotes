---
aliases: 
tags: 
date created: sexta-feira, novembro 8º 2024, 5:17:51 pm
date modified: sexta-feira, novembro 8º 2024, 5:23:24 pm
---
É possível configurar globalmente um timeout no ef core.

Por default o ef core especifica um timeout de 30 segundos.

Exemplo:

```csharp
var optionsBuilder = new DbContextOptionsBuilder<BloggingContext>();

optionsBuilder.UseSqlServer(
    @"Server=(localdb)\mssqllocaldb;Database=EFQuerying;Connect Timeout=30"
);
```

ou tambem pelo optionsBuilder sem ser pela connection string:

```csharp
var optionsBuilder = new DbContextOptionsBuilder<BloggingContext>();

optionsBuilder.UseSqlServer(
    @"Server=(localdb)\mssqllocaldb;Database=EFQuerying",
    options => options.CommandTimeout(60)
);
```

---

É possível também configurar temporariamente um CommandTimeOut para somente um fluxo em especifico.

Exemplo:

```csharp
using var db = new BloggingContext();

using var transaction = db.Database.BeginTransaction();

try
{
    db.Database.SetCommandTimeout(30);

    db.Database.ExecuteSqlRaw("UPDATE Blogs SET Rating = 5");

    transaction.Commit();
}
catch (Exception)
{
    transaction.Rollback();
}
```
