---
aliases: 
tags: 
date created: quinta-feira, outubro 24º 2024, 12:54:30 am
date modified: quinta-feira, outubro 24º 2024, 1:05:44 am
---
Consultas projetadas é quando fazemos uma query no banco, e só trazemos exatamente as exatas colunas que iremos precisar.

É muito útil quando você interage com vários JOINS e várias tabelas e não quer trafegar pela rede colunas e dados desnecessários e somente quer trazer o necessário.

Exemplo:

```csharp
var clientesAtivos = await context.Clientes
    .Where(c => c.Ativo)
    .Select(c => new { c.Nome, c.Email })
    .ToListAsync();
```

Nessa consulta projetada, temos a tabela cliente, mas como só precisamos somente do nome e email evitamos de trazer outros campos e assim economizando performance, trafego na internet e consumo de memoria na API.

---

