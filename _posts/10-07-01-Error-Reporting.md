---
isChild: true
anchor:  error_reporting
---

## Reporte de Erros {#error_reporting_title}

O rexistro de erros pode ser útil para atopar os puntos problemáticos na túa aplicación, pero tamén pode expoñer información sobre
a estrutura da túa aplicación ao mundo exterior. Para protexer efectivamente a túa aplicación de problemas que poderían
ser causados pola saída destas mensaxes, necesitas configurar o teu servidor diferentemente en desenvolvemento versus
produción (en vivo).

### Desenvolvemento

Para mostrar cada erro posible durante o **desenvolvemento**, configura as seguintes configuracións no teu `php.ini`:

{% highlight ini %}
display_errors = On
display_startup_errors = On
error_reporting = -1
log_errors = On
{% endhighlight %}

> Pasar o valor `-1` mostrará cada erro posible, mesmo cando novos niveis e constantes son engadidos en futuras versións de PHP.
> A constante `E_ALL` tamén se comporta deste xeito a partir de PHP 5.4. -
> [php.net](https://www.php.net/function.error-reporting)

A constante de nivel de erro `E_STRICT` foi introducida en 5.3.0 e non é parte de `E_ALL`, con todo converteuse en parte de
`E_ALL` en 5.4.0. Que significa isto? En termos de reportar cada erro posible na versión 5.3 significa que debes
usar ou `-1` ou `E_ALL | E_STRICT`.

**Reportando cada erro posible por versión de PHP**

* &lt; 5.3 `-1` ou `E_ALL`
* &nbsp; 5.3 `-1` ou `E_ALL | E_STRICT`
* &gt; 5.3 `-1` ou `E_ALL`

### Produción

Para ocultar erros no teu ambiente de **produción**, configura o teu `php.ini` como:

{% highlight ini %}
display_errors = Off
display_startup_errors = Off
error_reporting = E_ALL
log_errors = On
{% endhighlight %}

Con estas configuracións en produción, os erros aínda serán rexistrados nos rexistros de erro do servidor web, pero non serán
mostrados ao usuario. Para máis información sobre estas configuracións, vexa o manual de PHP:

* [error_reporting](https://www.php.net/errorfunc.configuration#ini.error-reporting)
* [display_errors](https://www.php.net/errorfunc.configuration#ini.display-errors)
* [display_startup_errors](https://www.php.net/errorfunc.configuration#ini.display-startup-errors)
* [log_errors](https://www.php.net/errorfunc.configuration#ini.log-errors)
