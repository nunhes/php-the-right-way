---
isChild: true
anchor:  command_line_interface
---

## Interfaz de Liña de Comandos {#command_line_interface_title}

PHP foi creado para escribir aplicacións web, pero tamén é útil para programar scripts de interfaz de liña de comandos (CLI).
Os programas PHP de liña de comandos poden axudar a automatizar tarefas comúns como probas, despliegue e administración de aplicacións.

Os programas CLI PHP son poderosos porque podes usar o código da túa aplicación directamente sen ter que crear e asegurar unha
GUI web para iso. Só asegúrate de **non** poñer os teus scripts PHP CLI no teu directorio raíz web público!

Tenta executar PHP desde a túa liña de comandos:

{% highlight console %}
> php -i
{% endhighlight %}

A opción `-i` imprimirá a túa configuración PHP xusto como a función [`phpinfo()`][phpinfo].

A opción `-a` proporciona un shell interactivo, similar ao IRB de ruby ou o shell interactivo de python. Hai un número
de outras [opcións de liña de comandos][cli-options] útiles tamén.

Escribamos un programa CLI simple "Ola, $name". Para probalo, crea un arquivo chamado `hello.php`, como abaixo.

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php <name>" . PHP_EOL;
    exit(1);
}
$name = $argv[1];
echo "Hello, $name" . PHP_EOL;
{% endhighlight %}

PHP configura dúas variables especiais baseadas nos argumentos co que o teu script é executado. [`$argc`][argc] é unha variable enteira
que contén a *conta* de argumentos e [`$argv`][argv] é unha variable array que contén o *valor* de cada argumento.
O primeiro argumento é sempre o nome do teu arquivo script PHP, neste caso `hello.php`.

A expresión `exit()` é usada cun número non cero para deixar que o shell saiba que o comando fallou. Códigos de saída comúns
poden ser atopados [aquí][exit-codes].

Para executar o noso script, de arriba, desde a liña de comandos:

{% highlight console %}
> php hello.php
Usage: php hello.php <name>
> php hello.php world
Hello, world
{% endhighlight %}


 * [Aprender sobre executar PHP desde a liña de comandos][php-cli]

[phpinfo]: https://www.php.net/function.phpinfo
[cli-options]: https://www.php.net/features.commandline.options
[argc]: https://www.php.net/reserved.variables.argc
[argv]: https://www.php.net/reserved.variables.argv
[exit-codes]: https://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: https://www.php.net/manual/en/features.commandline.php
