---
aliases: 
tags: 
date created: quarta-feira, novembro 13º 2024, 8:42:44 pm
date modified: quarta-feira, novembro 13º 2024, 8:46:16 pm
---
É possível usando o data annotation configurar o nome da tabela na classe.

Exemplo:

```cs
[Table("Client")]
public class Cliente
{
	[Key]
    public int Id { get; set; }

	[Required]
	[Column("Nome", TypeName= "VARCHAR(300)")]
    public string Nome { get; set; }

	[MaxLength(300)]
    public string Email { get; set; }
}
```