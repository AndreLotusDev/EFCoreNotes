---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:30:42 am
date modified: sexta-feira, novembro 15º 2024, 1:09:33 am
---
Interceptadores de comandos no EF Core é um recurso que nos fornece a capacidade de interceptar basicamente todas as operações que são enviadas para nosso banco de dados.

IDbCommandInterceptor.
IDbConnectionInterceptor.

Parece muito com o que temos na API o que chamamos de middleware.

![[Pasted image 20241115003127.png]]

--- 

# Como criar um interceptador?

Para criar um interceptador basta criar uma classe que hera uma interface do tipo IDbCommandInterceptor, permitindo assim selecionar os comandos que voce que sobrescrever ou adicionar funcionalidades, outros voce pode simplesmente ignorar.

Exemplo:

```cs
public class Interceptador : DbCommandInterceptor {

}
```

Herdando a interface voce pode fazer o mesmo, todavia tem que implementar todos os comandos, não podendo selecionar quais voce quer usar.

```cs
public class Interceptador : IDbCommandInterceptor {
    public void NonQueryExecuted(DbCommand command, DbCommandInterceptionContext<int> interceptionContext) {
        throw new NotImplementedException();
    }

    public void NonQueryExecuting(DbCommand command, DbCommandInterceptionContext<int> interceptionContext) {
        throw new NotImplementedException();
    }

    public void ReaderExecuted(DbCommand command, DbCommandInterceptionContext<DbDataReader> interceptionContext) {
        throw new NotImplementedException();
    }

    public void ReaderExecuting(DbCommand command, DbCommandInterceptionContext<DbDataReader> interceptionContext) {
        throw new NotImplementedException();
    }

    public void ScalarExecuted(DbCommand command, DbCommandInterceptionContext<object> interceptionContext) {
        throw new NotImplementedException();
    }

    public void ScalarExecuting(DbCommand command, DbCommandInterceptionContext<object> interceptionContext) {
        throw new NotImplementedException();
    }
}
}
```

Depois de implementado podemos usar na hora de construir o contexto na injeção de dependência.

```cs
services.AddDbContext<Contexto>(options => {
    options.UseSqlServer("connectionString");
    options.AddInterceptors(new Interceptador());
});
```

---

