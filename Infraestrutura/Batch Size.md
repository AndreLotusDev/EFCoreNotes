---
aliases: 
tags: 
date created: sexta-feira, novembro 8º 2024, 5:09:13 pm
date modified: sexta-feira, novembro 8º 2024, 5:17:27 pm
---
Por padrão o EF Core tem uma configuração de batch size, isso significa que quando você insere muitos dados de uma vez ao banco de dados ele quebra em comandos menores aos quais ele precisa ir várias vezes ao banco de dados para concluir sua tarefa de inserção de dados.

Em sistemas pequenos isso pode não fazer muita diferença, todavia em ambientes com altos volumes de dados trafegando para la e para ca pode fazer e muita diferença.

Geralmente é também muito recomendável usar essa feature quando sua rede do banco de dados é muito instável, portanto acessar somente uma vez acaba sendo uma melhor opção do que acessando várias vezes.

![[Pasted image 20241108171143.png]]

Exemplo

```csharp
using Microsoft.EntityFrameworkCore;

public class MyDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer(
            "YourConnectionString",
            sqlServerOptions => sqlServerOptions
                .MaxBatchSize(100) // Set batch size to 100
        );
    }

    // DbSets and other configurations
}
```

---