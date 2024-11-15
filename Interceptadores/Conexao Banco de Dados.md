---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 1:05:39 am
date modified: sexta-feira, novembro 15º 2024, 1:19:58 am
---
Exemplo de conexão com o banco de dados sendo interceptada e logano momento que acontece a conexão.

```cs
using System;
using Microsoft.EntityFrameworkCore.Diagnostics;
using System.Data.Common;
using Microsoft.Extensions.Logging;

public class ConnectionLoggingInterceptor : DbConnectionInterceptor
{
    private readonly ILogger<ConnectionLoggingInterceptor> _logger;

    public ConnectionLoggingInterceptor(ILogger<ConnectionLoggingInterceptor> logger)
    {
        _logger = logger;
    }

    public override InterceptionResult ConnectionOpening(
        DbConnection connection, 
        ConnectionEventData eventData, 
        InterceptionResult result)
    {
        _logger.LogInformation("Iniciando conexão com o banco de dados.");
        _logger.LogInformation("String de Conexão: {ConnectionString}", connection.ConnectionString);
        _logger.LogInformation("Data e Hora: {Time}", DateTime.Now);

        return base.ConnectionOpening(connection, eventData, result);
    }
}
```