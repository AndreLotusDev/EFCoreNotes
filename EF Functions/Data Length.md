---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:05:11 am
date modified: sexta-feira, novembro 15º 2024, 12:10:47 am
---
O DataLength é uma função no banco de dados que nos permite verificar o tamanho em bytes de uma coluna ou expressão, temos também algo muito semelhante chamado LEN, que retorna o número de caracteres de uma coluna do tipo string.

Exemplo: 

```cs
var resultados = db.Query<int>("SELECT DataLength(Nome) FROM Pessoas");
```

E assim conseguimos verificar qual o nome mais longo e ao mesmo tempo mais pesado dentro do nosso banco de dados.