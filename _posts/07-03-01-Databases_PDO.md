---
isChild: true
title:   Extensión PDO
anchor:  pdo_extension
---

## Extensión PDO {#pdo_extension_title}

[PDO] é unha libraría de abstracción de conexión a bases de datos &mdash; integrada en PHP desde 5.1.0 &mdash; que proporciona unha interface
común para falar con moitas bases de datos diferentes. Por exemplo, podes usar código basicamente idéntico para interactuar con
MySQL ou SQLite:

{% highlight php %}
<?php
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some_field FROM some_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO non traducirá as túas consultas SQL ou emulará funcionalidades que faltan; é puramente para conectar a múltiples tipos de
base de datos coa mesma API.

Máis importante, `PDO` permite inxectar de forma segura entrada estraña (ex. IDs) nas túas consultas SQL sen preocuparte
sobre ataques de inxección SQL da base de datos.
Isto é posible usando statements PDO e parámetros vinculados.

Asumamos que un script PHP recibe un ID numérico como parámetro de consulta. Este ID debería ser usado para obter un rexistro de usuario
desde unha base de datos. Esta é a forma `incorrecta` de facelo:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NON!
{% endhighlight %}

Este é código terrible. Estás inserindo un parámetro de consulta bruto nunha consulta SQL. Isto che levará a ser hackeado nun
instante, usando unha práctica chamada [SQL Injection]. Só imaxina se un hacker pasa un parámetro `id` inventivo
chamando unha URL como `http://domain.com/?id=1%3BDELETE+FROM+users`. Isto establecerá a variable `$_GET['id']` a `1; DELETE
FROM users` que eliminará todos os teus usuarios! En cambio, deberías sanitizar a entrada do ID usando parámetros vinculados PDO.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$id = filter_input(INPUT_GET, 'id', FILTER_SANITIZE_NUMBER_INT); // <-- filtra os teus datos primeiro (ver [Filtrado de Datos](#data_filtering)), especialmente importante para INSERT, UPDATE, etc.
$stmt->bindParam(':id', $id, PDO::PARAM_INT); // <-- Automaticamente sanitizado para SQL por PDO
$stmt->execute();
{% endhighlight %}

Este é código correcto. Usa un parámetro vinculado nun statement PDO. Isto escapa a entrada estraña do ID antes de que sexa
introducida na base de datos previndo potenciais ataques de inxección SQL.

Para escrituras, como INSERT ou UPDATE, é especialmente crítico aínda [filtrar os teus datos](#data_filtering) primeiro e sanitizalos para outras cousas (eliminación de etiquetas HTML, JavaScript, etc). PDO só o sanitizará para SQL, non para a túa aplicación.

* [Aprender sobre PDO][pdo]

Tamén deberías ser consciente de que as conexións a bases de datos usan recursos e non era inaudito ter recursos
esgotados se as conexións non se pechaban implicitamente, con todo isto era máis común noutras linguaxes. Usando PDO podes
pechar implicitamente a conexión destruíndo o obxecto asegurándote de que todas as referencias restantes a el son eliminadas, ex.
establecidas a NULL. Se non fas isto explicitamente, PHP pechará automaticamente a conexión cando o teu script termine -
a menos que por suposto esteas usando conexións persistentes.

* [Aprender sobre conexións PDO]


[pdo]: https://www.php.net/pdo
[SQL Injection]: https://web.archive.org/web/20210413233627/http://wiki.hashphp.org/Validation
[Aprender sobre conexións PDO]: https://www.php.net/pdo.connections
