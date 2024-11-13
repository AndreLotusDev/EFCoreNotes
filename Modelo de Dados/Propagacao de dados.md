---
aliases: 
tags: 
date created: segunda-feira, novembro 11º 2024, 1:47:44 pm
date modified: segunda-feira, novembro 11º 2024, 1:55:09 pm
---
É possível criar seeds para valores estaticos e que não mudam por meio do comando .HasData();

exemplo:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>().HasData(
        new Blog { BlogId = 1, Url = "http://sample.com" },
        new Blog { BlogId = 2, Url = "http://sample2.com" }
    );
}
```

Para que o comando funcione é necessário que a chave primária seja configurada para auto incremento, caso contrário, o comando não funcionará.
