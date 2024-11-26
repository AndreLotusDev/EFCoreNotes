---
aliases: 
tags: 
date created: terça-feira, novembro 26º 2024, 4:30:49 pm
date modified: terça-feira, novembro 26º 2024, 4:36:11 pm
---
Podemos definir Unidade de trabalho (unit of work) como uma única transação que pode envolver múltiplas operações tais como: (inserção/atualização/exclusão).

Mantém uma lista de objetos de negócios afetados por uma transação e coordena a escrita a partir de alterações e a resolução de problemas de concorrência.

Fun fact: o DbContext por definição já é o UOW implementado, ele contem todos os dbset e tem um metodo para finalizar a transação.

---

