---
aliases: 
tags: 
date created: terça-feira, novembro 26º 2024, 4:26:30 pm
date modified: terça-feira, novembro 26º 2024, 4:30:43 pm
---
O repository pattern é um padrão de desenvolvimento que embrulha uma entidade + suas funções especificas + acesso ao banco de dados tudo ao mesmo tempo.

Basicamente, é um objeto que faz o isolamento das entidades do domínio de seu código que faz acesso à dados.

Prós
- Um único ponto de acesso à dados
- Encapsulamento da lógica de acesso à dados
- SPOF (Ponto único de falha)

Contras
	Se sua aplicação é uma aplicação simples, talvez não seja necessário tamanha complexidade.

![[Pasted image 20241126162723.png]]

---

