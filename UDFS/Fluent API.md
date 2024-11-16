---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 12:05:55 am
date modified: sábado, novembro 16º 2024, 12:09:50 am
---
É possível registrar funções usando o Fluent API também, não só restringindo somente a Data Annotations.

Exemplo:

```cs
public static class MinhasFuncoes {
	[DbFunction(name: "LEFT", IsBuiltIn = true)]
	public static string Left(string dados, int quantidade) {
		throw new NotImplementedException();
	}
	public static void RegistrarFuncoes(ModelBuilder builder) {
		var funcoes = typeof(MinhasFuncoes).GetMethods().Where(m => m.GetCustomAttribute<DbFunctionAttribute>() != null);

		foreach (var funcao in funcoes) {
		      builder.HasDbFunction(funcao);
    }
	}
}
```

```cs
public class ApplicationContext: DbContext {
	    public DbSet<User> Users { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder) {
        modelBuilder.Entity<User>().Property(u => u.Name).IsRequired();

	    modelBuilder.HasDbFunction(() => MinhasFuncoes.Left(default(string), default(int)));
    }

	protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder) {
        optionsBuilder.UseSqlServer("Server=localhost;Database=FluentAPI;Trusted_Connection=True;");
    }

	
}
```