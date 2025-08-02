---
isChild: true
title:   Capas de abstracción
anchor:  databases_abstraction_layers
---

## Capas de abstracción {#databases_abstraction_layers_title}

Moitos marcos de traballo proporcionan a súa propia capa de abstracción que pode ou non estar enriba de [PDO][1]. Estes a miúdo emulan características para un sistema de bases de datos que faltan noutro envolvendo as túas consultas en métodos PHP, dándoche
unha abstracción real da base de datos en lugar de só a abstracción de conexión que proporciona PDO. Isto, por suposto, engadirá
un pouco de sobrecarga, pero se estás a crear unha aplicación portátil que necesita funcionar con MySQL, PostgreSQL e SQLite
entón un pouco de sobrecarga pagará a pena polo ben da limpeza do código.

Algunhas capas de abstracción foron construídas usando os estándares de espazo de nomes [PSR-0][psr0] ou [PSR-4][psr4], polo que se poden instalar en calquera aplicación que se desexe:

* [Atlas][5]
* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Medoo][8]
* [Propel][7]
* [laminas-db][4]


[1]: https://www.php.net/book.pdo
[2]: https://www.doctrine-project.org/projects/dbal.html
[4]: https://docs.laminas.dev/laminas-db/
[5]: https://atlasphp.io
[6]: https://github.com/auraphp/Aura.Sql
[7]: https://propelorm.org/
[8]: https://medoo.in/
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/
