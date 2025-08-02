---
isChild: true
anchor:  test_driven_development
---

## Desenvolvemento Dirixido por Probas {#test_driven_development_title}

Desde [Wikipedia](https://wikipedia.org/wiki/Test-driven_development):

> O desenvolvemento dirixido por probas (TDD) é un proceso de desenvolvemento de software que depende da repetición dun ciclo de desenvolvemento moi curto:
> primeiro o desenvolvedor escribe un caso de proba automatizado que falla que define unha mellora desexada ou nova
> función, entón produce código para pasar esa proba e finalmente refactoriza o novo código a estándares aceptábeis. Kent Beck,
> a quen se lle acredita ter desenvolvido ou 'redescubrido' a técnica, declarou en 2003 que TDD fomenta deseños
> simples e inspira confianza.

Hai varios tipos diferentes de probas que podes facer para a túa aplicación:

### Probas Unitarias

As Probas Unitarias son un enfoque de programación para asegurar que funcións, clases e métodos están funcionando como esperado, desde o punto
en que os constrúes todo o camiño a través do ciclo de desenvolvemento. Ao verificar valores que entran e saen de varias funcións e
métodos, podes asegurar que a lóxica interna está funcionando correctamente. Ao usar Inxección de Dependencias e construír clases "mock"
e stubs podes verificar que as dependencias son usadas correctamente para unha mellor cobertura de probas.

Cando creas unha clase ou función deberías crear unha proba unitaria para cada comportamento que debe ter. A un nivel moi básico
deberías asegurar que dá erro se lle envías argumentos malos e asegurar que funciona se lle envías argumentos válidos. Isto
axudará a asegurar que cando fagas cambios a esta clase ou función máis tarde no ciclo de desenvolvemento que a funcionalidade antiga
continúa funcionando como esperado. A única alternativa a isto sería `var_dump()` nun test.php, que non é forma de construír unha aplicación - grande ou pequena.

O outro uso para as probas unitarias é contribuír ao código aberto. Se podes escribir unha proba que mostre funcionalidade rota
(é dicir, falla), entón arranxala, e mostra a proba pasando, os parches son moito máis propensos a ser aceptados. Se executas un proxecto
que acepta pull requests entón deberías suxerir isto como un requisito.

[PHPUnit](https://phpunit.de/) é o framework de probas de facto para escribir probas unitarias para aplicacións PHP, pero hai
varias alternativas:

* [atoum](https://github.com/atoum/atoum)
* [Kahlan](https://github.com/kahlan/kahlan)
* [Peridot](https://peridot-php.github.io/)
* [Pest](https://pestphp.com/)
* [SimpleTest](https://github.com/simpletest/simpletest)

### Probas de Integración

Desde [Wikipedia](https://wikipedia.org/wiki/Integration_testing):

> As probas de integración (ás veces chamadas Integración e Proba, abreviado "I&T") é a fase na proba de software na
> cal módulos individuais de software son combinados e probados como un grupo. Ocorre despois das probas unitarias e antes das
> probas de validación. As probas de integración toman como entrada módulos que foron probados unitariamente, agrúpanos en agregados máis grandes,
> aplican probas definidas nun plan de proba de integración a eses agregados, e entregan como saída o
> sistema integrado listo para probas de sistema.

Moitas das mesmas ferramentas que poden ser usadas para probas unitarias poden ser usadas para probas de integración xa que moitos dos mesmos
principios son usados.

### Probas Funcionais

Ás veces tamén coñecidas como probas de aceptación, as probas funcionais consisten en usar ferramentas para crear probas automatizadas que
realmente usan a túa aplicación en lugar de só verificar que unidades individuais de código están comportándose correctamente e que
unidades individuais poden falar entre si correctamente. Estas ferramentas tipicamente traballan usando datos reais e simulando usuarios
reais da aplicación.

#### Ferramentas de Proba Funcional

* [Codeception](https://codeception.com/) é un framework de probas de stack completo que inclúe ferramentas de proba de aceptación
* [Cyress](https://www.cypress.io/)
* [Mink](https://mink.behat.org/)
* [Selenium](https://www.selenium.dev/)
* [Storyplayer](https://github.com/MeltwaterArchive/storyplayer) é un framework de probas de stack completo que inclúe soporte para crear e destruír ambientes de proba baixo demanda
