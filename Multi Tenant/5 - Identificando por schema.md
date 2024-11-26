---
aliases: 
tags: 
date created: terça-feira, novembro 26º 2024, 2:44:40 pm
date modified: terça-feira, novembro 26º 2024, 2:46:10 pm
---
Exemplo:

```cs
public class StrategySchemaInterceptor : DbCommandInterceptor {
	private readonly TenantData _tenantData;

	public StrategySchemaInterceptor(TenantData tenantData) {
    _tenantData = tenantData;
  }

	public override InterceptionResult<DbDataReader> ReaderExecuting(DbCommand command, CommandEventData eventData, InterceptionResult<DbDataReader> result) {
	
    command.CommandText = command.CommandText.Replace("{{schema}}", _tenantData.Schema);
    return result;
  }
}
```

Ou seja, criamos um interceptador, ao qual quando utilizado ele vai repor o schema de acordo com o usuário e seu schema.