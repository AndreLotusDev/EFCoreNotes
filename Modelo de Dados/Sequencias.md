---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:24:47 pm
date modified: segunda-feira, novembro 11º 2024, 1:35:43 pm
---
Atráves do EF Core podemos criar uma sequencia customizada.

Para se configurar uma sequencia exemplo:

```csharp
modelBuilder.HasSequence<int>("MinhaSequencia", schema: "dbo")
    .StartsAt(1)
    .IncrementsBy(1)
    .HasMin(1)
    .HasMax(1000)
    .IsCyclic();
```

Para se utilizar a sequencia:

```csharp
modelBuilder.Entity<MinhaEntidade>()
    .Property(x => x.Id)
    .UseHiLo("MinhaSequencia", "dbo");
```

