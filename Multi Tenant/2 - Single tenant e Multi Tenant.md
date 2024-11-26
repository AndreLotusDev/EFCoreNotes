---
aliases: 
tags: 
date created: quarta-feira, novembro 20º 2024, 7:28:06 pm
date modified: quarta-feira, novembro 20º 2024, 7:40:07 pm
---
Single-tenant (inquilino único) tem como objetivo realizar o isolamento tanto de suas aplicações quanto de seus dados.

Ou seja, para cada cliente, um novo banco, uma nova aplicação...

---

Vantagens:

Isso permite uma maior customização, por exemplo, para cada cliente podemos criar em uma infraestrutura diferente:
- Cliente A criamos a infraestrutura no Google cloud
- Cliente B criamos a infraestrutura na Amazon
- Cliente C criamos a infraestrutura na Azure

Há uma maior segurança, por mais que possamos garantir uma configuração muito bem feita do multi tenant, como os dados ficam no mesmo banco de dados, pode haver situações hipoteticas não confirmadas que permitam que um hacker ou atacante possa acessar dados indevidos de várias empresas, ou de empresa A acessando coisas de empresa B.

---

Desvantagens:

Há um maior custo e perca de tempo dando manutenção, há também o risco que pelos ambientes serem separados o cliente pedirem features e customizações que não são compativeis para todos os ambientes.

---
---

Diferentemente do single tenant, a aplicação que utiliza o estilo de arquitetura multi tenant tem como objetivo compartilhar a mesma instância da aplicação para atender vários clientes (inquilinos).

---

Vantagens:

É mais fácil dar manutenção em cenários com muitos clientes em aplicações multi tenant. (É necessário somente atualizar uma única aplicação).

Centralizamos a infraestrutura em somente um lugar, podendo levar assim por fim menores custos de infraestrutura.

---

Desvantagem:

Em algumas situações, o olhar crítico referente a vazamento de dados, isolamento de dados, segurança em geral devem ser muitos maiores, por exemplo, em caso de queries manuais, deve se precaver e muito que um usuário da aplicação A nunca por N motivos possa ver dados de usuário de aplicação B.

Customização nessa estratégia é mais dificil, por exemplo, todos os clientes usam o mesmo software, todavia somente um cliente quer que o aplicativo seja mais customizado, levando a problemas de codificação, que não seria tão grande se isolasse esse único cliente em um ambiente separado.