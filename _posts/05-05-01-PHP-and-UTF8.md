---
title:   Traballando con UTF-8
isChild: true
anchor:  php_and_utf8
---

## Traballando con UTF-8 {#php_and_utf8_title}

_Esta sección foi orixinalmente escrita por [Alex Cabal](https://alexcabal.com/) en
[PHP Best Practices](https://phpbestpractices.org/#utf-8) e foi usada como base para o noso propio consello UTF-8_.

### Non hai unha liña única. Sé coidadoso, detallado e consistente.

Actualmente PHP non soporta Unicode a baixo nivel. Hai formas de asegurar que as cadeas UTF-8 son procesadas ben,
pero non é fácil, e require escavar en case todos os niveis da aplicación web, desde HTML a SQL a PHP. Pretendemos
un resumo breve e práctico.

### UTF-8 ao nivel de PHP

As operacións básicas de cadeas, como concatenar dúas cadeas e asignar cadeas a variables, non necesitan nada
especial para UTF-8. Con todo, a maioría das funcións de cadeas, como `strpos()` e `strlen()`, necesitan consideración especial. Estas
funcións a miúdo teñen unha contraparte `mb_*`: por exemplo, `mb_strpos()` e `mb_strlen()`. Estas funcións de cadeas `mb_*` están feitas
dispoñibles para ti a través da [Extensión de Cadeas Multibyte], e están especificamente deseñadas para operar en cadeas Unicode.

Debes usar as funcións `mb_*` sempre que operes nunha cadea Unicode. Por exemplo, se usas `substr()` nunha
cadea UTF-8, hai unha boa posibilidade de que o resultado inclúa algúns caracteres medio confusos. A función correcta para usar
sería a contraparte multibyte, `mb_substr()`.

A parte difícil é recordar usar as funcións `mb_*` en todo momento. Se esqueces incluso só unha vez, a túa cadea Unicode
ten unha posibilidade de ser confusa durante o procesamento posterior.

Non todas as funcións de cadeas teñen unha contraparte `mb_*`. Se non hai unha para o que queres facer, entón poderías estar
sen sorte.

Debes usar a función `mb_internal_encoding()` no cume de cada script PHP que escribas (ou no cume do teu
script de inclusión global), e a función `mb_http_output()` xusto despois dela se o teu script está saíndo a un navegador.
Definir explicitamente a codificación das túas cadeas en cada script che aforrará moitas dores de cabeza no futuro.

Ademais, moitas funcións PHP que operan en cadeas teñen un parámetro opcional permitíndoche especificar a codificación de caracteres.
Debes sempre indicar explicitamente UTF-8 cando teñes a opción. Por exemplo, `htmlentities()` ten unha
opción para codificación de caracteres, e debes sempre especificar UTF-8 se tratas con tales cadeas. Nota que desde PHP 5.4.0, UTF-8 é a codificación por defecto para `htmlentities()` e `htmlspecialchars()`.

Finalmente, se estás construíndo unha aplicación distribuída e non podes estar certo de que a extensión `mbstring` será
habilitada, entón considera usar o paquete Composer [symfony/polyfill-mbstring]. Isto usará `mbstring` se está dispoñible, e
volverá a funcións non UTF-8 se non.

[Multibyte String Extension]: https://www.php.net/book.mbstring
[symfony/polyfill-mbstring]: https://packagist.org/packages/symfony/polyfill-mbstring

### UTF-8 ao nivel da Base de Datos

Se o teu script PHP accede a MySQL, hai unha posibilidade de que as túas cadeas poidan ser almacenadas como cadeas non UTF-8 na base de datos
mesmo se segues todas as precaucións anteriores.

Para asegurar que as túas cadeas van desde PHP a MySQL como UTF-8, asegúrate de que a túa base de datos e táboas están todas configuradas ao
conxunto de caracteres e colación `utf8mb4`, e que usas o conxunto de caracteres `utf8mb4` na cadea de conexión PDO. Vexa
código de exemplo abaixo. Isto é _críticamente importante_.

Nota que debes usar o conxunto de caracteres `utf8mb4` para soporte completo UTF-8, non o conxunto de caracteres `utf8`! Vexa
Lectura Adicional para por que.

### UTF-8 ao nivel do Navegador

Usa a función `mb_http_output()` para asegurar que o teu script PHP sae cadeas UTF-8 ao teu navegador.

O navegador entón necesitará ser dito pola resposta HTTP que esta páxina debería ser considerada como UTF-8. Hoxe, é común configurar o conxunto de caracteres no cabeceira da resposta HTTP así:

{% highlight php %}
<?php
header('Content-Type: text/html; charset=UTF-8')
{% endhighlight %}

O enfoque histórico para facer iso era incluír a [etiqueta `<meta>` charset](http://htmlpurifier.org/docs/enduser-utf8.html) na túa etiqueta `<head>` da páxina.

{% highlight php %}
<?php
// Dille a PHP que estamos usando cadeas UTF-8 ata o final do script
mb_internal_encoding('UTF-8');
$utf_set = ini_set('default_charset', 'utf-8');
if (!$utf_set) {
    throw new Exception('could not set default_charset to utf-8, please ensure it\'s set on your system!');
}

// Dille a PHP que sairemos UTF-8 ao navegador
mb_http_output('UTF-8');
 
// A nosa cadea de proba UTF-8
$string = 'Êl síla erin lû e-govaned vîn.';

// Transforma a cadea dalgunha forma cunha función multibyte
// Nota como cortamos a cadea nun carácter non-Ascii para propósitos de demostración
$string = mb_substr($string, 0, 15);

// Conecta a unha base de datos para almacenar a cadea transformada
// Vexa o exemplo PDO neste documento para máis información
// Nota o `charset=utf8mb4` no Nome da Fonte de Datos (DSN)
$link = new PDO(
    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
    'your-username',
    'your-password',
    array(
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_PERSISTENT => false
    )
);

// Almacena a nosa cadea transformada como UTF-8 na nosa base de datos
// A túa BD e táboas están no conxunto de caracteres e colación utf8mb4, certo?
$handle = $link->prepare('insert into ElvishSentences (Id, Body, Priority) values (default, :body, :priority)');
$handle->bindParam(':body', $string, PDO::PARAM_STR);
$priority = 45;
$handle->bindParam(':priority', $priority, PDO::PARAM_INT); // dille explicitamente a pdo que espere un int
$handle->execute();

// Recupera a cadea que acabamos de almacenar para probar que foi almacenada correctamente
$handle = $link->prepare('select * from ElvishSentences where Id = :id');
$id = 7;
$handle->bindParam(':id', $id, PDO::PARAM_INT);
$handle->execute();

// Almacena o resultado nun obxecto que sairemos máis tarde no noso HTML
// Este obxecto non matará a túa memoria porque obtén os datos Just-In-Time para
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

// Un exemplo wrapper para permitirche escapar datos a html
function escape_to_html($dirty){
    echo htmlspecialchars($dirty, ENT_QUOTES, 'UTF-8');
}
// Innecesario se o teu 'default_charset' xa está configurado a utf-8
header('Content-Type: text/html; charset=UTF-8'); 
?><!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            escape_to_html($row->Body);  // Isto debería mostrar correctamente a nosa cadea UTF-8 transformada ao navegador
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Lectura adicional

* [Manual PHP: Operacións de Cadeas](https://www.php.net/language.operators.string)
* [Manual PHP: Funcións de Cadeas](https://www.php.net/ref.strings)
    * [`strpos()`](https://www.php.net/function.strpos)
    * [`strlen()`](https://www.php.net/function.strlen)
    * [`substr()`](https://www.php.net/function.substr)
* [Manual PHP: Funcións de Cadeas Multibyte](https://www.php.net/ref.mbstring)
    * [`mb_strpos()`](https://www.php.net/function.mb-strpos)
    * [`mb_strlen()`](https://www.php.net/function.mb-strlen)
    * [`mb_substr()`](https://www.php.net/function.mb-substr)
    * [`mb_internal_encoding()`](https://www.php.net/function.mb-internal-encoding)
    * [`mb_http_output()`](https://www.php.net/function.mb-http-output)
    * [`htmlentities()`](https://www.php.net/function.htmlentities)
    * [`htmlspecialchars()`](https://www.php.net/function.htmlspecialchars)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](https://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](https://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4)
* [Bringing Unicode to PHP with Portable UTF-8](https://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
* [Stack Overflow: DOMDocument loadHTML does not encode UTF-8 correctly](https://stackoverflow.com/questions/8218230/php-domdocument-loadhtml-not-encoding-utf-8-correctly)
