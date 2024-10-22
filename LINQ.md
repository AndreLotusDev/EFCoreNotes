---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 3:22:23 pm
date modified: terça-feira, outubro 22º 2024, 3:35:22 pm
---
# Tipos de LINQ

No C# temos dois jeitos de utilizar o LINQ.


1 - Sintaxe de consulta (Query Sintax)

Geralmente utilizada para simular queries no banco de dados, muito semelhante a sintaxe SQL.

Gera uma leitura mais intuitiva para quem está acostumado/familiarizado com SQL queries.

```csharp
var query = from p in pessoas
            where p.Idade > 18
            select p;
```

2 - Sintaxe de método (Method Sintax)

Nesse modo de utilizar LINQ, as chamadas são encadeadas e chamadas por metodos de extensao.

Geralmente é muito útil onde há cenários onde a consulta de sintaxe pode não ser tão expressiva.

```csharp
var query = pessoas.Where(p => p.Idade > 18);
```
