---
isChild: true
title:   Interacting with Databases
anchor:  databases_interacting
---

## Interacción con bases de datos {#databases_interacting_title}

Cando os desenvolvedores comezan a aprender PHP, a miúdo acaban mesturando a interacción da base de datos coa súa lóxica de presentación, usando código que podería ter este aspecto:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
{% endhighlight %}

Esta é unha mala práctica por moitos motivos, principalmente porque é difícil de depurar, difícil de probar, difícil de ler e vai xerar moitos campos se non se lle pon un límite.

Aínda que hai moitas outras solucións para facelo, dependendo de se prefires [OOP](/#object-oriented-programming) ou
[programación funcional](/#functional-programming) - debe haber algún elemento de separación.

Considera o paso básico:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

$results = getAllFoos($db);
foreach ($results as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

Ese é un bo comezo. Pon eses dous elementos en dous arquivos diferentes e terás unha separación clara.

Crea unha clase para colocar ese método e terás un "Modelo" - "Model"-. Crea un sinxelo arquivo `.php` para poñer a lóxica da presentación e tes un "Vista" - "View"-, que é case [MVC] - unha arquitectura POO común para a maioría dos
[frameworks](/#frameworks).

**foo.php**

{% highlight php %}
<?php
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8mb4', 'username', 'password');

// Fai que o teu modelo estea dispoñible
include 'models/FooModel.php';

// Crear unha instancia
$fooModel = new FooModel($db);
// Obtén a lista de Foos
$fooList = $fooModel->getAllFoos();

// Mostra a vista
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class FooModel
{
    public function __construct(protected PDO $db)
    {
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<?php foreach ($fooList as $row): ?>
    <li><?= $row['field1'] ?> - <?= $row['field1'] ?></li>
<?php endforeach ?>
{% endhighlight %}

Isto é esencialmente o mesmo que o que a maioría dos frameworks modernos están a facer, aínda que sexa un pouco máis manual. Podes non precisar facer todo isto cada vez, pero combinar demasiada lóxica de presentación e interacción coa base de datos pode ser un problema real se algún día queres unha proba unitaria [unit-test](/#unit-testing) da túa aplicación.


[MVC]: https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
