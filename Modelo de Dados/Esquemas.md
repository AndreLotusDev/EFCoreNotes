---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:56:14 pm
date modified: segunda-feira, novembro 11º 2024, 1:57:51 pm
---
É possível utilizar schemas pelo EF Core.

Exemplo:

```csharp
modelBuilder.HasSchema("default");
```

É também possível configurar o schema para uma tabela única.

Exemplo:

```csharp
modelBuilder.Entity<Blog>().ToTable("Blogs", schema: "blogging");
```
