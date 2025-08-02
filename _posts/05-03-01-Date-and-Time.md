---
title:   Data e Hora
isChild: true
anchor:  date_and_time
---

## Data e Hora {#date_and_time_title}

PHP ten unha clase chamada DateTime para axudarte cando leas, escribas, compares ou calcules con data e hora. Hai
moitas funcións relacionadas con data e hora en PHP ademais de DateTime, pero proporciona unha interface orientada a obxectos agradable para
os usos máis comúns. DateTime pode manexar zonas horarias, pero iso está fóra do alcance desta breve introdución.

Para comezar a traballar con DateTime, converte a cadea bruta de data e hora a un obxecto co método factory `createFromFormat()`
ou fai `new DateTime` para obter a data e hora actual. Usa o método `format()` para converter DateTime de volta a unha cadea para
saída.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('Y-m-d') . PHP_EOL;
{% endhighlight %}

Calcular con DateTime é posible coa clase DateInterval. DateTime ten métodos como `add()` e `sub()` que
toman un DateInterval como argumento. Non escribas código que espere o mesmo número de segundos en cada día. Tanto o horario de verán
como as alteracións de zona horaria romperán esa suposición. Usa intervalos de data en cambio. Para calcular a diferenza de data
usa o método `diff()`. Retornará un novo DateInterval, que é super fácil de mostrar.

{% highlight php %}
<?php
// crea unha copia de $start e engade un mes e 6 días
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . PHP_EOL;
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

Podes usar comparacións estándar en obxectos DateTime:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before the end!" . PHP_EOL;}
{% endhighlight %}

Un último exemplo para demostrar a clase DatePeriod. Úsase para iterar sobre eventos recorrentes. Pode tomar dous
obxectos DateTime, inicio e fin, e o intervalo para o cal retornará todos os eventos entre eles.

{% highlight php %}
<?php
// saída todos os xoves entre $start e $end
$periodInterval = DateInterval::createFromDateString('first thursday');
$periodIterator = new DatePeriod($start, $periodInterval, $end, DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // saída cada data no período
    echo $date->format('Y-m-d') . ' ';
}
{% endhighlight %}

Unha extensión API PHP popular é [Carbon](https://carbon.nesbot.com/). Herda todo na clase DateTime, polo que implica alteracións mínimas de código, pero as funcionalidades extra inclúen soporte de Localización, máis formas de engadir, subtraer e formatear un obxecto DateTime, ademais dun medio para probar o teu código simulando unha data e hora da túa elección.

* [Ler sobre DateTime][datetime]
* [Ler sobre formateado de data][dateformat] (opcións de cadea de formato de data aceptadas)

[datetime]: https://www.php.net/book.datetime
[dateformat]: https://www.php.net/function.date
