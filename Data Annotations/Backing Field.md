---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 9:15:15 pm
date modified: quarta-feira, novembro 13º 2024, 9:20:42 pm
---
Tem a mesma usabilidade que no fluente API do backing field [[Area/Programming/NET/EFCore/Modelo de Dados/Backing Field|Backing Field]], todavia sendo possível agora de se utilizar dentro de uma data annotation.

```cs
using System.ComponentModel.DataAnnotations;

public class Pessoa
{
	private string _cpf;
	
	public int Id {get;set;}
	public void SetCPF(string cpf) {
		if(string.IsNullOrEmpty(cpf)) {
			throw new System.Exception("CPF Invalido");
		}

		_cpf = cpf;
	}

	[BackingField(nameof(_cpf))]
	public string CPF => _cpf;
	public string GetCPF() => _cpf;
}
```

