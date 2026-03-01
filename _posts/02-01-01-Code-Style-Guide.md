---
title: Guía de estilo de código
anchor: code_style_guide
---

# Guía de estilo de código {#code_style_guide_title}

A comunidade PHP é grande e diversa, composta por innumerables librarías, frameworks e compoñentes. É común que os desenvolvedores de PHP elixan varios destes e os combinen nun único proxecto. É importante que o código PHP adhira (o máis próximo posible) a un estilo de código común para facilitar aos desenvolvedores mesturar e combinar varias librarías para os seus proxectos.

O [Framework Interop Group][fig] propuxo e aprobou unha serie de recomendacións de estilo. Non todas elas están relacionadas co estilo de código, pero as que o están son [PSR-1][psr1], [PSR-12][psr12], [PSR-4][psr4] e [PER Coding Style][per-cs]. Estas recomendacións son meramente un conxunto de regras que moitos proxectos como Drupal, Zend, Symfony, Laravel, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium, etc. están adoptando. Podes usalas para os teus propios proxectos, ou continuar usando o teu propio estilo persoal.

Idealmente, deberías escribir código PHP que adhira a un estándar coñecido. Isto podería ser calquera combinación de PSRs, ou un dos estándares de codificación feitos por PEAR ou Zend. Isto significa que outros desenvolvedores poden ler e traballar facilmente co teu código, e as aplicacións que implementan os compoñentes poden ter consistencia mesmo cando traballan con moito código de terceiros.

* [Ler sobre PSR-1][psr1]
* [Ler sobre PSR-12][psr12]
* [Ler sobre PSR-4][psr4]
* [Ler sobre PER Coding Style][per-cs]
* [Ler sobre PEAR Coding Standards][pear-cs]
* [Ler sobre Symfony Coding Standards][symfony-cs]

Podes usar [PHP_CodeSniffer][phpcs] para verificar o código contra calquera unha destas recomendacións, e plugins para editores de texto como [Sublime Text][st-cs] para recibir retroalimentación en tempo real.

Podes arranxar o layout do código automaticamente usando unha das seguintes ferramentas:

- Unha é o [PHP Coding Standards Fixer][phpcsfixer] que ten unha base de código moi ben probada.
- Tamén, a ferramenta [PHP Code Beautifier and Fixer][phpcbf] que está incluída con PHP_CodeSniffer pode ser usada para axustar o teu código en consecuencia.

E podes executar phpcs manualmente desde o shell:

    phpcs -sw --standard=PSR1 file.php

Mostrará erros e describirá como arranxalos.
Tamén pode ser útil incluír o comando `phpcs` nun hook pre-commit de git co argumento CLI `--filter=GitStaged`.
Dese xeito, o código que contén violacións contra o estándar elixido non pode entrar no repositorio ata que esas violacións foron arranxadas.

Se tes PHP_CodeSniffer, entón podes arranxar os problemas de layout do código reportados por el, automaticamente, co [PHP Code Beautifier and Fixer][phpcbf].

    phpcbf -w --standard=PSR1 file.php

Outra opción é usar o [PHP Coding Standards Fixer][phpcsfixer].
Mostrará que tipo de erros tiña a estrutura do código antes de arranxalos.

    php-cs-fixer fix -v --rules=@PSR1 file.php

O inglés é preferido para todos os nomes de símbolos e infraestrutura de código. Os comentarios poden ser escritos en calquera idioma facilmente lexible por todas as partes actuais e futuras que poden estar a traballar na base de código.

Finalmente, un bo recurso complementario para escribir código PHP limpo é [Clean Code PHP][cleancode].

[fig]: https://www.php-fig.org/
[psr1]: https://www.php-fig.org/psr/psr-1/
[psr12]: https://www.php-fig.org/psr/psr-12/
[psr4]: https://www.php-fig.org/psr/psr-4/
[per-cs]: https://www.php-fig.org/per/coding-style/
[pear-cs]: https://pear.php.net/manual/en/standards.php
[symfony-cs]: https://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: https://github.com/PHPCSStandards/PHP_CodeSniffer
[phpcbf]: https://github.com/PHPCSStandards/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: https://cs.symfony.com/
[cleancode]: https://github.com/jupeter/clean-code-php
