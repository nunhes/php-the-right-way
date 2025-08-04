---
title: Modelos PHP sinxelos
isChild: true
anchor:  plain_php_templates
---

## Modelos PHP sinxelos {#plain_php_templates_title}

Os modelos PHP sinxelos son simplemente modelos que usan código PHP nativo. Son unha elección natural xa que PHP é en realidade unha
linguaxe de modelos en si mesma. Iso simplemente significa que podes combinar código PHP dentro doutro código, como HTML. Isto é
beneficioso para os desenvolvedores de PHP xa que non hai que aprender unha nova sintaxe, coñecen as funcións dispoñibles para eles e os seus
editores de código xa teñen incorporado o resaltado de sintaxe PHP e o autocompletado. Ademais, os modelos PHP sinxelos tenden a ser
moi rápidos xa que non se require ningunha etapa de compilación.

Todos os frameworks PHP modernos empregan algún tipo de sistema de modelos, a maioría dos cales usan PHP simple por defecto. Fóra dos
frameworks, librarías como [Plates][plates] ou [Aura.View][aura] facilitan o traballo con modelos PHP simples ao
ofrecer funcionalidades de modelos modernas como herdanza, deseños e extensións.

### Exemplo simple de un modelo PHP 

Usando a libraría [Plates][plates].

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}

### Exemplo de plantilla PHP sinxel usando herencia

Usando a libraría [Plates][plates].

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
{% endhighlight %}


[plates]: https://platesphp.com/
[aura]: https://github.com/auraphp/Aura.View
