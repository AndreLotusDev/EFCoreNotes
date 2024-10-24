---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 2:10:11 pm
date modified: terça-feira, outubro 22º 2024, 11:55:39 pm
---
# Comandos EF Core

get-help entityframework

add-migration "Nome da migracao" // Cria uma nova migração
script-migration // Gera o script da migração

---

- dotnet ef migrations add "Nome da migracao" 
	- Cria uma nova migração

- dotnet ef migrations script -p ../MyProject.csproj -o script.sql 
	- Gera o script da migração

- dotnet ef migrations script -i -o script.sql 
	- Gera o script da migração com o comando de execução

- dotnet ef database update
	- Atualiza o banco de dados
- dotnet ef database update 0 
	- Atualiza o banco de dados para a migração 0
- dotnet ef database update UmaMigracaoAnterior
	- Remove a migracao atual e volta para migracao antiga
- dotnet ef migrations remove
	- Remove a última migração
- dotnet ef migrations list --context ApplicationContext
	- Lista todas as migracoes, inclusive as quais estao pendente e prontas para serem aplicadas

---

- dotnet add package Microsoft.Extensions.Logging.Console --version 3.1.5 
	- permite trackear os logs que o ef core vai gerando ao longo do runtime da aplicação

---

