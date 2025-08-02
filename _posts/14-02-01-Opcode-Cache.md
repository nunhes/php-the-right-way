---
isChild: true
anchor:  opcode_cache
---

## Caché de Opcode {#opcode_cache_title}

Cando un arquivo PHP é executado, debe primeiro ser compilado en [opcodes](https://php-legacy-docs.zend.com/manual/php4/en/internals2.opcodes) (instrucións de linguaxe de máquina para a CPU). Se o código fonte non cambiou, os opcodes serán os mesmos, polo que este paso de compilación convértese nun desperdicio de recursos da CPU.

Un caché de opcode prevén a compilación redundante almacenando opcodes en memoria e reutilizándoos en chamadas sucesivas. Tipicamente verificará a sinatura ou tempo de modificación do arquivo primeiro, no caso de que houbese cambios.

É probable que un caché de opcode faga unha mellora significativa de velocidade na túa aplicación. Desde PHP 5.5 hai un integrado - [Zend OPcache][opcache-book]. Dependendo do teu paquete/distribución de PHP, xeralmente está activado por defecto - verifica [opcache.enable](https://www.php.net/manual/opcache.configuration.php#ini.opcache.enable) e a saída de `phpinfo()` para asegurar. Para versións anteriores hai unha extensión PECL.

Ler máis sobre cachés de opcode:

* [Zend OPcache][opcache-book] (incluído con PHP desde 5.5)
* Zend OPcache (anteriormente coñecido como Zend Optimizer+) agora é [código aberto][Zend Optimizer+]
* [WinCache] (extensión para MS Windows Server)
* [lista de aceleradores PHP en Wikipedia][PHP_accelerators]
* [Precarga PHP] - PHP >= 7.4


[opcache-book]: https://www.php.net/book.opcache
[Zend Optimizer+]: https://github.com/zendtech/ZendOptimizerPlus
[WinCache]: https://www.iis.net/downloads/microsoft/wincache-extension
[PHP_accelerators]: https://wikipedia.org/wiki/List_of_PHP_accelerators
[PHP Preloading]: https://www.php.net/opcache.preloading
