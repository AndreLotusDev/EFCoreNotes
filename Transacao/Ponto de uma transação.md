---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 2:14:39 am
date modified: sexta-feira, novembro 15º 2024, 2:23:47 am
---
É possível utilizar o EF Core criar pontos de checkpoint de uma transação, sendo possível a posteriori re utilizar esse estado da transação para retornar e continuar a operação.

Geralmente isso vai ser utilizado em cenários complexos.

Pode ser útil onde há cenários complexos e com grandes volumes de dados, onde se algo ocorrer de errado ele não deveria invalidar uma transação por inteiro.

Exemplo: Você pode criar checkpoints, se um falhar por algum motivo, como por exemplo falha de network re tentar processar novamente.

Exemplo:
- Atualiza o estoque de produtos
- Registra uma venda
- Processa o pagamento

```cs
using var transaction = context.Database.BeginTransaction();

try
{
    // Atualiza o estoque
    await UpdateStockAsync();
    await context.SaveChangesAsync();

    // Cria um savepoint após atualizar o estoque
    await transaction.CreateSavepointAsync("AfterStockUpdate");

    // Registra a venda
    await RegisterSaleAsync();
    await context.SaveChangesAsync();

    // Cria um savepoint após registrar a venda
    await transaction.CreateSavepointAsync("AfterSaleRegistration");

    // Processa o pagamento
    await ProcessPaymentAsync();
    await context.SaveChangesAsync();

    // Comita a transação completa
    await transaction.CommitAsync();
}
catch (PaymentException)
{
    // Se o processamento do pagamento falhar, reverte para após o registro da venda
    await transaction.RollbackToSavepointAsync("AfterSaleRegistration");
    await transaction.CommitAsync();
}
catch (Exception)
{
    // Para outros erros, faz rollback total
    await transaction.RollbackAsync();
    throw;
}
```

PS:

- Nem todo banco de dados oferece suporte a savepoints, é sempre importante verificar se seu banco de dados oferece suporte para tal funcionalidade.
- Essa feature pode adicionar muita complexidade ao seu código, sendo portanto importante verificar se sua complexidade não supera os custos de manter tal funcionalidade.
- Performance: Criar savepoints pode onerar a performance do banco de dados, ainda mais em situações com grandes volumes de dados.