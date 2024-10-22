---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 2:12:24 am
date modified: terça-feira, outubro 22º 2024, 2:17:49 am
---
Em poucas palavras podemos definir como uma combinação dos padrões Uow e Repository, que contém um conjunto de métodos responsáveis por gravar e ler informações do banco de dados.
O DbContext é classe principal e mais importante que você terá acesso, o objetivo dela é simplificar a interação de sua aplicação com o seu banco de dados.

- Configurar seu modelo de dados
- Gerenciar a conexão com o banco de dados
- Consultar e persistir dados em seu banco
- Fazer toda rastreabilidade de objetos
- Materializar resultado das consultas
- Cache de primeiro nível

OnConfiguring: É usado para informar qual provider será utilizado e informar a string de conexão, logger, serviços customizados e outros.

OnModelCreating: É usado para configurar todo o modelo de dados que serão posteriormente transformados em tabelas e comandos SQL.