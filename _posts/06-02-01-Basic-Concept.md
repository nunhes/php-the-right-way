---
title: Concepto Básico
isChild: true
anchor:  basic_concept
---

## Concepto Básico {#basic_concept_title}

Podemos demostrar o concepto cun exemplo simple, pero inxenuo.

Aquí temos unha clase `Database` que require un adaptador para falar coa base de datos. Instanciamos o adaptador no
construtor e creamos unha dependencia dura. Isto fai que as probas sexan difíciles e significa que a clase `Database` está moi estreitamente
acoplada ao adaptador.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Este código pode ser refactorizado para usar Inxección de Dependencias e polo tanto soltar a dependencia.
Aquí, inxectamos a dependencia nun construtor e usamos a [promoción de propiedades do construtor][php-constructor-promotion] para que estea dispoñible como unha propiedade a través da clase:

{% highlight php %}
<?php
namespace Database;

class Database
{
    public function __construct(protected MySqlAdapter $adapter)
    {
    }
}

class MysqlAdapter {}
{% endhighlight %}

Agora estamos dando á clase `Database` a súa dependencia en lugar de creala ela mesma. Poderíamos mesmo crear un método
que aceptase un argumento da dependencia e a configurase dese xeito, ou se a propiedade `$adapter` fose `public` poderíamos
configurala directamente.

[php-constructor-promotion]: https://www.php.net/manual/en/language.oop5.decon.php#language.oop5.decon.constructor.promotion
