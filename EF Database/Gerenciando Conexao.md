---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 7:52:26 pm
date modified: terça-feira, outubro 22º 2024, 7:56:22 pm
---
O EFCore por costume, dependendo do jeito que a query é feita irá abrir a conexão multiplas vezes, mesmo que se possa fazer com somente uma chamada e uma conexão, é importante ficar atento a isso pois isso pode degradar a performance em locais que ocorrem muitas chamadas.

```csharp
static void GerenciadEstadoDaConexao(bool gerenciarEstadoConexao) {
	using var db = new ApplicationContext();
	var time = Stopwatch.StartNew();
	
	var conexao = db.Database.GetDbConnection();
	  conexao.StateChange += (s, e) => Console.WriteLine($"State: {e.CurrentState}");
	if(gerenciarEstadoConexao) {
	    conexao.Open();
	}

	for (var i = 0; i < 200; i++) {
	    db.Departamentos.AsNoTracking().Any();
	}

	time.Stop();
	var mensagem = $"Tempo: {time.ElapsedMilliseconds}ms";
	
	Console.WriteLine(mensagem);
}
```