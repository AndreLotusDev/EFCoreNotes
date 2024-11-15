---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:47:56 am
date modified: sexta-feira, novembro 15º 2024, 12:52:49 am
---
Podemos sobrescrever ao herdar da classe base DbCommandInterceptor as seguintes duas funções: ReaderExecuting (1) e ReaderExecutingAsync(2).

```cs
public class Interceptador : DbCommandInterceptor {
	    public override void ReaderExecuting(DbCommand command, DbCommandInterceptionContext<DbDataReader> interceptionContext) {
        Console.WriteLine("ReaderExecuting");

		return base.ReaderExecuting(command, interceptionContext);
    }

    public override void ReaderExecutingAsync(DbCommand command, DbCommandInterceptionContext<DbDataReader> interceptionContext, CancellationToken cancellationToken) {
        Console.WriteLine("ReaderExecutingAsync");

		    return base.ReaderExecutingAsync(command, interceptionContext, cancellationToken);
    }
}
```

Ao sobrescrever os dois metodos da seguinte maneira, qualquer query ao ser executada e exigir leitura do que retornou do banco ira cuspir no Console uma das duas mensagems.

Exemplo (ReaderExecuting):

```cs
using (var context = new BloggingContext()) {
    var query = context.Blogs.Where(b => b.Name.Contains("Entity Framework"));
    var result = query.ToList();
}
```

Exemplo (ReaderExecutingAsync):

```cs
using (var context = new BloggingContext()) {
    var query = context.Blogs.Where(b => b.Name.Contains("Entity Framework"));
    var result = query.ToListAsync();
}
```
