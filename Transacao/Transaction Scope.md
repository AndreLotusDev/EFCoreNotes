---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 2:27:20 am
date modified: sexta-feira, novembro 15º 2024, 2:42:17 am
---
O Transaction Scope é uma classe que faz transações com base em um bloco de código, ela possui própria infraestrutura para gerenciar as transações automaticamente.

Sendo assim, o TransactionScope reduz a complexidade do código e, portanto, é muito utilizado e indicado para o desenvolvimento de software.

O TransactionScope permite que podemos desfazer transações de multiplos contextos inicializados ao mesmo tempo, vamos supor que você tenha separado seu banco por contextos, e então você pode utilizar da seguinte forma.

Outro ponto a se detalhar é que transactionscope facilita o codigo para controlar transações, você não precisa explicitamente abrir uma transação, commitar or dar rollback para cada contexto da conexão.

```cs
using (var scope = new TransactionScope())
{
    using (var context1 = new MeuDbContext())
    {
        // Operações no contexto1
        context1.SaveChanges();
    }

    using (var context2 = new OutroDbContext())
    {
        // Operações no contexto2
        context2.SaveChanges();
    }

    scope.Complete(); // Confirma a transação
}
```

PS: Não é possível utilizar o TransactionScope para fazer transação através de diversos bancos, para isso é necessário utilizar o padrão SAGA.