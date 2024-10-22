---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 1:58:22 pm
date modified: terça-feira, outubro 22º 2024, 2:41:10 pm
---
A migração é uma das coisas mais importantes do Entity Framework Core, com ela podemos versionar nosso schema de banco.

Assim como temos de forma auditavel as versões que nosso banco de dado foi ao longo do tempo, e podemos reverter e navegar entre as versões.

# O que é necessário para criar uma migração?

É necessário instalar: Microsoft.EntityFrameworkCore.Design.

Opcional, mas necessário se você for usar os comandos pelo nuget package manager: Microsoft.EntityFrameworkCore.Tools.

---

# Estrutura da migracao

Uma migração é composta por 2 métodos:

protected override void Up(MigrationBuilder migrationBuilder) { }

	Esse comando vai ser executado para executar a migracao

protected override void Down(MigrationBuilder migrationBuilder) { }

    Esse comando vai ser executado para desfazer a migração

Observacao: Para cada comando criado de forma manual no UP, é necessário para criar um oposto equivalente no lado do DOWN.

---

# Por que usar o Script SQL?

Bem, pode ser por vários motivos, mas um principal é quando você não tem acesso ao ambiente de produção, ai para isso você pode gerar o script e entregar para o time responsável de executar isso no ambiente de produção.

---

# Notas adicionais

- Os scripts SQL são formados de forma que sempre executado o produto final será idempotente.