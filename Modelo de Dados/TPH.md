---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 7:45:41 pm
date modified: quarta-feira, novembro 13º 2024, 8:16:12 pm
---
o EF Core permite configurar quando o banco da suporte o que chamamos de tabela por hierarquia em portugues, ou em ingles Table Per Hierarchy.

Heranca do tipo Pessoa:

```cs
public class Pessoa
{
    public int Id { get; set; }
    public string Nome { get; set; }
}

public class Aluno : Pessoa
{
    public string Matricula { get; set; }
}

public class Professor : Pessoa
{
    public string Disciplina { get; set; }
}
```

Na hora de configurar no dbContext:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Pessoa>()
        .HasDiscriminator<int>("TipoPessoa")
        .HasValue<Pessoa>(3)
        .HasValue<Aluno>(1)
        .HasValue<Professor>(2);
}
```

No final, o que o EF Core irá fazer será criar uma tabela única ao qual vai inserir para os 3 tipos diferentes de pessoa nessa mesma tabela, sendo possível somente de saber e é um ou outro por uma coluna chamada TipoPessoa ao qual recebe valores do tipo inteiro.