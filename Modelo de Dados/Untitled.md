---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 11:59:33 am
date modified: quarta-feira, novembro 13º 2024, 7:22:46 pm
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