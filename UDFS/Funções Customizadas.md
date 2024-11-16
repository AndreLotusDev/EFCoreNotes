---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 12:21:06 am
date modified: sábado, novembro 16º 2024, 12:22:51 am
---
É possível também registrar funções customizadas que foram criadas pelo próprio usuário.

```cs
public class AppDbContext : DbContext
{
    // Seus DbSets e configurações

    [DbFunction("TransformFirst100ToUpper", "dbo")]
    public static string TransformFirst100ToUpper(string input)
    {
        // O corpo do método não é importante; ele será executado no banco de dados
        throw new NotImplementedException();
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        // Registre a função UDF
        modelBuilder.HasDbFunction(typeof(AppDbContext).GetMethod(nameof(TransformFirst100ToUpper)))
            .HasName("TransformFirst100ToUpper")
            .HasSchema("dbo");
    }
}
```

Após isso, crie uma migração com o seguinte código SQL:

```cs
migrationBuilder.Sql(@"
CREATE FUNCTION dbo.TransformFirst100ToUpper(@input NVARCHAR(MAX))
RETURNS NVARCHAR(MAX)
AS
BEGIN
    IF @input IS NULL
        RETURN NULL;
    ELSE
        RETURN UPPER(SUBSTRING(@input, 1, 100));
END
");

```

Depois, utilize o metodo implementado na camada de repositório:

```cs
var resultados = context.SeuDbSet
    .Select(x => new
    {
        TextoTransformado = AppDbContext.TransformFirst100ToUpper(x.SeuCampoTexto)
    })
    .ToList();
```