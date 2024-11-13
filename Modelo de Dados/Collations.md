---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:15:53 pm
date modified: segunda-feira, novembro 11º 2024, 1:18:29 pm
---
Introduzido no EF Core 5.0.

Collation é a configuração como os dados são ordenados, comparados e codificados.

Para se configurar um collation no ef core.

Exemplo:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .UseCollation("SQL_Latin1_General_CP1_CS_AS");
}
```

Com isso eu estou usando a collation latin1, case sensitive e acentos sensíveis. Portanto se eu tenho no banco uma pessoa André e eu pesquisar com a seguinte QUERY eu não irei achar:

```sql
SELECT * FROM Blog WHERE Url = 'andre'
```



