---
isChild: true
anchor:  namespaces
---

## Espazos de Nomes {#namespaces_title}

Como se mencionou arriba, a comunidade PHP ten moitos desenvolvedores creando moito código. Isto significa que o código PHP dunha libraría
podería usar o mesmo nome de clase que outra. Cando ambas as librarías son usadas no mesmo espazo de nomes, coliden
e causan problemas.

Os _espazos de nomes_ solucionan este problema. Como se describe no manual de referencia de PHP, os espazos de nomes poden ser comparados a directorios
do sistema operativo que _espacian_ os arquivos; dous arquivos co mesmo nome poden coexistir en directorios separados. Do mesmo xeito,
dúas clases PHP co mesmo nome poden coexistir en espazos de nomes PHP separados. É tan simple como iso.

É importante para ti espaziar o teu código para que poida ser usado por outros desenvolvedores sen medo de colidir
con outras librarías.

Unha forma recomendada de usar espazos de nomes está esbozada en [PSR-4][psr4], que pretende proporcionar un estándar de arquivo, clase e
convención de espazo de nomes para permitir código plug-and-play.

En outubro de 2014 o PHP-FIG deprecou o estándar anterior de autoloading: [PSR-0][psr0]. Tanto PSR-0 como PSR-4 son aínda perfectamente usables. O último require PHP 5.3, polo que moitos proxectos só PHP 5.2 implementan PSR-0.

Se vas usar un estándar de autoloader para unha nova aplicación ou paquete, mira PSR-4.

* [Ler sobre Espazos de Nomes][namespaces]
* [Ler sobre PSR-0][psr0]
* [Ler sobre PSR-4][psr4]


[namespaces]: https://www.php.net/language.namespaces
[psr0]: https://www.php-fig.org/psr/psr-0/
[psr4]: https://www.php-fig.org/psr/psr-4/
