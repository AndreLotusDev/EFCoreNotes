---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 12:57:34 am
date modified: sexta-feira, novembro 15º 2024, 1:05:39 am
---
Como explicado previamente, podemos usar interceptadores em muitas fases da comunicação com o banco de dados, sendo possível então configurar que nas queries podemos utilizar o NO LOCK garantindo maior performance na QUERY, mas como tudo na vida é feito de trade offs, isso pode gerar retornos de leitura com dados sujos e incosistentes, ou seja, voce troca qualidade da leitura por performance.

Exemplo:

```cs
public class Interceptador : DbCommandInterceptor {
	private static readonly Regex _tableRegex = new Regext(@"?<tableAlias>FROM +(\[.*\]\.)?(\[,*\]) AS (\[.*\])(?! WITH \(NOLOCK\))", RegexOptions.Multiline | RegexOptions.IgnoreCase | RegexOptions.Compiled);

	public override InterceptionResult<DbDataReader> ReaderExecuting(DbCommand command, CommandExecutingContext<DbDataReader> context, InterceptionResult<DbDataReader> result) {
	  UsarNoLock(command);
	  return base.ReaderExecuting(command, context, result);
	}


	private static void UsarNoLock(DbCommand command) {
		if(!command.CommadText.Contains("WITH (NOLOCK)")) {
			command.CommandText = _tableRegex.Replace(command.CommandText, "${tableAlias} WITH (NOLOCK)");
		}
	}
}
```