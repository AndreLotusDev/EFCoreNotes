---
aliases: 
tags: 
date created: quarta-feira, outubro 23º 2024, 12:03:14 am
date modified: quarta-feira, outubro 23º 2024, 11:05:19 pm
---
O eager loading no ef core se baseia em fazer queries já deixando explicito antes de tirar as coisas de memoria o que voce precisa incluir.

Exemplo:

```csharp
var blogs = dbContext.Blogs 
	.Include(b => b.Posts)
	.ThenInclude(p => p.Comments)
	.ToList();
```

No exemplo acima, eu deixo explicito que eu não quero somente os blogs, mas tambem todos os posts e comentarios.

Com isso, por mais que a gente dumpe a memoria em excesso caso tenha muitos resultados, trocamos essa carga de memoria por uma carga de processamento, evitando idas adicionais ao banco que impacta o IO e tempo de resposta total.

---


 