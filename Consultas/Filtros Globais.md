---
aliases: 
tags: 
date created: quinta-feira, outubro 24º 2024, 12:46:32 am
date modified: quinta-feira, outubro 24º 2024, 12:51:28 am
---
Essa feature foi introduzida no ef core na versão 2.0.

É muito útil para por exemplo configurar um soft delete, onde na maioria das tabelas vai ter uma coluna status falando se uma row esta "deletada" ou não.

Exemplo:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<BaseEntity>().HasQueryFilter(p => p.Ativo);
}
```

Nesse código acima por exemplo, somente iremos trazer pras queries somente items em todas as tabelas que herdam do BaseEntity somente items que nao foram deletados de forma logica.

---

Ha tambem a possibilidade de ignorar em algumas queries esses filtros globais:

```csharp
var todosOsProdutos = context.Produtos.IgnoreQueryFilters().ToList();
```

Com essa query acima por exemplo, iremos trazer todos os produtos, inclusive aqueles que já foram deletados.