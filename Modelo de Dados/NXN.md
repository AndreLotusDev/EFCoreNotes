---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 11:49:59 am
date modified: quarta-feira, novembro 13º 2024, 7:38:02 pm
---
Geralmente a configuração muitos para muitos é utilizada quando temos duas tabelas ao quais são igualmente uma dependente da outra, em contraste de um para muitos onde temos uma tabela forte e uma tabela fraca.

No EF Core podemos configurar da seguinte maneira:

```cs
public class Pessoa
{
    public int PessoaId { get; set; }
    public string Nome { get; set; }
    public virtual ICollection<PessoaEndereco> PessoaEnderecos { get; } = new();
}


public class Endereco
{
    public int EnderecoId { get; set; }
    public string Rua { get; set; }
    public string Cidade { get; set; }
    public string Estado { get; set; }
    public string CEP { get; set; }
    public virtual ICollection<PessoaEndereco> PessoaEnderecos { get; } = new();
}

public class PessoaEndereco
{
    public int PessoaId { get; set; }
    public Pessoa Pessoa { get; set; }
    public int EnderecoId { get; set; }
    public Endereco Endereco { get; set; }
}
```

No caso temos a tabela Pessoa e Endereco, e como as duas sao igualmente fortes, criamos uma tabela intermediaria chamada PessoaEndereco para linkar as duas.

---

Também é possível fazer isso sem criar a tabela especifica, somente usando o DbContext.

```cs
public class Pessoa
{
    public int PessoaId { get; set; }
    public string Nome { get; set; }
    public virtual ICollection<Endereco> Enderecos { get; } = new();
}

public class Endereco
{
    public int EnderecoId { get; set; }
    public string Rua { get; set; }
    public string Cidade { get; set; }
    public string Estado { get; set; }
    public string CEP { get; set; }
    public virtual ICollection<Pessoa> Pessoas { get; } = new();
}

protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Pessoa>()
	    .HasMany(p => p.Enderecos)
	    .WithMany(e => e.Pessoas)
	    .UsingEntity(p => p.ToTble("PessoasEnderecos"));
}
```
