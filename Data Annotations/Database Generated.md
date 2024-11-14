---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 8:58:17 pm
date modified: quarta-feira, novembro 13º 2024, 9:06:40 pm
---
Essa data annotation é usada para definir como essa coluna vai ser manipulada pelo banco de dados. Indica se nessa coluna vai ser gerado um valor automatico pelo banco de dados, se é computado, ou se é configurado pelo BACKEND.

A data annotation [DatabaseGenerated] recebe um enum do tipo DatabaseGeneratedOption, ao qual tem 3 valores.

- **DatabaseGeneratedOption.None**: O valor **não** é gerado pelo banco de dados. O aplicativo é responsável por definir o valor da propriedade. Isso é útil quando você deseja inserir manualmente valores em uma coluna que normalmente seria gerada pelo banco de dados.
    
- **DatabaseGeneratedOption.Identity**: O valor é gerado pelo banco de dados **ao inserir** um novo registro. É comumente usado para colunas de chave primária que são auto-incrementadas (IDENTITY) pelo banco de dados.
    
- **DatabaseGeneratedOption.Computed**: O valor é gerado ou atualizado pelo banco de dados **ao inserir ou atualizar** um registro. Isso é típico para colunas que têm valores calculados, como somas, médias ou timestamps de última atualização.