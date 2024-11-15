---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:13:37 am
date modified: sexta-feira, novembro 15º 2024, 12:16:25 am
---
Geralmente quando usamos uma shadown property é porque queremos esconder uma coluna do banco de dados no nosso modelo de dominio, entao usamos a shadow property.

Todavia mesmo que não conseguimos acessar essa propriedade diretamente conseguimos utilizando o EF.Property.

Exemplo:

```cs
var query = context.Pessoas
    .Where(p => EF.Property<bool>(p, "Ativo") == true)
    .ToList();
```