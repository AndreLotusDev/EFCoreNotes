---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 5:22:40 pm
date modified: quarta-feira, novembro 20º 2024, 7:22:01 pm
---
Para gerar uma migração no EF Core, você pode fazer o seguinte:

```bash
dotnet ef migrations add NomeDaMigracao
```

Com isso, o EF Core irá buscar o AppDbContext, ver as diferenças e comparar com o Snapshot, se tiver alguma diferença, ele irá gerar um arquivo com metodos Up e Down, o Up será para executar a migração, o método Down será para dar rollback da migração caso seja necessário.

---

É possível também depois de gerar a migração gerar o arquivo em forma de SQL para poder atualizar o banco de dados.

```bash
dotnet ef migrations script
```

Há também a possibilidade de gerar esse script, só que de forma idempotente, ou seja, se você rodar ele inúmeras vezes no final ele irá produzir o mesmo resultado.

```bash
dotnet ef migrations script --idempotent
```

---

É possível realizar desfeitas de migracao usando o comando dotnet ef database updated.

Se você tem duas migrações. Ao qual a primeira se chama (CRIANDO BANCO DE DADOS) e a segunda (ATUALIZANDO BANCO DE DADOS).

E o seu banco está tualmente na ATUALIZANDO BANCO DE DADOS, quando você executar o comando.

dotnet ef database update CRIANDO BANCO DE DADOS, ele irá simplesmente reverter a segunda migração.

PS: Todavia, reverter uma migração dessa forma não exclui a segunda migração...

Para remover essa migração que agora ficou pendente, basta executar o comando dotnet ef migrations remove.