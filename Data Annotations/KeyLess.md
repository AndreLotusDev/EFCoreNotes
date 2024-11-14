---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 9:21:38 pm
date modified: quarta-feira, novembro 13º 2024, 9:23:59 pm
---
Permite configurar um modelo de dados para uma entidade ao qual não possui ID muito menos uma KEY.

Geralmente usado em tabelas pre definidas, tabelas pre materializadas ou view onde não há necessidade de uma chave.

Exemplo:

```cs
[Keyless]
public class RelatorioFinanceiro {
	public string Descricao {get;set;}
	public decimal Total {get;set;}
	public DateTime Data {get;set;} 
}
```