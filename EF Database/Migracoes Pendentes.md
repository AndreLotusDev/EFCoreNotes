---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 8:16:15 pm
date modified: terça-feira, outubro 22º 2024, 11:57:15 pm
---
O EF Core oferece suporte a analisar quais migracoes estão pendentes no seu banco de dados.

Codigo exemplo:

```csharp
using System;
using Microsoft.EntityFrameworkCore;

namespace EFGetStarted
{
    public class BloggingContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }
        public DbSet<Post> Posts { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder options)
            => options.UseSqlite("Data Source=blogging.db");
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }
    }

    public class Post
    {
        public int PostId { get; set; }
        public string Title { get; set; }
        public string Content { get; set; }
        public int BlogId { get; set; }
    }

    class Program
    {
        static void Main()
        {
            using (var context = new BloggingContext())
            {
                var pendingMigrations = context.Database.GetPendingMigrations();
                foreach (var migration in pendingMigrations)
                {
                    Console.WriteLine(migration);
                }
            }
        }
    }
}
```

É possível também obter todas as migrações existentes dentro do banco de dados:

```csharp
var migrations = context.Database.GetMigrations();
foreach (var migration in migrations)
{
    Console.WriteLine(migration);
}
```

É também possível dar retrieve somente nas migrações aos quais já foram aplicadas:

```csharp
var appliedMigrations = context.Database.GetAppliedMigrations();
foreach (var migration in appliedMigrations)
{
    Console.WriteLine(migration);
}
```


---

# Notas adicionais

