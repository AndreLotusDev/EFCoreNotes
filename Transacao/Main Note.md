---
aliases: 
tags: 
date created: sexta-feira, novembro 15º 2024, 1:28:05 am
date modified: sexta-feira, novembro 15º 2024, 1:56:08 am
---
Quando estamos falando transação, principalmente no contexto de banco de dados, naturalmente estamos falando sobre uma sequência de operações que serão executadas.

Uma transação possui:

- Atomicidade: "Faz tudo, ou não faz nada". Em uma transação que envolve duas ou mais partes de informações, ou a transação será executada totalmente ou não será executada.
	- Exemplo: Eu preencho um carrinho de compras, e ao mesmo tempo insiro no historico do usuario a movimentação dele. Se um dos dois inserts der errado, nem um nem outro será inserido, pois um depende do outro.
- Consistencia: Garantir que o banco de dados esteja consistente antes e depois de um transação, a transação deve sempre finalizar com o estado consistente.
	- Nada de adicionar uma Pessoa sem seu endereço, sendo que se considerar o modelo de domínio uma pessoa não existe no sistema sem seu endereço, gerando assim dirty inserts.
- Isolamento: Uma transação em andamento que ainda não foi confirmada deve permanecer totalmente isolada de outras operações, dessa forma o banco de dados garante que a transação não ser interferida por nenhuma outra transação concorrente.
	- Exemplo: Se eu estou fazendo um insert, e outro usuário faz um select, ele não pode ver o insert que estou fazendo.
- Durabilidade: Basicamente é fazer com os dados sejam gravados no seu banco de dados, depois desse passo mesmo que o serviço do banco de dados seja reinicializado, seus dados ainda estão disponíveis para você acessar.

---

Por default, você pode empilhar comandos no EF Core, e somente quando executa o SaveChanges é que todos os comandos são encapsulados em uma transação e são executados em conjunto.

Se alguma coisa falhar de forma singular irá impedir que as demais também sejam salvas, alteradas e editadas.

Exemplo:

1 - Adiciono uma pessoa no banco de dados (dbContext.Add(pessoaTemp)).
2 - Adiciono uma segunda pessoa no banco de dados (dbContext.Add(segundaPessoa)).
3 - Adiciono um endereço, so que sem a descrição, ao qual é uma coluna requerida no banco de dados (irá produzir erro).
4 - Tento salvar, ao tentar salvar, ele verá que endereço não está preenchido corretamente e irá entregar um erro, fazendo assim que não somente o endereço não seja salvo como pessoa um e dois.

PS: Para cada vez que voce chama o metodo .SaveChanges() é como se você tivesse explicitando para o EF Core para ele encerrar a transação.