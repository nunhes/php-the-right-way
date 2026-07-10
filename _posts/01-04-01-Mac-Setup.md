---
title: Configurar en Mac
isChild: true
anchor:  mac_setup
---

## Configuración de macOS {#mac_setup_title}

macOS 12 (Monterey) e versións posteriores non veñen con PHP preinstalado. As versións anteriores de macOS inclúen PHP pero están atrasadas respecto á versión estable máis recente. Hai múltiples formas de instalar a versión máis recente de PHP en macOS.

### Instalar PHP via Homebrew

[Homebrew] é un xestor de paquetes para macOS que che axuda a instalar PHP e varias extensións facilmente. O repositorio principal de Homebrew proporciona "fórmulas" para PHP 8.1, 8.2, 8.3, 8.4 and 8.5. Instala a versión máis recente con este comando:

```
brew install php
```

Podes cambiar entre versións de PHP de Homebrew modificando a túa variable `PATH`. Alternativamente, podes usar [brew-php-switcher][brew-php-switcher] para cambiar versións de PHP automaticamente.

Tamén podes cambiar entre versións de PHP manualmente desvinculando e vinculando a versión desexada:

```
brew unlink php
brew link --overwrite php@8.2
```

```
brew unlink php
brew link --overwrite php@8.3
```

### Instalar PHP via Macports

O Proxecto [MacPorts] é unha iniciativa da comunidade de código aberto para deseñar un
sistema fácil de usar para compilar, instalar e actualizar software
de código aberto baseado en liña de comandos, X11 ou Aqua no sistema operativo
macOS.

MacPorts soporta binarios precompilados, polo que non necesitas recompilar cada
dependencia desde os arquivos tar.gz de código fonte, salva a túa vida se non
tes ningún paquete instalado no teu sistema.

Neste punto, podes instalar `php54`, `php55`, `php56`, `php70`, `php71`, `php72`, `php73`, `php74`, `php80`, `php81`, `php82`, `php83` ou `php84` usando o comando `port install`, por exemplo:

    sudo port install php74
    sudo port install php83

E podes executar o comando `select` para cambiar o teu PHP activo:

    sudo port select --set php php83

### Instalar PHP via phpbrew

[phpbrew] é unha ferramenta para instalar e xestionar múltiples versións de PHP. Isto pode ser realmente útil se dúas aplicacións/proxectos
diferentes requiren diferentes versións de PHP, e non estás usando máquinas virtuais.

### Instalar PHP via o instalador binario de Liip

Outra opción popular é [php-osx.liip.ch] que proporciona métodos de instalación dunha liña para versións 5.3 ata 7.3.
Non sobrescribe os binarios de PHP instalados por Apple, senón que instala todo nunha localización separada (/usr/local/php5).

### Compilar desde o Código Fonte

Outra opción que che dá control sobre a versión de PHP que instalas, é [compilalo ti mesmo][mac-compile].
Nese caso asegúrate de ter instalado [Xcode][xcode-gcc-substitution] ou o substituto de Apple
["Command Line Tools for XCode"] descargable desde o Centro de Desenvolvedores de Apple.

### Instaladores Todo-en-Un

As solucións listadas arriba principalmente manexan PHP en si, e non proporcionan cousas como [Apache][apache], [Nginx][nginx] ou un servidor SQL.
As solucións "todo-en-un" como [MAMP][mamp-downloads] e [XAMPP][xampp] instalarán estes outros bits de software para
ti e os conectarán todos xuntos, pero a facilidade de configuración vén cun trade-off de flexibilidade.

[Homebrew]: https://brew.sh/
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://web.archive.org/web/20220505163210/https://php-osx.liip.ch/
[mac-compile]: https://www.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[apache]: https://httpd.apache.org/
[nginx]: https://www.nginx.com/
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
