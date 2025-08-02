---
isChild: true
anchor:  data_filtering
---

## Filtrado de Datos {#data_filtering_title}

Nunca (nunca) confíes na entrada estraña introducida no teu código PHP. Sempre sanitiza e valida a entrada estraña antes de
usala no código. As funcións `filter_var()` e `filter_input()` poden sanitizar texto e validar formatos de texto (ex.
enderezos de email).

A entrada estraña pode ser calquera cousa: datos de entrada de formulario `$_GET` e `$_POST`, algúns valores no superglobal `$_SERVER`, e o
corpo da petición HTTP vía `fopen('php://input', 'r')`. Lembra, a entrada estraña non está limitada a datos de formulario enviados polo
usuario. Arquivos subidos e descargados, valores de sesión, datos de cookies, e datos de servizos web de terceiros son entrada
estraña tamén.

Mentres os datos estraños poden ser almacenados, combinados, e accedidos máis tarde, aínda é entrada estraña. Cada vez que procesas,
saes, concatenas, ou inclúes datos no teu código, pregúntate se os datos están filtrados adecuadamente e se poden ser confiábeis.

Os datos poden ser _filtrados_ diferentemente baseado no seu propósito. Por exemplo, cando a entrada estraña non filtrada é pasada á saída da páxina HTML,
pode executar HTML e JavaScript no teu sitio! Isto é coñecido como Cross-Site Scripting (XSS) e pode ser un
ataque moi perigoso. Unha forma de evitar XSS é sanitizar todos os datos xerados polo usuario antes de saílos á túa páxina
eliminando etiquetas HTML coa función `strip_tags()` ou escapando caracteres con significado especial ás súas respectivas
entidades HTML coas funcións `htmlentities()` ou `htmlspecialchars()`.

Outro exemplo é pasar opcións para ser executadas na liña de comandos. Isto pode ser extremadamente perigoso (e xeralmente é
unha mala idea), pero podes usar a función integrada `escapeshellarg()` para sanitizar os argumentos do comando executado.

Un último exemplo é aceptar entrada estraña para determinar un arquivo para cargar desde o sistema de arquivos. Isto pode ser explotado
cambiando o nome do arquivo a unha ruta de arquivo. Necesitas eliminar `"/"`, `"../"`, [bytes nulos][6], ou outros caracteres da
ruta do arquivo para que non poida cargar arquivos ocultos, non públicos, ou sensíbeis.

* [Aprender sobre filtrado de datos][1]
* [Aprender sobre `filter_var`][4]
* [Aprender sobre `filter_input`][5]
* [Aprender sobre manexo de bytes nulos][6]

### Sanitización

A sanitización elimina (ou escapa) caracteres ilegais ou inseguros da entrada estraña.

Por exemplo, deberías sanitizar a entrada estraña antes de incluír a entrada no HTML ou inserila nunha consulta SQL bruta.
Cando usas parámetros vinculados con [PDO](#databases), sanitizará a entrada para ti.

Ás veces é requirido permitir algunhas etiquetas HTML seguras na entrada cando a inclúes na páxina HTML. Isto é moi
difícil de facer e moitos evítano usando outro formato máis restritivo como Markdown ou BBCode, aínda que bibliotecas de lista branca
como [HTML Purifier][html-purifier] existen por esta razón.

[Ver Filtros de Sanitización][2]

### Deserialización

É perigoso `unserialize()` datos de usuarios ou outras fontes non confiábeis. Facelo pode permitir a usuarios maliciosos instanciar obxectos (con propiedades definidas polo usuario) cuxos destructores serán executados, **mesmo se os obxectos en si non son usados**. Polo tanto deberías evitar deserializar datos non confiábeis.

Usa un formato seguro e estándar de intercambio de datos como JSON (vía [`json_decode`][json_decode] e [`json_encode`][json_encode]) se necesitas pasar datos serializados ao usuario.

### Validación

A validación asegura que a entrada estraña é o que esperas. Por exemplo, podes querer validar un enderezo de email, un
número de teléfono, ou idade cando procesas un envío de rexistro.

[Ver Filtros de Validación][3]


[1]: https://www.php.net/book.filter
[2]: https://www.php.net/filter.filters.sanitize
[3]: https://www.php.net/filter.filters.validate
[4]: https://www.php.net/function.filter-var
[5]: https://www.php.net/function.filter-input
[6]: https://www.php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
[json_decode]: https://www.php.net/manual/function.json-decode.php
[json_encode]: https://www.php.net/manual/function.json-encode.php
