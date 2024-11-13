---
aliases: 
tags: 
date created: terça-feira, novembro 12º 2024, 3:20:33 pm
date modified: terça-feira, novembro 12º 2024, 3:33:02 pm
---
Geralmente uma shadow propertie é gerada quando se é encontrado uma relação entre duas classes, todavia essa relação não se encontra uma chave estrangeira implicitamente configurada.

Exemplo, a classe Post tem uma relação de FK para Blog, todavia em nenhum lugar é explicito um BlogID.

```cs
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
    public ICollection<Post> Posts { get; set; }
}

public class Post
{
    public int PostId { get; set; }
    public string Title { get; set; }
    public Blog Blog { get; set; }
}
```

Portanto se faz necessário o acesso pela seguinte codificação.

```cs
var posts = context.Posts .Where(p => EF.Property<int>(p, "BlogId") == blogId) .ToList();
```

TL;DR: Ou seja, mesmo que você não configure adequadamente a FK, o EF Core dara um jeito de configurar para voce do lado do banco de dados, assim evitando maiores problemas.

---