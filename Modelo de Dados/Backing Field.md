---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 7:38:02 pm
date modified: quarta-feira, novembro 13º 2024, 7:44:50 pm
---
Essa feature no EF Core é muito útil para quem curte praticar DDD e precisa criar uma classe rica de dominio.

Exemplo usando o DbContext or OnConfigure:

```cs
public class Pessoa 
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public string Sobrenome { get; set; }
    public string NomeCompleto => $"{Nome} {Sobrenome}";
    private string _cpf;

    public string SetCfp(string cpf)
    {
        if (string.IsNullOrEmpty(cpf))
            throw new ArgumentException("Cpf não pode ser nulo ou vazio");

        _cpf = cpf;
    }

	public string GetCpf()
    {
        return _cpf;
    }

}

public class Context : DbContext
{
    public DbSet<Pessoa> Pessoas { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Pessoa>()
            .Property(p => p.NomeCompleto)
            .HasField("_nomeCompleto")
            .UsePropertyAccessMode(PropertyAccessMode.Field);

        modelBuilder.Entity<Pessoa>().Property("_cpf").HasColumnName("Cpf");
    
    }
}
```