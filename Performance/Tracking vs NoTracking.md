---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 4:11:49 pm
date modified: sábado, novembro 16º 2024, 4:22:01 pm
---
Tracking (consulta rastreada): Ao você trazer uma entidade para o backend em qualquer camada dele você pode alterar as propriedades dele, e quando você executar o SaveChanges elas serão persistidas automaticamente.

Para cada registro que ele trazer do banco de dados ele irá criar um registro.

Ou seja, não há a necessidade de trazer o metodo update, se foi utilizado o metodo Tracking, o EF Core por definição saberá quais entidades sofreram alterações.

![[Pasted image 20241116161759.png]]

---

As No Tracking (consulta não rastreada): Utilizamos quando (geralmente) queremos trazer algo para o FRONT END ou para o BACK END, todavia de forma de somente leitura, não iremos operar nenhuma alteração no estado da entidade, tanto é que se você realizar operações de alteração e mandar salvar essa entidade o EF Core irá produzir uma exceção. 

Exemplo de um código usando AsNoTracking():

```cs
using var db = new ApplicationContext();

var cursos = db.Cursos
	.AsNoTracking()
	.Where(w => w.Id < 10)
	.ToList();
```