---
aliases: 
tags: 
date created: quinta-feira, novembro 14º 2024, 11:54:13 pm
date modified: sexta-feira, novembro 15º 2024, 12:05:08 am
---
A função like é uma função implementada em quase todo banco de dados relacional, ela nos ajuda a pesquisar entre colunas. Permitindo que possamos pesquisar não somente exact cases, mas pesquisar tendo somente metade da informação ou menos da coluna.

Ele é expressado da seguinte maneira:

```cs
EF.Functions.Like(string matchExpression, string pattern);
```

Exemplo:

```cs
var pessoas = await _context.Pessoas
    .Where(p => EF.Functions.Like(p.Nome, "João%"))
    .ToListAsync();
```

Nesse exemplo aqui, iremos retornar todo mundo que começa com João, mas sem especificar o sobrenome, trazendo não somente exact case de João, mas como também qualquer pessoa com sobrenome no banco de dados.

Lembrando que: % => substitui zero ou mais caracteres, enquanto _ substitui somente um caracter.

Por exemplo, podemos procurar nomes com 5 caracteres assim:

```cs
var clientes = contexto.Clientes
    .Where(c => EF.Functions.Like(c.Nome, "_____"))
    .ToList();
```

O contains faz a tarefa de forma parecida, todavia ele sempre faz a pesquisa como se fosse um like '%{pattern}%', ou seja, ele sempre adiciona o % no começo e no final do pattern.

```cs
var pessoas = await _context.Pessoas
    .Where(p => p.Nome.Contains("João"))
    .ToListAsync();
```

Que para SQL vira a seguinte QUERY:

```sql
SELECT * FROM Pessoas WHERE Nome LIKE '%João%'
```

Então por questões de desempenho e uso de índices pode ser interessante usar o Like em vez do Contains. Assim como o LIKE pode permitir consultas mais refinadas.