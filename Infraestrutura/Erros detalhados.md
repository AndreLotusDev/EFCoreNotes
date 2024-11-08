---
aliases: 
tags: 
date created: sexta-feira, novembro 8º 2024, 4:27:28 pm
date modified: sexta-feira, novembro 8º 2024, 4:56:08 pm
---
É possível configurar um wrapper no ef core, ao qual você pode receber logs detalhados de erro, todavia isso não é muito recomendável em ambientes de produção, tendo em vista que é uma sobrecarga de todos os metodos do EF Core, só que contudo é muito útil para ambiente de teste e desenvolvimento pois ajuda a capturar erros e corrigir eles sem maiores problemas.

Exemplo:

```csharp
public class CustomDbContext : DbContext
{
    public CustomDbContext(DbContextOptions<CustomDbContext> options) : base(options)
    {
    }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.EnableDetailedErrors();
    }
}
```

---


