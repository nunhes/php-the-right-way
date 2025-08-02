---
isChild: true
anchor:  programming_paradigms
---

## Paradigmas de Programación {#programming_paradigms_title}

PHP é unha linguaxe flexible e dinámica que soporta unha variedade de técnicas de programación. Evolucionou dramaticamente ao longo
dos anos, notablemente engadindo un modelo sólido orientado a obxectos en PHP 5.0 (2004), funcións anónimas e espazos de nomes en
PHP 5.3 (2009), e traits en PHP 5.4 (2012).

### Programación Orientada a Obxectos

PHP ten un conxunto moi completo de funcionalidades de programación orientada a obxectos incluíndo soporte para clases, clases abstractas,
interfaces, herdanza, construtores, clonación, excepcións, e máis.

* [Ler sobre PHP Orientado a Obxectos][oop]
* [Ler sobre Traits][traits]

### Programación Funcional

PHP soporta funcións de primeira clase, significando que unha función pode ser asignada a unha variable. Tanto funcións definidas polo usuario como
funcións integradas poden ser referenciadas por unha variable e invocadas dinamicamente. As funcións poden ser pasadas como argumentos a
outras funcións (unha funcionalidade chamada _Funcións de Orde Superior_) e as funcións poden retornar outras funcións.

A recursión, unha funcionalidade que permite a unha función chamarse a si mesma, está soportada pola linguaxe, pero a maioría do código PHP
está enfocado na iteración.

As novas funcións anónimas (con soporte para closures) están presentes desde PHP 5.3 (2009).

PHP 5.4 engadiu a capacidade de vincular closures ao ámbito dun obxecto e tamén mellorou o soporte para callables de tal xeito que poden
ser usados intercambiablemente con funcións anónimas en case todos os casos.

* Continúa lendo sobre [Programación Funcional en PHP](/pages/Functional-Programming.html)
* [Ler sobre Funcións Anónimas][anonymous-functions]
* [Ler sobre a clase Closure][closure-class]
* [Máis detalles no RFC de Closures][closures-rfc]
* [Ler sobre Callables][callables]
* [Ler sobre invocar funcións dinamicamente con `call_user_func_array()`][call-user-func-array]

### Meta Programación

PHP soporta varias formas de meta-programación a través de mecanismos como a API de Reflection e Métodos Máxicos. Hai
moitos Métodos Máxicos dispoñibles como `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, etc. que permiten
aos desenvolvedores enganchar no comportamento das clases. Os desenvolvedores de Ruby a miúdo din que a PHP lle falta `method_missing`, pero está
dispoñible como `__call()` e `__callStatic()`.

* [Ler sobre Métodos Máxicos][magic-methods]
* [Ler sobre Reflection][reflection]
* [Ler sobre Overloading][overloading]


[oop]: https://www.php.net/language.oop5
[traits]: https://www.php.net/language.oop5.traits
[anonymous-functions]: https://www.php.net/functions.anonymous
[closure-class]: https://www.php.net/class.closure
[closures-rfc]: https://wiki.php.net/rfc/closures
[callables]: https://www.php.net/language.types.callable
[call-user-func-array]: https://www.php.net/function.call-user-func-array
[magic-methods]: https://www.php.net/language.oop5.magic
[reflection]: https://www.php.net/intro.reflection
[overloading]: https://www.php.net/language.oop5.overloading
