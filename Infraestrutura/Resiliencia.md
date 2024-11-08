---
aliases: 
tags: 
date created: sexta-feira, novembro 8º 2024, 5:23:49 pm
date modified: sexta-feira, novembro 8º 2024, 5:58:55 pm
---
É possível configurar o EF Core para ele ser apto de ser mais resiliente, como com problemas de conexão, para isso basta na hora de configurar o dbContext adicionar uma linha de configuração.

Exemplo:

```csharp
const string connectionString = "Server=localhost;Database=EFCore;User

optionsBuilder.UseSqlServer(connectionString, options =>
{
    options.EnableRetryOnFailure(
        maxRetryCount: 5,
        maxRetryDelay: TimeSpan.FromSeconds(30),
        errorNumbersToAdd: null);
});
```

Com isso, se algum erro acontece, ele retenta novamente com um espacamento de 30 segundos.

---

Todavia adicionando essa configuração é necessário estar ciente que se alguma coisa é adicionada ao nosso banco de dados e tenha um erro ao tentar retornar o STATUS para o backend ou usuário final o sistema simplesmente tentará executar novamente o comando de insert ou seu semelhante, para se evitar isso podemos utilizar o padrão strategy.

```cs

static void ExecutaInsertNoBanco()
{
    var strategy = new ExecutionStrategy();
    strategy.Execute(() =>
    {
        using (var context = new BloggingContext())
        {
            context.Blogs.Add(new Blog { Url = "http://blogs.msdn.com/dotnet" });
            context.SaveChanges();
        }
    });
}
```
