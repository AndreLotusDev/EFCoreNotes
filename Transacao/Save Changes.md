---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 2:02:51 am
date modified: sexta-feira, novembro 15º 2024, 2:04:52 am
---
O EF Core permite que a gente gerencie manualmente nossas transações, essas transações começam com a chamada da função context.Database.BeginTransaction(); e terminam com transaction.Commit();

Todavia deve se atentar que o .Commit(); não irá salvar os dados sozinho e automaticamente.

Para gerar os comandos de DELTE, INSERT e UPDATE ainda se faz necessário o uso do comando .SaveChanges(); sem ele e chamando somente o .Commit(); a transação irá terminar e nenhum dado será inserido no banco de dados.

Exemplo:

```cs
using var transaction = context.Database.BeginTransaction();

var novoCliente = new Cliente { Nome = "João" };
context.Clientes.Add(novoCliente);

// Até aqui, 'novoCliente' está apenas no contexto do EF Core.

context.SaveChanges(); // Envia o INSERT para o banco de dados dentro da transação.

transaction.Commit(); // Confirma a transação, tornando a inserção permanente.

// Sem 'SaveChanges()', o 'Commit()' não teria inserido 'novoCliente' no banco de dados.
```