---
layout: page
title:  The Basics
sitemap: true
---

# Básicos

## Operadores de comparación

Os operadores de comparación son un aspecto do PHP que a miúdo se pasa por alto, o que pode levar a resultados inesperados. Un destes problemas provén das comparacións estritas (a comparación de booleanos como enteiros).

{% highlight php %}
<?php
$a = 5;   // 5 como enteiro, integer

var_dump($a == 5);       // compare value; return true
var_dump($a == '5');     // comparar valor (ignorar tipo); devolve verdadeiro - true
var_dump($a === 5);      // compare type/value (integer vs. integer); return true
var_dump($a === '5');    // comparar tipo/valor (enteiro vs. cadea|integer vs. string); devolve falso - false

// Comparacións de igualdade
if (strpos('testing', 'test')) {    // 'test' atópase na posición 0, que se interpreta como booleano 'false'
    // código...
}

// vs. comparacións estritas
if (strpos('testing', 'test') !== false) {    // true, xa que se fai unha comparación rigorosa (0 !== false)
    // código...
}
{% endhighlight %}

* [Operadores de comparación](https://www.php.net/language.operators.comparison)
* [Táboa comparativa](https://www.php.net/types.comparisons)
* [Folla de referencia de comparación](https://phpcheatsheets.com/index.php?page=compare)

## Sentenzas condicionais

### Sentenzas If

Ao usar sentenzas 'if/else' dentro dunha función ou método de clase, existe a idea errónea común de que 'else' debe usarse
xunto para declarar resultados potenciais. Non obstante, se o resultado é definir o valor de retorno, 'else' non é
necesario xa que 'return' rematará a función, facendo que 'else' deixe de ser relevante.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else non é necesario
}

// ou incluso máis curto:

function test($a)
{
    return (bool) $a;
}

{% endhighlight %}

* [Sentenzas If](https://www.php.net/control-structures.if)

### Sentenzas Switch

As sentenzas Switch son unha boa forma de evitar escribir infinitos if's e elseif's, pero hai algunhas cousas que ter en conta:

- As sentenzas Switch só comparan valores, non o tipo (equivalente a '==')
- Iteran caso por caso ata atopar unha coincidencia. Se non se atopa ningunha, úsase o valor por defecto (default, se está definido)
- Sen un 'break', continuarán executando cada caso ata chegar a un break/return
- Dentro dunha función, usar 'return' elimina a necesidade de 'break' xa que finaliza a función

{% highlight php %}
<?php
$answer = test(2);    // o código de ambos 'case 2' e 'case 3' serán implementados

function test($a)
{
    switch ($a) {
        case 1:
            // código...
            break;             // break úsase para finalizar a sentenza switch
        case 2:
            // código...         // sen break, a comparación continuará no 'case 3'
        case 3:
            // código...
            return $result;    // dentro dunha función, 'return' rematará a función
        default:
            // código...
            return $error;
    }
}
{% endhighlight %}

* [Sentenzas Switch](https://www.php.net/control-structures.switch)
* [PHP switch](http://phpswitch.com/)

## Espazo de nomes global - global namespace

Cando usas namespaces, pode que as funcións internas estean ocultas polas funcións que escribiches. Para solucionar isto, consulta a función global usando unha barra invertida antes do nome da función.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // O nome da nosa función é o mesmo que o dunha función interna.
                         // Executa a función desde o espazo global engadindo '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator é unha clase interna. Usando o seu nome sen barra invertida
                                         // tentará resolvelo dentro do teu espazo de nomes.
}
{% endhighlight %}

* [Espazo Global](https://www.php.net/language.namespaces.global)
* [Regras Globais](https://www.php.net/userlandnaming.rules)

## Cadeas - strings

### Concatenación

- Se a túa liña supera a lonxitude recomendada (120 caracteres), considera concatenar a túa liña
- Para mellorar a lexibilidade, é mellor usar operadores de concatenación no canto de operadores de asignación de concatenación
- Mentres esteas dentro do ámbito orixinal da variable, aplica sangría cando a concatenación usa unha nova liña


{% highlight php %}
<?php
$a  = 'Multi-line example';    // concatenating assignment operator (.=)
$a .= "\n";
$a .= 'of what not to do';

// vs

$a = 'Exemplo do que facer'      // operador de concatenación (.)
    . "\n"                     // sangrar novas liñas
    . 'con múltiples liñas';
{% endhighlight %}

* [Operadores de cadeas](https://www.php.net/language.operators.string)

### Tipos de cadeas

As cadeas de texto - strings- son unha serie de caracteres, o que debería parecer sinxelo. Dito isto, existen algúns tipos diferentes de cadeas de texto e ofrecen unha sintaxe lixeiramente diferente, con comportamentos lixeiramente diferentes.

#### Comiñas simples - Single quotes

As comiñas simples úsanse para denotar unha "cadea literal" (*literal string*). As cadeas literais non tentan analizar caracteres especiais nin variables.

Se usas comiñas simples, poderías introducir un nome de variable nunha cadea como esta: `'some $thing'`, e verías a
saída exacta de `some $thing`. Se usas comiñas dobres, se tentaría avaliar o nome da variable `$thing` e se mostrarían os
erros se non se atopaba ningunha variable.

{% highlight php %}
<?php
echo 'Esta é a miña cadea, mirade que bonita é.';    // non hai necesidade de analizar unha cadea simple

/**
 * Saída:
 *
 * Esta é a miña cadea, mirade que bonita é.
 */
 {% endhighlight %}

* [Comiñas simples](https://www.php.net/language.types.string#language.types.string.syntax.single)

#### Comiñas dobres - Double quotes

As comiñas dobres son a navalla suíza das cadeas de texto. Non só analizan variables como se mencionou anteriormente, senón tamén todo tipo de caracteres especiais, como `\n` para unha nova liña, `\t` para unha tabulación, etc.

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // a single quotes example that uses multiple concatenating for
    . "\n"                                       // variables and escaped string
    . 'I love learning' . $code . '!';

// vs

echo "phptherightway is $adjective.\n I love learning $code!"  // En lugar de concatenar varias veces, as comiñas dobres
                                                               // permítenos usar unha cadea analizable
{% endhighlight %}

As comiñas dobres poden conter variables; isto chámase "interpolación".

{% highlight php %}
<?php
$juice = 'plum';
echo "I like $juice juice";    // Saída: I like plum juice
{% endhighlight %}

Ao usar a interpolación, adoita ocorrer que a variable toca outro carácter. Isto xerará certa confusión sobre cal é o nome da variable e cal é un carácter literal.

Para solucionar este problema, envolva a variable entre corchetes.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice non se pode analizar

// vs

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice será analizado

/**
 * As variables complexas tamén se analizarán entre corchetes
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] será analizado
{% endhighlight %}

* [Comiñas dobres](https://www.php.net/language.types.string#language.types.string.syntax.double)

#### Sintaxe de Nowdoc

A sintaxe Nowdoc foi introducida en 5.3 e internamente compórtase do mesmo xeito que as comiñas simples, agás que é axeitado para o uso de cadeas de varias liñas sen necesidade de concatenación.

{% highlight php %}
<?php
$str = <<<'EOD'             // initialized by <<<
Example of string
spanning multiple lines
using nowdoc syntax.
$a non se analiza.
EOD;                        // o peche de "EOD" debe estar na súa propia liña e no punto máis á esquerda

/**
 * Saída:
 *
 * Exemplo de cadea
 * abarcando varias liñas
 * usando a sintaxe nowdoc.
 * $a non se analiza.
 */
 {% endhighlight %}

* [Sintaxe de Nowdoc](https://www.php.net/language.types.string#language.types.string.syntax.nowdoc)

#### Sintaxe de Heredoc

A sintaxe de Heredoc compórtase internamente do mesmo xeito que as comiñas dobres, agás que é axeitada para o uso de cadeas de varias liñas sen necesidade de concatenación.

{% highlight php %}
<?php
$a = 'Variables';

$str = <<<EOD               // initialized by <<<
Example of string
spanning multiple lines
using heredoc syntax.
$a será analizado
EOD;                        // O peche de 'EOD' debe estar na súa propia liña e no punto máis á esquerda

/**
 * Saída:
 *
 * Exemplo de cadea
 * abarcando varias liñas
 * usando a sintaxe heredoc.
 * As variables se analizan.
 */
 {% endhighlight %}

* [Sib¡ntaxe Heredoc](https://www.php.net/language.types.string#language.types.string.syntax.heredoc)

> Cómpre sinalar que as cadeas multilínea tamén se poden formar continuándoas a través de varias liñas nunha sentenza. _e.g._

{% highlight php %}
$str = "
Example of string
spanning multiple lines
using statement syntax.
$a are parsed.
";

/**
 * Saída:
 *
 * Exemplo de cadea
 * abarcando varias liñas
 * usando a sintaxe das sentenzas.
 * As variables se analizan.
 */
 {% endhighlight %}

### Que é máis rápido?

Circula o mito de que as cadeas entre comiñas simples son lixeiramente máis rápidas que as cadeas entre comiñas dobres. Isto non é certo en absoluto.

Se estás a definir unha única cadea de texto e non intentas concatenar valores nin nada complicado, entón unha cadea de texto entre comiñas simples ou dobres será completamente idéntica. Ningunha das dúas é máis rápida.

Se estás a concatenar varias cadeas de calquera tipo ou interpolar valores nunha cadea entre comiñas dobres, os resultados poden variar. Se estás a traballar cun pequeno número de valores, a concatenación é lixeiramente máis rápida. Con moitos valores, a interpolación é lixeiramente máis rápida.

Independentemente do que esteas a facer coas cadeas, ningún dos tipos terá ningún impacto notable na túa
aplicación. Tentar reescribir código para usar un ou outro sempre é un exercicio inútil, polo que debes evitar esta
microoptimización a menos que realmente comprendas o significado e o impacto das diferenzas.

* [Desmentindo o mito do rendemento das comiñas simples](https://www.npopov.com/2012/01/09/Disproving-the-Single-Quotes-Performance-Myth.html)

## Operadores ternarios

Os operadores ternarios son unha boa maneira de condensar código, pero adoitan usarse en exceso. Aínda que os operadores ternarios poden apilarse/aniñarse, recoméndase usar un por liña para maior lexibilidade.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';
{% endhighlight %}

En comparación, aquí tes un exemplo que sacrifica todas as formas de lexibilidade para reducir o número de liñas.

{% highlight php %}
<?php
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // aniñamento excesivo, sacrificando a lexibilidade
{% endhighlight %}

Para devolver - 'return'- un valor con operadores ternarios, use a sintaxe correcta.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // este exemplo mostrará un erro

// vs

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // este exemplo devolverá 'yay'

{% endhighlight %}

Cómpre sinalar que non é necesario usar un operador ternario para devolver un valor booleano. Un exemplo disto sería:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? true : false; // Devolverá true se $a == 3 ou false

// vs

$a = 3;
return $a == 3; // Devolverá true se $a == 3 ou false

{% endhighlight %}

Isto tamén se pode dicir para todas as operacións (===, !==, !=, == etc).

#### Uso de parénteses con operadores ternarios para form e function

Ao empregar un operador ternario, os corchetes poden contribuír a mellorar a lexibilidade do código e tamén a incluír unións dentro de bloques de instrucións. Un exemplo de cando non é necesario usar corchetes é:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? "yay" : "nope"; // devolve yay se $a == 3 ou nope

// vs

$a = 3;
return $a == 3 ? "yay" : "nope"; // devolve yay se $a == 3 ou nope
{% endhighlight %}

A inclusión de corchetes tamén nos permite crear unións dentro dun bloque de instrucións onde o bloque se comprobará
no seu conxunto. Como neste exemplo, que devolverá verdadeiro se ambos (`$a == 3` e `$b == 4`) son verdadeiros e `$c == 5` amén é true.

{% highlight php %}
<?php
return ($a == 3 && $b == 4) && $c == 5;
{% endhighlight %}

Outro exemplo é o fragmento de código que aparece a continuación, que devolverá verdadeiro se ($a != 3 AND $b != 4) OR $c == 5.

{% highlight php %}
<?php
return ($a != 3 && $b != 4) || $c == 5;
{% endhighlight %}

Desde​ PHP 5.3, é posible omitir a parte central do operador ternario.
Expresión​  "expr1 ?: expr3" devolve expr1 se expr1 se avalía a TRUE, e expr3 en caso contrario.

* [Operadores ternarios](https://www.php.net/language.operators.comparison)
