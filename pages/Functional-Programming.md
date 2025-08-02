---
layout: page
title:  Programación Funcional en PHP
sitemap: true
---

# Programación Funcional en PHP

PHP soporta funcións de primeira clase, o que significa que unha función pode ser asignada a unha variable. Tanto as funcións definidas polo usuario como as funcións incorporadas poden ser referenciadas por unha variable e invocadas dinámicamente. As funcións poden pasarse como argumentos a outras funcións e unha función pode devolver outras funcións (unha característica coñecida como funcións de orde superior).

A recursión, unha característica que permite a unha función chamarse a si mesma, está soportada pola linguaxe, pero a maioría do código PHP está enfocado á iteración.

As funcións anónimas (con soporte para clausuras) están presentes dende PHP 5.3 (2009).

PHP 5.4 engadiu a capacidade de vincular clausuras ao ámbito dun obxecto e tamén mellorou o soporte para callables, de xeito que poden usarse de forma intercambiable con funcións anónimas en case todos os casos.

O uso máis común das funcións de orde superior é cando se implementa un patrón de estratexia. A función incorporada `array_filter()`
pide tanto o array de entrada (datos) como unha función (unha estratexia ou callback) que se usa como función de filtro en cada elemento do array.

{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// Creates a new anonymous function and assigns it to a variable
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// Built-in array_filter accepts both the data and the function
$output = array_filter($input, $filter_even);

// The function doesn't need to be assigned to a variable. This is valid too:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

Unha clausura é unha función anónima que pode acceder a variables importadas dende o ámbito externo sen usar variables globais. Teoricamente, unha clausura é unha función con algúns argumentos pechados (é dicir, fixados) polo ambiente cando se define. As clausuras poden eludir as restricións de ámbito de variables dun xeito limpo.

No seguinte exemplo usamos clausuras para definir unha función que devolve unha única función de filtro para `array_filter()`, dunha familia de funcións de filtro.

{% highlight php %}
<?php
/**
 * Creates an anonymous filter function accepting items > $min
 *
 * Returns a single filter out of a family of "greater than n" filters
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Use array_filter on a input with a selected filter function
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // items > 3
{% endhighlight %}

Cada función de filtro na familia só acepta elementos maiores que un valor mínimo. O filtro único devolto por
`criteria_greater_than` é unha clausura co argumento `$min` pechado polo valor no ámbito (dado como argumento cando
se chama a `criteria_greater_than`).

Por defecto, úsase early binding para importar a variable `$min` á función creada. Para clausuras con late
binding, débese usar unha referencia ao importar. Imaxina unha biblioteca de modelos ou validación de entrada, onde se define unha clausura para capturar variables no ámbito e acceder a elas máis tarde cando se avalía a función anónima.

* [Ler sobre funcións anónimas][anonymous-functions]
* [Máis detalles no RFC de Closures][closures-rfc]
* [Ler sobre a invocación dinámica de funcións con `call_user_func_array()`][call-user-func-array]


[anonymous-functions]: https://www.php.net/functions.anonymous
[closures-rfc]: https://wiki.php.net/rfc/closures
[call-user-func-array]: https://www.php.net/function.call-user-func-array
