---
aliases: 
tags: 
date created: quarta-feira, novembro 20º 2024, 7:40:40 pm
date modified: quarta-feira, novembro 20º 2024, 7:50:00 pm
---
Temos 3 jeitos de configurar estrategia multi tenant (na verdade mais do que isso).

1 - Banco de dados (cada usuário tem um banco de dados diferente).

![[Pasted image 20241120194307.png]]

Podemos configurar na web api que cada usuário tem seu banco de dados de forma diferente e apontar para a localização do banco de dados, o tipo de provedor e suas credenciais.

Podemos configurar que cada usuário tenha um subdominio dentro do dominio, assim permitindo identificar qual é o banco de dados a ser utilizado por X usuário.

Essa forma é mais adequada e mais fácil para estar em conformidade com a LGPD, tendo em vista que estamos segregando cada aplicação para ter seu banco de dados isolado, não permitindo assim vazamento de dados tão facilmente.

TLDR: Temos vários clientes e usuários, vários banco de dados, todavia somente uma aplicação que faz esse controle fino.

---

2 - Schema

Nesse modelo segregamos os dados de cada grupo de usuários por Schema, então CLIENTE 1 usa schema A, CLIENTE 2 usa schema B.

Nessa utilizamos uma aplicação e um banco somente, alternando somente o schema por cliente.

![[Pasted image 20241120194634.png]]

---

3 - Identificador na tabela

![[Pasted image 20241120194836.png]]

Todos os clientes usam o mesmo banco de dados, a mesma aplicação, o que permite a segregação dos dados é que em todas as tabelas teremos uma coluna identificando de quem é a proveniencia dos dados...

PS: É o mais fácil de dar manutenção e de gerenciar. Por mais que seja a mais fácil de se implementar, pode por fim sendo a mais difícil para se adequar na lei da LGPD.