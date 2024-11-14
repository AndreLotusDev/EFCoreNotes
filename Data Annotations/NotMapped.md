---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 8:54:54 pm
date modified: quarta-feira, novembro 13º 2024, 8:57:02 pm
---
O atributo not mapped é utilizado para quando queremos que uma propriedade do banco não seja mapeada para a classe, ou caso um field da clase você queira que não vire alguma coluna no banco.

Exemplo:

```cs
public class Pessoa
{
    public int Id { get; set; }
    public string Nome { get; set; }
    [NotMapped]
    public string Senha { get; set; }
}
```