---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 2:31:10 pm
date modified: terça-feira, novembro 12º 2024, 3:20:34 pm
---
É possível criar conversores para que possamos usar em mais de um lugar, muito útil para quando queremos padronizar as coisas no banco de dados.

Exemplo, um conversor monetário, assim toda vez que precisamos usar uma coluna do tipo moeda podemos utilizar isso.

```cs
public class MoneyConverter : IValueConverter<Money, string>
{
    public string ConvertToProvider(Money value)
    {
        // Lógica para formatar o valor monetário como uma string
        return value.ToString("C");
    }

    public Money ConvertFromProvider(string value)
    {
        // Lógica para converter a string de volta para um objeto Money
        return Money.Parse(value);
    }
}
```