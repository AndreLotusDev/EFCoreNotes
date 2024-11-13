---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:59:36 pm
date modified: segunda-feira, novembro 11º 2024, 2:31:10 pm
---
É possível com EF Core criar conversões entre a camada do backend e o próprio banco de dados. Como por exemplo, no SQL Server não temos enum, então podemos converter o ENUM do C# para STRING no banco de dados SQL SERVER.

Exemplo:

```cs
public enum Tipo
{
    A = 1,
    B = 2,
    C = 3
}

public class Entidade
{
    public Tipo Tipo { get; set; }
}

public class Contexto : DbContext
{
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Entidade>()
            .Property(e => e.Tipo)
            .HasConversion(
                v => v.ToString(),
                v => (Tipo)Enum.Parse(typeof(Tipo), v));
    }
}
```

