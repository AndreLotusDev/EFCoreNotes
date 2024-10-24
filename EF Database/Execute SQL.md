---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 8:01:31 pm
date modified: terça-feira, outubro 22º 2024, 8:10:30 pm
---
É possível criar comandos no banco de dados sem criar instancia de rastreamento.

Isso é possivel criando queries por meio de comandos.

Exemplo:

using(var cmd = db.Database.GetDbConnection().CreateCommand()) {
	cmd.CommandText = "SELECT 1";
	cmd.ExecuteNonQuery();
}

---

No EF Core temos suporte além disso, temos o suporte de outros meios, tais quais:

db.Database.ExecuteSqlRaw("");

Lembrando que nesse modo, não existe sanitização de string, se fazendo necessário fazer isso de forma manual.

int userId = 1; 
db.Database.ExecuteSqlRaw("DELETE FROM Users WHERE Id = {0}", userId);

Essa opção é mais segura que a primeira pois evita ataques de SQL Injection se manuseado da maneira correta.

---

Ha também a opção pelo comando ExecuteSqlInterpolated("");

db.Database.ExecuteSqlInterpolated("");

Desse jeito, é o jeito mais moderno, onde o framework se encarrega de fazer a interpolação de forma automática para voce e sanitizar se necessário. Enquanto da segunda maneira isso só acontece quando você passa os dados como parametros.