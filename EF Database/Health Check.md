---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 7:35:42 pm
date modified: terça-feira, outubro 22º 2024, 7:48:07 pm
---
Podemos usar o metodo do ef core para validar se uma conexão poderá ser feita a posteriori.

var canConnect = db.Database.CanConnect();

Por debaixo dos panos tudo que ele irá fazer será tentar executar o comando SELECT 1 dentro do banco de dados.