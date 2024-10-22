---
aliases: 
tags: 
date created: terça-feira, outubro 22º 2024, 2:06:44 am
date modified: terça-feira, outubro 22º 2024, 2:10:34 am
---
# O que é Code First?

Geralmente é a abordagem mais popular e natural para quem utiliza o Entity Framework Core.

Basicamente o que você faz é o seguinte, em vez de criar todo banco de dados primeiro, você como programador se concentra no domínio, e começa criando suas classes que posteriormente irão se materializar em tabelas de seu banco de dados, o qual são conhecidos como Fluente API que é um das formas de fazer todo mapeamento de entidade, utilizando métodos, ou Data Annotation (direto na classe), que são atributos adicionados a uma classe ou uma propriedade.

O data annotation é muito limitado, sendo recomendado então na maior parte do tempo se utilizar do fluentAPI onde permite maior flexibilidade.