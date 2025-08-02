---
title:   Servidores Virtuais ou Dedicados
isChild: true
anchor:  virtual_or_dedicated_servers
---

## Servidores Virtuais ou Dedicados {#virtual_or_dedicated_servers_title}

Se estás cómodo coa administración de sistemas, ou estás interesado en aprendela, os servidores virtuais ou dedicados danche
control completo do ambiente de produción da túa aplicación.

### nginx e PHP-FPM

PHP, vía o Xestor de Procesos FastCGI integrado de PHP (FPM), combina realmente ben con [nginx], que é un servidor web lixeiro e
de alto rendemento. Usa menos memoria que Apache e pode manexar mellor máis peticións concurrentes. Isto é
especialmente importante en servidores virtuais que non teñen moita memoria de sobra.

* [Ler máis sobre nginx][nginx]
* [Ler máis sobre PHP-FPM][phpfpm]
* [Ler máis sobre configurar nginx e PHP-FPM de forma segura][secure-nginx-phpfpm]

### Apache e PHP

PHP e Apache teñen unha longa historia xuntos. Apache é tremendamente configurábel e ten moitos [módulos][apache-modules] dispoñíbeis
para estender a funcionalidade. É unha elección popular para servidores compartidos e unha configuración fácil para frameworks PHP
e aplicacións de código aberto como WordPress. Desafortunadamente, Apache usa máis recursos que nginx por defecto e
non pode manexar tantos visitantes ao mesmo tempo.

Apache ten varias configuracións posibles para executar PHP. A máis común e fácil de configurar é o [MPM prefork]
con `mod_php`. Aínda que non é o máis eficiente en memoria, é o máis simple para facer funcionar e usar. Isto é probablemente
a mellor elección se non queres profundizar demasiado nos aspectos de administración do servidor. Nota que se usas
`mod_php` DEBES usar o MPM prefork.

Alternativamente, se queres exprimir máis rendemento e estabilidade de Apache entón podes aproveitar o
mesmo sistema FPM que nginx e executar o [MPM worker] ou [MPM event] con mod_fastcgi ou mod_fcgid. Esta configuración será
significativamente máis eficiente en memoria e moito máis rápida pero é máis traballo para configurar.

Se estás executando Apache 2.4 ou máis recente, podes usar [mod_proxy_fcgi] para obter gran rendemento que é fácil de configurar.

* [Ler máis sobre Apache][apache]
* [Ler máis sobre Módulos Multi-Procesamento][apache-MPM]
* [Ler máis sobre mod_fastcgi][mod_fastcgi]
* [Ler máis sobre mod_fcgid][mod_fcgid]
* [Ler máis sobre mod_proxy_fcgi][mod_proxy_fcgi]
* [Ler máis sobre configurar Apache e PHP-FPM con mod_proxy_fcgi][tutorial-mod_proxy_fcgi]


[nginx]: https://nginx.org/
[phpfpm]: https://www.php.net/install.fpm
[secure-nginx-phpfpm]: https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/
[apache-modules]: https://httpd.apache.org/docs/2.4/mod/
[prefork MPM]: https://httpd.apache.org/docs/2.4/mod/prefork.html
[worker MPM]: https://httpd.apache.org/docs/2.4/mod/worker.html
[event MPM]: https://httpd.apache.org/docs/2.4/mod/event.html
[apache]: https://httpd.apache.org/
[apache-MPM]: https://httpd.apache.org/docs/2.4/mod/mpm_common.html
[mod_fastcgi]: https://blogs.oracle.com/opal/post/php-fpm-fastcgi-process-manager-with-apache-2
[mod_fcgid]: https://httpd.apache.org/mod_fcgid/
[mod_proxy_fcgi]: https://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html
[tutorial-mod_proxy_fcgi]: https://serversforhackers.com/video/apache-and-php-fpm
