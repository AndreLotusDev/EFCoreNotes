---
aliases: 
tags: 
date created: terça-feira, novembro 12º 2024, 3:33:02 pm
date modified: quarta-feira, novembro 13º 2024, 11:16:00 am
---
Owned Types é quando isolamos propriedades e valores em uma classe separada, essa classe separada podemos reutilizar em diversos lugares, em contraste com o OOP o owned type não irá configurar uma FK para outra tabela, so ira indicar que se uma classe tem outra classe é meramente por pura organizacao, os fields da classe filha ainda irão persistir na classe pai.

Exemplo:

```cs
public class Endereco
{
    public string Rua { get; set; }
    public string Cidade { get; set; }
    public string Estado { get; set; }
    public string CEP { get; set; }
}

public class Cliente
{
    public int ClienteId { get; set; }
    public string Nome { get; set; }
    public Endereco Endereco { get; set; }
}
```

No DbContext:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Cliente>()
        .OwnsOne(c => c.Endereco);
}
```

No final, a tabela cliente terá também as colunas Rua, Cidade, Estado e CEP.