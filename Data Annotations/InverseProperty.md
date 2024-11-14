---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 8:48:34 pm
date modified: quarta-feira, novembro 13º 2024, 8:53:38 pm
---
No EF Core mais recente foi introduzido o chamado inverse property. Geralmente ele é utilizando quando temos um relacionamento entre duas tabelas que ocorrem mais de uma vez.

Exemplo: Um sistema de companhia aerea, eu tenho uma tabela VOO e uma tabela AEROPORTO, eu tenho que para cada VOO eu tenho um AEROPORTO de CHEGADA (FK) e um outro AEROPORTO de SAIDA (FK).

Para isso podemos usar o Inverse Property.

```cs
public class Aeroporto 
{
    public int Id { get; set; }
    public string Nome { get; set; }

	[InverseProperty("AeroportoChegada")]
    public ICollection<Voo> VoosChegada { get; set; }
    [InverseProperty("AeroportoSaida")]
    public ICollection<Voo> VoosSaida { get; set; }
}

public class Voo 
{
    public int Id { get; set; }
    public Aeroporto AeroportoChegada { get; set; }
    public Aeroporto AeroportoSaida { get; set; }
}

```