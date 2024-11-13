---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 8:18:04 pm
date modified: quarta-feira, novembro 13º 2024, 8:34:45 pm
---
No EF Core também é possível configurar as tabelas como TPT (Tabela por tipo) em portugues, ou em ingles Tabela Per Type. Muito parecido com o TBH.

A diferença entre TBH e TPT, é que no TPT é criado uma tabela base, todavia para cada subvariação criamos uma tabela diferente... Enquanto no TBH utilizamos a mesma tabela para tudo.

Em quesito organização o TPT é muito superior, pois permite colunas nulaveis e restricoes, enquanto no TBH isso não é possivel pois é tudo na mesma tabela, e se uma coluna é requerida somente para um tipo não é possível tornar essa coluna requerida e não nulável pois para outros tipos ela nem é utilizada...

Exemplo:

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

No OnModelConfiguring:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    // Mapeia a classe base para a tabela "Pessoas"
    modelBuilder.Entity<Pessoa>()
        .ToTable("Pessoas");

    // Mapeia a classe derivada Aluno para a tabela "Alunos"
    modelBuilder.Entity<Aluno>()
        .ToTable("Alunos");

    // Mapeia a classe derivada Professor para a tabela "Professores"
    modelBuilder.Entity<Professor>()
        .ToTable("Professores");
}
```