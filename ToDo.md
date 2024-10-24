---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 3:10:54 pm
date modified: quinta-feira, outubro 24º 2024, 12:45:29 am
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