---
aliases: 
tags: 
date created: quarta-feira, outubro 23º 2024, 11:05:24 pm
date modified: quarta-feira, outubro 23º 2024, 11:11:14 pm
---
PS: O EF Core não implementa de forma nativa e direta o lazy loading, para isso é necessário instalar um pacote para que isso seja possível, tem também o adendo que esse pacote por debaixo dos panos usa proxies e o castle proxies para ser mais exato.

Primeiro instale o pacote requerido: Install-Package Microsoft.EntityFrameworkCore.Proxies

Configure a string de conexao: 

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    optionsBuilder
        .UseLazyLoadingProxies()
        .UseSqlServer("sua_string_de_conexão");
}
```

Com isso voce implementa o lazy loading no ef core.

---

O lazy loading é muito parecido com o explicit loading.

A diferença se dar pela nuance sútil de que não é necessário deixar explicito a nova chamada no banco como no explicit loading

```csharp
var blog = dbContext.Blogs.First();

// Os posts não são carregados até que sejam acessados
foreach (var post in blog.Posts)
{
    Console.WriteLine(post.Titulo);
}
```

No exeplo acima, carregamos somente todos os blogs, e somente quando eu itero os blogs, para cada blog eu faco uma chamada adicional no banco para ler todos os posts do blog referido.

Ou seja, temos o tradeoff de nao trazer tudo em memoria, todavia precisamos ficar chamando o banco toda hora, transferindo os danos em memoria para o IO, rede e conexoes dependuradas no banco de forma simultanea.

---

