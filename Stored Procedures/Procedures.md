---
aliases: 
tags: 
date created: quinta-feira, novembro 7º 2024, 3:32:48 pm
date modified: quinta-feira, novembro 7º 2024, 3:50:55 pm
---
É possível usando EF Core de criar procedures.


```csharp
static void CriarStoredProcedure(){
	var criarDepartamento = @"
    CREATE PROCEDURE CriarDepartamento
      @Nome nvarchar(50)
    AS
    BEGIN
      INSERT INTO Departamentos (Nome)
      VALUES (@Nome)
    END
}
```

---

Depois da procedure criada é possível consumir ela usando o EF Core.

```csharp
using (var context = new Context())
{
    var nome = new SqlParameter("@Nome", "TI");
    context.Database.ExecuteSqlRaw("CriarDepartamento @Nome", nome);
}
```

---

Também é possível criar procedures de consulta.

```csharp
static void ConsultarDepartamento(){
  var consultarDepartamento = @"
    CREATE PROCEDURE ConsultarDepartamento
    AS
    BEGIN
      SELECT * FROM Departamentos
    END
}
```

---

Depois da procedure criada é possível consumir ela usando o EF Core.

```csharp
using (var context = new Context())
{
    var departamentos = context.Departamentos.FromSqlRaw("ConsultarDepartamento").ToList();
}
```

