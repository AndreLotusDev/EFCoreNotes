---
aliases: 
tags: 
date created: quinta-feira, novembro 14º 2024, 11:15:52 pm
date modified: quinta-feira, novembro 14º 2024, 11:53:20 pm
---
Podemos manipular datas no ef core, todavia manipular manualmente pode ser muito cansativo, complexo, e além de que pode prejudicar a legibilidade e facilidade de dar manutenção no programa.

É possivel calcular:

DateDiffYear: A diferença de anos entre duas datas.
DateDiffMonth: A diferença entre duas datas por mês.
DateDiffDay: A diferença de dias entre duas datas.
DateDiffHour: A diferença em horas entre duas datas.
DateDiffMinut: A diferença em minutos entre duas datas.
DateDiffSecond: A diferença em segundos entre duas datas.
DateDiffMillisecond: A diferença em milissegundo entre duas datas.
DateDiffMicrosecond: A diferença em microsegundos entre duas datas.
DateDiffNanosecond: A diferença entre duas datas em nano segundos.

Caso de uso:

```cs
var eventosLongos = contexto.Eventos .Where(e => EF.Functions.DateDiffDay(e.DataInicio, e.DataFim) > 30) .ToList();
```

É possível também validar se um campo pode ser considerado como data com o EF.Functions:

```cs
var eventos = contexto.Eventos .Where(e => EF.Functions.IsDate(e.DataInicio)) .ToList();
```

É possível também montar uma data a partir de pedaços com o EF.Functions:

```cs
var data = contexto.Eventos .Select(e => new DateTime(e.Ano, e.Mes, e.Dia)) .ToList();
```
