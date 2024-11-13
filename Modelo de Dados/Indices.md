---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:35:43 pm
date modified: segunda-feira, novembro 11º 2024, 1:47:45 pm
---
A priori quando falamos de criar indice no banco de dados, geralmente nos referimos criação de indice para aumentar a performance.

É possível criar indices de coluna única pelo EF Core como também indices multi valorados com mais de uma coluna.

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => p.Nome);
```

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => new { p.Nome, p.Sobrenome });
```

O EF Core também permite a criação de indices únicos.

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => p.Nome)
    .IsUnique();
```

Também é possível criar indices com nome especifico.

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => p.Nome)
    .HasDatabaseName("IX_Nome");
```

Também é possível indexar somente valores não nullos.

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => p.Nome)
    .IsUnique()
    .HasFilter("[Nome] IS NOT NULL");
```

É também possível configurar o fator de preenchimento das páginas das tabelas.

```csharp
modelBuilder.Entity<Pessoa>()
    .HasIndex(p => p.Nome)
    .IsUnique()
    .HasFillFactor(80);
```



