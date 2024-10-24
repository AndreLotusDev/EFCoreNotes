---
aliases: 
tags: 
date created: quarta-feira, outubro 23º 2024, 11:16:04 pm
date modified: quarta-feira, outubro 23º 2024, 11:18:38 pm
---
Assim como o lazy loading, o explicit loading só é executado a posteriori, ou seja, diferente do eager loading se fazem necessário ir no banco novamente para requerir novos dados de navegação, e sua diferença do lazy loading se dá que voce precisa deixar explicito em codigo que voce quer carregar isso logo apos a primeira query.

Exemplo:

```csharp
var blog = dbContext.Blogs.First();

// Carrega explicitamente a coleção de posts relacionados ao blog
dbContext.Entry(blog)
    .Collection(b => b.Posts)
    .Load();

// Agora, os posts estão disponíveis para uso
foreach (var post in blog.Posts)
{
    Console.WriteLine(post.Titulo);
}
```

No exemplo acima, veja que é necessário fazer a chamada de .Load() e explicitar exatamente o tipo de elemento que voce quer receber, e diferente do eager loading, na linha 12 não foi feito a requesicao completa no banco, portanto para cada blog é novamente feito uma chamada no banco para carregar todos os posts do blog referido, então se tiver 1000 blogs, serão feitas 1000 chamadas novamente no banco.

Ou seja, voce troca overload em memoria para overload em network, IO e conexoes penduradas na pool.

---

