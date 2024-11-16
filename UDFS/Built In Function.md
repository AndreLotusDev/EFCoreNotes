---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 11:46:19 pm
date modified: sexta-feira, novembro 15º 2024, 11:58:00 pm
---
Chamado também de função incorporada.

Uma built in function é nada menos que uma função já incorporada nativamente pelo seu banco de dados.

Cada banco de dados possui seu conjunto de funções nativas.

Por isso é importante ler a documentação de cada banco de dados separadamente, o que um banco suporta provavelmente o outro banco não suporta.

Por exemplo, o SQL Server possui sua documentação hospedada no site docs.microsoft.com.

---

O EF Core também possui suporte para mapear uma função do seu banco de dados para o código. Em muitos casos a maioria das funções em LINQ e funções padrões do NET já são traduzidas para seu banco, mas algumas funções pode requerer mapeamento manual.

Exemplo do mapeamento da função LEFT no ApplicationContext:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.HasDbFunction(() => EF.Functions.Left(default(string), default(int)));
}
```

Ou também usando o o data annotation DbFunction:

```cs
[DbFunction(name: "LEFT", IsBuiltIn = true)]
public static string Left(string value, int length) {
    throw new NotImplementedException();
}
```

PS: Mesmo com o throw new NotImplementedException, como temos o data annotation o sistema executa corretamente a função do lado do banco sem gerar de fato uma exceção.
