---
aliases: 
tags: 
date created: sábado, novembro 16º 2024, 4:58:19 pm
date modified: sábado, novembro 16º 2024, 5:07:29 pm
---
É sempre bom por convenção e boas práticas nunca ir diretamente numa tabela do tipo DbSet e dar um ToList e ToArray, é sempre importante somente trazer o que é necessário para a camada do backend, sempre selecionando somente o necessário.

Isso se dá pois, vamos supor que temos um sistema de redes sociais e tenho um painel admnistrativo, e eu posso dentro desse painel acessar todos os usuários de uma vez, e eu preciso somente ler na tabela USUARIO o NOME e SOBRENOME, se eu fizer uma query trazendo tudo no EF Core, e então dentro dessa tabela tiver uma coluna do tipo imagem, isso por fim irá onerar e muito a performance do BACKEND.