---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 11:32:29 am
date modified: quarta-feira, novembro 13º 2024, 11:51:00 am
---
É a configuração de tabela onde temos uma tabela forte e outra tabela fraca, exemplo:

"Uma pessoa tem muitos endereços", isso significa que a tabela forte será pessoa e a tabela fraca será endereços, onde a tabela endereço é a dependente do relacionamento.

Exemplo:

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
    public int PessoaId { get; set; }
    public string Rua { get; set; }
    public string Cidade { get; set; }
    public string Estado { get; set; }
    public string CEP { get; set; }
    public virtual Pessoa Pessoa { get; set; }
}
```