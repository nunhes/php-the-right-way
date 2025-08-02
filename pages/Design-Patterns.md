---
layout: page
title:  Patróns de Deseño
sitemap: true
---

# Patróns de Deseño

Hai numerosas formas de estruturar o código e o proxecto para a túa aplicación web, e podes empregar máis ou menos esforzo na súa arquitectura. Non obstante, adoita ser unha boa idea seguir patróns comúns xa que fan que o teu código sexa máis doado de xestionar e máis sinxelo de entender para outros.

* [Patrón arquitectónico en Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Patrón de deseño de software en Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Colección de exemplos de implementación](https://designpatternsphp.readthedocs.io/en/latest/)

## Fábrica (Factory)

Un dos patróns de deseño máis empregados é o patrón fábrica. Neste patrón, unha clase simplemente crea o obxecto que desexas usar. Considera o seguinte exemplo do patrón fábrica:

{% highlight php %}
<?php
class Automobile
{
    private $vehicleMake;
    private $vehicleModel;

    public function __construct($make, $model)
    {
        $this->vehicleMake = $make;
        $this->vehicleModel = $model;
    }

    public function getMakeAndModel()
    {
        return $this->vehicleMake . ' ' . $this->vehicleModel;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// have the factory create the Automobile object
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->getMakeAndModel()); // outputs "Bugatti Veyron"
{% endhighlight %}

Este código usa unha fábrica para crear o obxecto Automobile. Hai dous posibles beneficios ao construír o teu código desta forma; o primeiro é que se necesitas cambiar, renomear ou substituír a clase Automobile máis adiante, só terás que modificar o código na fábrica, en vez de en cada lugar do teu proxecto onde se use a clase Automobile. O segundo beneficio posible é que, se crear o obxecto é un traballo complicado, podes facer todo o traballo na fábrica en vez de repetilo cada vez que queiras crear unha nova instancia.

Usar o patrón fábrica non sempre é necesario (ou sabio). O código de exemplo empregado aquí é tan sinxelo que unha fábrica simplemente estaría engadindo complexidade innecesaria. Non obstante, se estás a facer un proxecto bastante grande ou complexo, podes aforrarte moitos problemas no futuro usando fábricas.

* [Patrón Fábrica en Wikipedia](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

Cando se deseñan aplicacións web, a miúdo ten sentido conceptual e arquitectónicamente permitir o acceso a unha e só unha instancia dunha clase en particular. O patrón singleton permítenos facer isto.

**TODO: NOVO EXEMPLO NECESARIO DE CÓDIGO SINGLETON**

O código anterior implementa o patrón singleton usando unha variable [*estática*](https://www.php.net/language.variables.scope#language.variables.scope.static) e o método de creación estático `getInstance()`.
Observa o seguinte:

* O construtor [`__construct()`](https://www.php.net/language.oop5.decon#object.construct) está declarado como protexido para
impedir a creación dunha nova instancia fóra da clase mediante o operador `new`.
* O método máxico [`__clone()`](https://www.php.net/language.oop5.cloning#object.clone) está declarado como privado para impedir
que se clone unha instancia da clase mediante o operador [`clone`](https://www.php.net/language.oop5.cloning).
* O método máxico [`__wakeup()`](https://www.php.net/language.oop5.magic#object.wakeup) está declarado como privado para impedir
a deserialización dunha instancia da clase mediante a función global [`unserialize()`](https://www.php.net/function.unserialize).
* Crese unha nova instancia mediante [enlace estático en tempo de execución](https://www.php.net/language.oop5.late-static-bindings) no método de creación estático `getInstance()` coa palabra chave `static`. Isto permite a herdanza da clase `Singleton` no exemplo.

O patrón singleton é útil cando necesitamos asegurarnos de que só temos unha única instancia dunha clase durante todo o ciclo de vida dunha petición nunha aplicación web. Isto ocorre normalmente cando temos obxectos globais (como unha clase de Configuración) ou un recurso compartido (como unha cola de eventos).

Debes ter coidado ao usar o patrón singleton, xa que pola súa propia natureza introduce estado global na túa aplicación, reducindo a súa capacidade de proba. Na maioría dos casos, a inxección de dependencias pode (e debería) usarse no canto dunha clase singleton. Usar inxección de dependencias significa que non introducimos acoplamento innecesario no deseño da nosa aplicación, xa que o obxecto que usa o recurso compartido ou global non require coñecemento dunha clase definida concretamente.

* [Patrón Singleton en Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Estratexia (Strategy)

Co patrón estratexia encapsulas familias específicas de algoritmos permitindo que a clase cliente responsable de instanciar un algoritmo particular non teña coñecemento da implementación real. Hai varias variacións do patrón estratexia, a máis simple das cales se describe a continuación:

Este primeiro fragmento de código describe unha familia de algoritmos; podes querer un array serializado, algún JSON ou simplemente un array de datos:

{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

Ao encapsular os algoritmos anteriores estás facendo que o teu código sexa claro e permitindo que outros desenvolvedores poidan engadir facilmente novos tipos de saída sen afectar o código cliente.

Verás como cada clase 'output' concreta implementa unha OutputInterface - isto serve para dous propósitos: principalmente proporciona un contrato simple que debe ser cumprido por calquera nova implementación concreta. En segundo lugar, ao implementar unha interface común, verás na seguinte sección que agora podes utilizar [Type Hinting](https://www.php.net/language.oop5.typehinting) para asegurarte de que o cliente que está utilizando estes comportamentos é do tipo correcto, neste caso 'OutputInterface'.

O seguinte fragmento de código describe como unha clase cliente que fai a chamada podería usar un destes algoritmos e incluso mellor, establecer o comportamento requirido en tempo de execución:

{% highlight php %}
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

A clase cliente que fai a chamada ten unha propiedade privada que debe ser establecida en tempo de execución e ser do tipo 'OutputInterface'.
Unha vez que esta propiedade está definida, unha chamada a loadOutput() chamará ao método load() na clase concreta do tipo de saída que se estableceu.

{% highlight php %}
<?php
$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Patrón Estratexia en Wikipedia](https://en.wikipedia.org/wiki/Strategy_pattern)

## Controlador Frontal (Front Controller)

O patrón de controlador frontal é cando tes un único punto de entrada para a túa aplicación web (por exemplo, index.php) que xestiona todas as peticións. Este código é responsable de cargar todas as dependencias, procesar a petición e enviar a resposta ao navegador. O patrón de controlador frontal pode ser beneficioso porque fomenta o código modular e proporciona un lugar central para engadir código que debe executarse para cada petición (como a desinfección de entrada).

* [Patrón Controlador Frontal en Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Modelo-Vista-Controlador (MVC)

O patrón modelo-vista-controlador (MVC) e os seus parentes HMVC e MVVM permítenche dividir o código en obxectos lóxicos
que serven a propósitos moi específicos. Os modelos serven como unha capa de acceso a datos onde se obteñen e devolven datos en formatos utilizables en toda a túa aplicación. Os controladores xestionan a petición, procesan os datos devoltos polos modelos e cargan as vistas para envialas na resposta. E as vistas son modelos de visualización (marcado, XML, etc.) que se envían na resposta ao navegador web.

MVC é o patrón arquitectónico máis común utilizado nos [frameworks PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks) máis populares.

Aprende máis sobre MVC e as súas variantes:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
