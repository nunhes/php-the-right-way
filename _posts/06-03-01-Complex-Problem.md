---
title: Problema Complexo
isChild: true
anchor:  complex_problem
---

## Problema Complexo {#complex_problem_title}

Se algunha vez leste sobre Inxección de Dependencias entón probablemente viste os termos *"Inversión de Control"* ou
*"Principio de Inversión de Dependencias"*. Estes son os problemas complexos que a Inxección de Dependencias resolve.

### Inversión de Control

A Inversión de Control é como di, "invertendo o control" dun sistema mantendo o control organizacional completamente
separado dos nosos obxectos. En termos de Inxección de Dependencias, isto significa soltar as nosas dependencias controlando e
instanciándoas noutro lugar do sistema.

Durante anos, os frameworks PHP estiveron logrando Inversión de Control, con todo, a pregunta converteuse en, que parte do control
estamos invertendo, e onde? Por exemplo, os frameworks MVC xeralmente proporcionarían un super obxecto ou controlador base
que outros controladores deben estender para obter acceso ás súas dependencias. Isto **é** Inversión de Control, con todo,
en lugar de soltar dependencias, este método simplemente móveas.

A Inxección de Dependencias permite-nos resolver este problema máis elegantemente só inxectando as dependencias que necesitamos, cando as
necesitamos, sen a necesidade de calquera dependencia codificada a man.

### S.O.L.I.D.

#### Principio de Responsabilidade Única

O Principio de Responsabilidade Única é sobre actores e arquitectura de alto nivel. Afirma que "Unha clase debería ter
só unha razón para cambiar." Isto significa que cada clase debería _só_ ter responsabilidade sobre unha única parte da
funcionalidade proporcionada polo software. O maior beneficio deste enfoque é que permite mellorada
_reutilizabilidade_ do código. Ao deseñar a nosa clase para facer só unha cousa, podemos usala (ou re-usala) en calquera outro programa sen
cambiala.

#### Principio Aberto/Pechado

O Principio Aberto/Pechado é sobre deseño de clases e extensións de funcionalidades. Afirma que "As entidades de software (clases,
módulos, funcións, etc.) deberían estar abertas para extensión, pero pechadas para modificación." Isto significa que deberíamos deseñar
os nosos módulos, clases e funcións dun xeito que cando se necesite unha nova funcionalidade, non deberíamos modificar o noso código
existente senón escribir novo código que será usado polo código existente. Practicamente falando, isto significa que deberíamos escribir
clases que implementen e adhiran a _interfaces_, entón type-hint contra esas interfaces en lugar de clases específicas.

O maior beneficio deste enfoque é que podemos moi facilmente estender o noso código con soporte para algo novo sen
ter que modificar código existente, significando que podemos reducir o tempo de QA, e o risco de impacto negativo na aplicación
é substancialmente reducido. Podemos desplegar novo código, máis rápido, e con máis confianza.

#### Principio de Substitución de Liskov

O Principio de Substitución de Liskov é sobre subtipado e herdanza. Afirma que "As clases fillas nunca deberían romper
as definicións de tipo da clase pai." Ou, nas palabras de Robert C. Martin, "Os subtipos deben ser substituíbles polos seus tipos
base."

Por exemplo, se temos unha interface `FileInterface` que define un método `embed()`, e temos clases `Audio` e `Video`
que ambas implementan a interface `FileInterface`, entón podemos esperar que o uso do método `embed()` sempre
faga a cousa que pretendemos. Se máis tarde creamos unha clase `PDF` ou unha clase `Gist` que implementan a interface `FileInterface`,
xa saberemos e entenderemos que fará o método `embed()`. O maior beneficio deste enfoque
é que temos a capacidade de construír programas flexibles e facilmente configurábeis, porque cando cambiamos un obxecto dun
tipo (ex., `FileInterface`) por outro non necesitamos cambiar nada máis no noso programa.

#### Principio de Segregación de Interfaces

O Principio de Segregación de Interfaces (ISP) é sobre comunicación _lóxica-de-negocio-a-clientes_. Afirma que "Ningún cliente
debería ser forzado a depender de métodos que non usa." Isto significa que en lugar de ter unha única interface monolítica
que todas as clases conformes necesitan implementar, deberíamos en cambio proporcionar un conxunto de interfaces máis pequenas, específicas de concepto
que unha clase conforme implementa unha ou máis.

Por exemplo, unha clase `Car` ou `Bus` estaría interesada nun método `steeringWheel()`, pero unha clase `Motorcycle` ou `Tricycle`
non. Inversamente, unha clase `Motorcycle` ou `Tricycle` estaría interesada nun método `handlebars()`, pero unha
clase `Car` ou `Bus` non. Non hai necesidade de ter todos estes tipos de vehículos implementando soporte tanto para
`steeringWheel()` como para `handlebars()`, polo que deberíamos romper a interface fonte.

#### Principio de Inversión de Dependencias

O Principio de Inversión de Dependencias é sobre eliminar enlaces duros entre clases discretas para que nova funcionalidade poida
ser aproveitada pasando unha clase diferente. Afirma que un debería *"Depender de Abstraccións. Non depender de
concrecións."*. Simplemente posto, isto significa que as nosas dependencias deberían ser interfaces/contratos ou clases abstractas en lugar de
implementacións concretas. Podemos facilmente refactorizar o exemplo anterior para seguir este principio.

{% highlight php %}
<?php
namespace Database;

class Database
{
    public function __construct(protected AdapterInterface $adapter)
    {
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Hai varios beneficios para a clase `Database` agora dependendo dunha interface en lugar dunha concreción.

Considera que estamos a traballar nun equipo e o adaptador está sendo traballado por un colega. No noso primeiro exemplo, teríamos
que esperar por dito colega para rematar o adaptador antes de que poidamos mockearlo adecuadamente para as nosas probas unitarias. Agora
que a dependencia é unha interface/contrato podemos felizmente mockear esa interface sabendo que o noso colega construirá
o adaptador baseado nese contrato.

Un beneficio aínda maior para este método é que o noso código agora é moito máis escalábel. Se un ano máis tarde decidimos
que queremos migrar a un tipo diferente de base de datos, podemos escribir un adaptador que implemente a interface orixinal
e inxecte iso en cambio, non se requiría máis refactorización xa que podemos asegurar que o adaptador segue o contrato
establecido pola interface.
