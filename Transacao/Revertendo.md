---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 2:06:32 am
date modified: sexta-feira, novembro 15º 2024, 2:12:28 am
---
Podemos quando configuramos uma transação manualmente embrulhar ela em um try catch, fazendo assim que quando é estourado uma exceção durante uma tentativa de alteração do banco de dados executar o rollback e por fim mantendo o banco de dados integro.

```cs
await using var transaction = await context.Database.BeginTransactionAsync();

try
{
    // Operação 1
    var cliente = new Cliente { Nome = "Maria" };
    await context.Clientes.AddAsync(cliente);
    await context.SaveChangesAsync();

    // Operação 2
    var pedido = new Pedido { ClienteId = cliente.Id, Valor = 200 };
    await context.Pedidos.AddAsync(pedido);
    await context.SaveChangesAsync();

    // Confirma a transação
    await transaction.CommitAsync();
}
catch (Exception ex)
{
    // Desfaz as alterações
    await transaction.RollbackAsync();
    // Opcional: log da exceção
    throw;
}
```