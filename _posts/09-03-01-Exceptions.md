---
title: Excepcións
isChild: true
anchor:  exceptions
---

## Excepcións {#exceptions_title}

As excepcións son unha parte estándar da maioría das linguaxes de programación populares, pero a miúdo son pasadas por alto polos programadores PHP.
Linguaxes como Ruby son extremadamente pesadas en Excepcións, polo que sempre que algo vai mal como unha petición HTTP fallando, ou
unha consulta de BD vai mal, ou mesmo se un recurso de imaxe non se puido atopar, Ruby (ou as xemas sendo usadas) lanzarán unha
excepción á pantalla significando que instantaneamente sabes que hai un erro.

PHP en si é bastante laxo con isto, e unha chamada a `file_get_contents()` xeralmente só che dará un `FALSE` e unha
advertencia.
Moitos frameworks PHP antigos como CodeIgniter só retornarán un false, rexistrarán unha mensaxe nos seus rexistros propietarios e quizais
te deixen usar un método como `$this->upload->get_error()` para ver que foi mal. O problema aquí é que tes que ir
buscando un erro e verificar a documentación para ver cal é o método de erro para esta clase, en lugar de tero feito
extremadamente obvio.

Outro problema é cando as clases automaticamente lanzan un erro á pantalla e saen do proceso. Cando fas isto
paras outro desenvolvedor de poder manexar dinamicamente ese erro. As excepcións deberían ser lanzadas para facer un
desenvolvedor consciente dun erro; entón poden elixir como manexar isto. Ex.:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // A validación fallou
}
catch(Fuel\Email\SendingFailedException $e)
{
    // O driver non puido enviar o email
}
finally
{
    // Executado independentemente de se unha excepción foi lanzada, e antes de que a execución normal continúe
}
{% endhighlight %}

### Excepcións SPL

A clase xenérica `Exception` proporciona moi pouco contexto de depuración para o desenvolvedor; con todo, para remediar isto, é
posible crear un tipo de `Exception` especializado sub-clasificando a clase xenérica `Exception`:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Isto significa que podes engadir múltiples bloques catch e manexar diferentes Excepcións de forma diferente. Isto pode levar á
creación de <em>moitas</em> Excepcións personalizadas, algunhas das cales poderían ser evitadas usando as Excepcións SPL
proporcionadas na [extensión SPL][splext].

Se por exemplo usas o Método Máxico `__call()` e un método inválido é solicitado entón en lugar de lanzar unha
Excepción estándar que é vaga, ou crear unha Excepción personalizada só para iso, poderías simplemente
`throw new BadMethodCallException;`.

* [Ler sobre Excepcións][exceptions]
* [Ler sobre Excepcións SPL][splexe]
* [Anidando Excepcións en PHP][nesting-exceptions-in-php]


[splext]: /#standard_php_library
[exceptions]: https://www.php.net/language.exceptions
[splexe]: https://www.php.net/spl.exceptions
[nesting-exceptions-in-php]: https://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
