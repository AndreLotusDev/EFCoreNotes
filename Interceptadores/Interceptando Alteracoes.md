---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 1:22:09 am
date modified: sexta-feira, novembro 15º 2024, 1:25:32 am
---
É possível também interceptar comandos que a priori irão alterar, adicionar, deletar registros no banco de dados.

Exemplo:

```cs
public class Interceptador : SaveChangesInterceptor {
	public override InterceptionResult<int> SavingChanges(
		DbContextEventData eventData,
		InterceptionResult<int> result
	)
	{
		Console.WriteLine(eventData.Context.ChangeTracker.DebugView.LongView);
		
	    return result;
	}
}
```