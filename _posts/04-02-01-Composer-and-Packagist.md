---
title:   Composer e Packagist
isChild: true
anchor:  composer_and_packagist
---

## Composer e Packagist {#composer_and_packagist_title}

Composer é o xestor de dependencias recomendado para PHP. Lista as dependencias do teu proxecto nun arquivo `composer.json` e,
con uns poucos comandos simples, Composer descargará automaticamente as dependencias do teu proxecto e configurará o autoloading para
ti. Composer é análogo a NPM no mundo de node.js, ou Bundler no mundo de Ruby.

Hai unha plethora de bibliotecas PHP que son compatibles con Composer e listas para ser usadas no teu proxecto. Estes
"paquetes" están listados en [Packagist], o repositorio oficial para bibliotecas PHP compatibles con Composer.

### Como Instalar Composer

A forma máis segura de descargar composer é [seguindo as instrucións oficiais](https://getcomposer.org/download/).
Isto verificará que o instalador non está corrompido ou manipulado.
O instalador instala un binario `composer.phar` no teu _directorio de traballo actual_.

Recomendamos instalar Composer *globalmente* (ex. unha única copia en `/usr/local/bin`). Para facelo, executa este comando a continuación:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Nota:** Se o anterior falla debido a permisos, prefixa con `sudo`.

Para executar un Composer instalado localmente usarías `php composer.phar`, globalmente é simplemente `composer`.

#### Instalando en Windows

Para usuarios de Windows a forma máis fácil de comezar é usar o instalador [ComposerSetup], que
realiza unha instalación global e configura o teu `$PATH` para que poidas simplemente chamar `composer` desde calquera
directorio na túa liña de comandos.

### Como Definir e Instalar Dependencias

Composer mantén un rexistro das dependencias do teu proxecto nun arquivo chamado `composer.json`. Podes xestionalo
manualmente se queres, ou usar o propio Composer. O comando `composer require` engade unha dependencia do proxecto
e se non tes un arquivo `composer.json`, un será creado. Aquí hai un exemplo que engade [Twig]
como unha dependencia do teu proxecto.

{% highlight console %}
composer require twig/twig:^2.0
{% endhighlight %}

Alternativamente, o comando `composer init` guiaráche a través da creación dun arquivo `composer.json` completo
para o teu proxecto. De calquera forma, unha vez que creaches o teu arquivo `composer.json` podes dicirlle a Composer que
descargue e instale as túas dependencias no directorio `vendor/`. Isto tamén se aplica a proxectos
que descargaches que xa proporcionan un arquivo `composer.json`:

{% highlight console %}
composer install
{% endhighlight %}

A continuación, engade esta liña ao arquivo PHP principal da túa aplicación; isto lle dirá a PHP que use o autoloader
de Composer para as dependencias do teu proxecto.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Agora podes usar as dependencias do teu proxecto, e serán autoloaded a demanda.

### Actualizando as túas dependencias

Composer crea un arquivo chamado `composer.lock` que almacena a versión exacta de cada paquete que
descargou cando executaste por primeira vez `composer install`. Se compartes o teu proxecto con outros,
asegúrate de que o arquivo `composer.lock` está incluído, para que cando eles executem `composer install` obteñan
as mesmas versións que ti. Para actualizar as túas dependencias, executa `composer update`. Non uses
`composer update` cando desplegues, só `composer install`, doutra forma poderías acabar con diferentes
versións de paquetes en produción.

Isto é máis útil cando defines os teus requisitos de versión de forma flexible. Por exemplo, un requisito de versión
de `~1.8` significa "calquera cousa máis nova que `1.8.0`, pero menos que `2.0.x-dev`". Tamén podes usar
o comodín `*` como en `1.8.*`. Agora o comando `composer update` de Composer actualizará todas as túas
dependencias á versión máis nova que se axuste ás restriccións que defines.

### Notificacións de Actualización

Para recibir notificacións sobre novas versións podes rexistrarte en [libraries.io], un servizo web
que pode monitorizar dependencias e enviarche alertas sobre actualizacións.

### Verificando as túas dependencias para problemas de seguridade

O [Local PHP Security Checker] é unha ferramenta de liña de comandos, que examinará o teu arquivo `composer.lock`
e che dirá se necesitas actualizar algunha das túas dependencias.

### Manejando dependencias globais con Composer

Composer tamén pode manexar dependencias globais e os seus binarios. O uso é directo, todo o que necesitas
facer é prefixar o teu comando con `global`. Se por exemplo quixeras instalar PHPUnit e telo
dispoñible globalmente, executarías o seguinte comando:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

Isto creará unha carpeta `~/.composer` onde residen as túas dependencias globais. Para ter os binarios dos paquetes
instalados dispoñibles en todas partes, entón engadirías a carpeta `~/.composer/vendor/bin` á túa
variable `$PATH`.

* [Aprender sobre Composer]

[Packagist]: https://packagist.org/
[Twig]: https://twig.symfony.com/
[libraries.io]: https://libraries.io/
[Local PHP Security Checker]: https://github.com/fabpot/local-php-security-checker
[Learn about Composer]: https://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
