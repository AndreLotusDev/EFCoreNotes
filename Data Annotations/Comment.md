---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 9:11:59 pm
date modified: quarta-feira, novembro 13º 2024, 9:15:15 pm
---
É possível documentar uma tabela utilizando o fluent API, todavia agora é possível também documentar uma classe dentro dela mesmo, não havendo necessidade de criar um arquivo de configuração.

Exemplo: 

```cs
[Comment("Tabela utilizada para guardar todas as notas fiscais da empresa inteira, não se restringindo somente a um setor")]
public class NotaFiscal {
public DateTime Gerada {get;set;}
public decimal Valor {get;set;}
}
```