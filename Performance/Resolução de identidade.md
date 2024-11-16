---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 4:22:49 pm
date modified: sábado, novembro 16º 2024, 4:50:16 pm
---
Essa funcionalidade permite a redução da utilização de memória no EF Core.

Essa funcionalidade vem com o proposito de descobrir por exemplo, temos duas tabelas, a tabela FUNCIONARIO e tabela DEPARTAMENTO, ao qual vários FUNCIONARIO podem estar no mesmo DEPARTAMENTO, quando fazemos a seguinte QUERY no EF CORE:

```csharp
var funcionarios = context.Funcionarios.Include(f => f.Departamento).ToList();
```

O que ele irá fazer, se for AsNoTracking é trazer o DEPARTAMENTO de cada FUNCIONARIO, e se tivermos 1000 FUNCIONARIOS, ele irá trazer 1000 DEPARTAMENTOS, o que pode ser um problema de memória, pois ele irá trazer todos os DEPARTAMENTOS para a memória, mesmo que o DEPARTAMENTO seja o mesmo.

E ainda pior, se caso esse INCLUDE tiver uma coluna de arquivo binário, por exemplo, o que irá trazer um grande volume de dados para a memória.

Para sanar esse problema, podemos então utilizar a resolução de identidade, que irá trazer o mesmo DEPARTAMENTO para a memória, mesmo que ele seja referenciado por vários FUNCIONARIOS.

Para isso, basta adicionar a seguinte linha de código no método OnConfiguring do AppDbContext:

```csharp
optionsBuilder.UseQueryTrackingBehavior(QueryTrackingBehavior.NoTrackingWithIdentityResolution);
```

Ou:

```cs
var query = context.Funcionarios.Include(f => f.Departamento).AsNoTrackingWithIdentityResolution().ToList();
```


---

PS: Essa funcionalidade foi introduzida no EF Core 5.0.

TO DO:

Utilizar a ferramenta de diagnostico, principalmente a aba do memory usage.

![[Pasted image 20241116162814.png]]

![[Pasted image 20241116162823.png]]