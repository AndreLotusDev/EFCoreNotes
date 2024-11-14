---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 9:06:39 pm
date modified: quarta-feira, novembro 13º 2024, 9:12:00 pm
---
É possível configurar o INDEX sem a necessidade de usar o Fluent API usando o atributo Index, o atributo Index recebe um array de propriedades ao qual quando especificado configurado no lado de banco de dados um INDEX de chave unica ou de multiplas colunas (multivalorado).

Exemplo:

```cs
using Microsoft.EntityFremeworkCore;

[Table("Pessoa")]
[Index(nameof(CPF), nameof(Id), IsUnique = true)]
public class Pessoa  {
	public int Id;
	public string CPF;

	public string Nome;
}
```