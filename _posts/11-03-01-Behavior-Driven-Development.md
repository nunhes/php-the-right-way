---
isChild: true
anchor:  behavior_driven_development
---

## Desenvolvemento Dirixido por Comportamento {#behavior_driven_development_title}

Hai dous tipos diferentes de Desenvolvemento Dirixido por Comportamento (BDD): SpecBDD e StoryBDD. SpecBDD enfócase no comportamento
técnico do código, mentres que StoryBDD enfócase en comportamentos ou interaccións de negocio ou funcionalidades. PHP ten frameworks para ambos
tipos de BDD.

Con StoryBDD, escribes historias lexíbeis por humanos que describen o comportamento da túa aplicación. Estas historias poden entón
ser executadas como probas reais contra a túa aplicación. O framework usado en aplicacións PHP para StoryBDD é [Behat], que
está inspirado no proxecto [Cucumber] de Ruby e implementa o DSL Gherkin para describir o comportamento das funcionalidades.

Con SpecBDD, escribes especificacións que describen como o teu código real debería comportarse. En lugar de probar unha función
ou método, estás describindo como esa función ou método debería comportarse. PHP ofrece o framework [PHPSpec] para este
propósito. Este framework está inspirado no proxecto [RSpec][Rspec] para Ruby.

### Enlaces BDD

* [Behat], o framework StoryBDD para PHP, inspirado no proxecto [Cucumber] de Ruby;
* [PHPSpec], o framework SpecBDD para PHP, inspirado no proxecto [RSpec] de Ruby;
* [Codeception] é un framework de probas de stack completo que usa principios BDD.


[Behat]: https://behat.org/
[Cucumber]: https://cucumber.io/
[PHPSpec]: https://phpspec.net/
[RSpec]: https://rspec.info/
[Codeception]: https://codeception.com/
