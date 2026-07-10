---
title: Plantillas Compiladas
isChild: true
anchor:  compiled_templates
---

## Modelos Compilados {#compiled_templates_title}

Aínda que PHP evolucionou converténdose nunha linguaxe madura e orientada a obxectos, [non mellorou moito][article_templating_engines] como
linguaxe de modelado. Os modelos compilados, como [Twig], [Brainy] ou [Smarty]*, cubren esta carencia ofrecendo unha nova sintaxe
deseñada especificamente para modelado. Desde escape automático, até herdanza e estruturas de control simplificadas,
os modelos compilados están pensados para ser máis doados de escribir, máis limpos de ler e máis seguros de usar. Estes modelos poden incluso compartirse entre diferentes linguaxes, sendo [Mustache] un bo exemplo disto. Xa que estes modelos deben ser compilados, hai unha lixeira penalización no rendemento, non obstante é mínima cando se usa unha caché axeitada.

**Aínda que Smarty ofrece escape automático, esta característica NON está activada por defecto.*

### Exemplo sinxelo dun modelo compilado     

Usando a libraría [Twig].

{% highlight html+jinja %}
{% raw %}
{% include 'header.html' with {'title': 'User Profile'} %}

<h1>User Profile</h1>
<p>Hello, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}

### Exemplo de modelos compilados mediante herdanza

Usando a libraría [Twig].

{% highlight html+jinja %}
{% raw %}
// template.html

<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>

<main>
    {% block content %}{% endblock %}
</main>

</body>
</html>
{% endraw %}
{% endhighlight %}

{% highlight html+jinja %}
{% raw %}
// user_profile.html

{% extends "template.html" %}

{% block title %}User Profile{% endblock %}
{% block content %}
    <h1>User Profile</h1>
    <p>Hello, {{ name }}</p>
{% endblock %}
{% endraw %}
{% endhighlight %}


[article_templating_engines]: http://fabien.potencier.org/templating-engines-in-php.html
[Twig]: https://twig.symfony.com/
[Brainy]: https://github.com/box/brainy
[Smarty]: https://www.smarty.net/
[Mustache]: https://mustache.github.io/
