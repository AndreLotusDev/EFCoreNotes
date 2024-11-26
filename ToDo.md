---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 3:10:54 pm
date modified: quarta-feira, novembro 20º 2024, 7:54:04 pm
---
- Instalar uma ILoggerFactory dentro do AppDbContext para logar todos os comandos no console do desenvolvedor pelo menos no ambiente de desenvolvimento de DEV e STG.
- Ver a problematica do DbContext e AsNoTracking e algumas coisas que guardam o tracking da entidade em memoria.
- Implementar no DBContext um metodo que detecta propriedade não configuradas.
- Implementar retry on failure para garantir resiliencia no banco de dados.
- Alterar o nome da tabela de historico para acomodar o padrao do sistema.
- Estudar as novas funcionalidades do EF Core, Bulk Insert, Bulk Update, SQL na mao e afins.
- Criar um health checker do banco de dados para validar se ele está de pe periodicamente.
- Testar se a aplicação fica abrindo e fechando conexão indevidamente.
- Fazer uma split query
- Adicionar TAGS nas queries para ajudar na depuracao do lado do banco.
- Instalar SQL Server Profiler ou algo parecido e alternativo so que para o postgreSQL.
- Criar um interceptor para logar melhor o que ocorrer no banco de dados, principalmente nas operações de alterar dados.
- Usar NO LOCK nos ambientes onde a leitura não será ou dificilmente será impactada por leituras sujas,
- Usar a ferramenta diagnostic tools e de memory usage para comparar diferentes cenários de uso do ef core.
- Configurar por padrão no ef core para ele usar o NoTrackingWithIdentityResolution.
- Ter uma operação de console falando quanto cada QUERY custou em MB no sistema.
- Criar uma aplicação multi tenant. Usando as tres diferentes tipos de estrategia.