---
aliases: 
tags: 
date created: quinta-feira, outubro 24º 2024, 1:25:54 am
date modified: quinta-feira, novembro 7º 2024, 3:25:30 pm
---
A divisão de consultas basicamente veio para solucionar um problema, e basicamente o problema é quando precisamos carregar dados relacionados.

---

Na construção de algumas queries, produzimos dados repetitivos ao realizar certos tipos de JOINS, isso chamamos de explosão cartesiana, e isso pode onerar e muito a performance do sistema, pois dados repetitivos significam o mesmo dado trafega pela rede de novo e de novo.

![[Pasted image 20241107150007.png]]

Podemos então nessas situações chamar o AsSplitQuery()

Exemplo:

```csharp
var query = _context.Set<Cliente>().AsSplitQuery().Include(x => x.Pedidos).ToList();
```


Ai em vez de ficar replicando o cliente sempre que o pedido é para o mesmo cliente, ele traz somente de uma vez e separa as queries conforme necessidade.

Em consultas projetadas pode ser mais benefico não se utilizar o splitquery ou para consultas com pouco volume de dados.

---

PS: É possível configurar globalmente o splitquery no OnConfiguring do DbContext

```csharp
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    optionsBuilder.UseSqlServer("connectionString", x => x.UseQuerySplittingBehavior(QuerySplittingBehavior.SplitQuery));
}
```

Caso voce configure globalmente, será necessário para queries ao qual você não quer performar o splitquery dar enforce do assinglequery.

```csharp
var query = _context.Set<Cliente>().AsSingleQuery().Include(x => x.Pedidos).ToList();
```

