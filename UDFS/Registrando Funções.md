---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 11:59:10 pm
date modified: sábado, novembro 16º 2024, 12:05:47 am
---
Quando criamos uma função mapeada do banco de dados, por default se ela é criada no ApplicationContext não irá lançar nenhum erro.

Todavia, se esse mapeamento de funções for feito fora do contexto há a necessidade de registrar essa classe e suas funções dentro do DbContext.

```cs
public static class MinhasFuncoes {
	[DbFunction(name: "LEFT", IsBuiltIn = true)]
	public static string Left(string dados, int quantidade) {
		throw new NotImplementedException();
	}
	public static void RegistrarFuncoes(ModelBuilder builder) {
		var funcoes = typeof(MinhasFuncoes).GetMethods().Where(m => m.GetCustomAttribute<DbFunctionAttribute>() != null);

		foreach (var funcao in funcoes) {
		      builder.HasDbFunction(funcao);
    }
	}
}
```

Ai é so chamar o RegistrarFuncoes dentro do contexto.