---
tags: 
aliases:
  - Ensure Created / Ensure Deleted
date created: terça-feira, outubro 22º 2024, 7:13:02 pm
date modified: terça-feira, outubro 22º 2024, 7:20:34 pm
---
O Ensure Created garante que no ambiente de desenvolvimento ou local ele sempre irá validar se o banco de dados não exista, e se não existe irá criar e irá aplicar pelo menos o primeiro schema de tabelas, muito útil.

Todavia temos o Migrate(); para ambiente de produção onde sempre que subimos um POD novo verificamos se as migrações estão em dia, caso contrário executa as migrações primeiro.

---

O Ensure Deleted é muito útil para ambiente de desenvolvimento e ambiente local, onde quando o POD morre podemos forçar também a deleção e limpeza dos dados localmente.

---

