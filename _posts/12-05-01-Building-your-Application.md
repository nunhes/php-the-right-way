---
title: Construíndo a túa Aplicación
isChild: true
anchor:  building_and_deploying_your_application
---

## Construíndo e Desplegando a túa Aplicación {#building_and_deploying_your_application_title}

Se te atopas facendo cambios manuais no esquema da base de datos ou executando as túas probas manualmente antes de actualizar os teus arquivos
(manual), pensa dúas veces! Con cada tarefa manual adicional necesaria para desplegar unha nova versión da túa aplicación, as posibilidades de
erros potencialmente fatais aumentan. Sexa que estés lidando cunha actualización simple, un proceso de construción completo ou mesmo
unha estratexia de integración continua, a [automatización de construción][buildautomation] é a túa amiga.

Entre as tarefas que podes querer automatizar están:

* Xestión de dependencias
* Compilación, minificación dos teus recursos
* Execución de probas
* Creación de documentación
* Empaquetado
* Despliegue


### Ferramentas de Despliegue

As ferramentas de despliegue poden ser descritas como unha colección de scripts que manexan tarefas comúns do despliegue de software. A ferramenta de despliegue non é parte do teu software, actúa no teu software desde 'fóra'.

Hai moitas ferramentas de código aberto dispoñíbeis para axudarte coa automatización de construción e despliegue, algunhas están escritas en PHP outras non. Isto non debería impedirte usalas, se están mellor axustadas para o traballo específico. Aquí hai algúns exemplos:

[Phing] pode controlar o teu proceso de empaquetado, despliegue ou proba desde dentro dun arquivo de construción XML. Phing (que está baseado en [Apache Ant]) proporciona un rico conxunto de tarefas xeralmente necesarias para instalar ou actualizar unha aplicación web e pode ser estendido con tarefas personalizadas adicionais, escritas en PHP. É unha ferramenta sólida e robusta e existe desde hai moito tempo, con todo a ferramenta podería ser percibida como un pouco antiga debido á forma en que trata coa configuración (arquivos XML).

[Capistrano] é un sistema para *programadores intermedios-a-avanzados* para executar comandos dunha forma estruturada e repetíbel nunha ou máis máquinas remotas. Está pre-configurado para desplegar aplicacións Ruby on Rails, con todo podes desplegar exitosamente sistemas PHP con el. O uso exitoso de Capistrano depende dun coñecemento funcional de Ruby e Rake.

[Ansistrano] é un par de roles de Ansible para xestionar facilmente o proceso de despliegue (desplegar e reverter) para aplicacións de script como PHP, Python e Ruby. É un port de Ansible para [Capistrano]. Xa foi usado por moitas empresas PHP.

[Deployer] é unha ferramenta de despliegue escrita en PHP. É simple e funcional. As funcionalidades inclúen executar tarefas en paralelo, despliegue atómico e manter consistencia entre servidores. Recetas de tarefas comúns para Symfony, Laravel, Zend Framework e Yii están dispoñíbeis. O artigo de Younes Rafie [Despliegue Fácil de Aplicacións PHP con Deployer][phpdeploy_deployer] é un gran tutorial para desplegar a túa aplicación coa ferramenta.

[Magallanes] é outra ferramenta escrita en PHP con configuración simple feita en arquivos YAML. Ten soporte para múltiples servidores e ambientes, despliegue atómico, e ten algunhas tarefas integradas que podes aproveitar para ferramentas e frameworks comúns.

#### Lectura adicional:

* [Automatiza o teu proxecto con Apache Ant][apache_ant_tutorial]
* [Desplegando Aplicacións PHP][deploying_php_applications] - libro de pago sobre mellores prácticas e ferramentas para o despliegue de PHP.

### Provisión de Servidores

Xestionar e configurar servidores pode ser unha tarefa desalentadora cando te enfrontas a moitos servidores. Hai ferramentas para lidar con isto para que poidas automatizar a túa infraestrutura para asegurar que tes os servidores correctos e que están configurados adecuadamente. A miúdo integranse cos maiores provedores de hosting na nube (Amazon Web Services, Heroku, DigitalOcean, etc) para xestionar instancias, o que fai que escalar unha aplicación sexa moito máis fácil.

[Ansible] é unha ferramenta que xestiona a túa infraestrutura a través de arquivos YAML. É simple para comezar e pode xestionar aplicacións complexas e de gran escala. Hai unha API para xestionar instancias na nube e pode xestionalas a través dun inventario dinámico usando certas ferramentas.

[Puppet] é unha ferramenta que ten a súa propia linguaxe e tipos de arquivo para xestionar servidores e configuracións. Pode ser usado nunha configuración mestre/cliente ou pode ser usado nun modo "sen mestre". No modo mestre/cliente os clientes consultarán o(s) mestre(s) central(es) para nova configuración en intervalos establecidos e actualizaranse se é necesario. No modo sen mestre podes empuxar cambios aos teus nodos.

[Chef] é un poderoso framework de integración de sistemas baseado en Ruby co que podes construír todo teu ambiente de servidor ou caixas virtuais. Integrase ben con Amazon Web Services a través do seu servizo chamado OpsWorks.

#### Lectura adicional:

* [Un Tutorial de Ansible][an_ansible_tutorial]
* [Ansible for DevOps][ansible_for_devops] - libro de pago sobre todo Ansible
* [Ansible for AWS][ansible_for_aws] - libro de pago sobre integrar Ansible e Amazon Web Services
* [Serie de blog de tres partes sobre desplegar unha aplicación LAMP con Chef, Vagrant, e EC2][chef_vagrant_and_ec2]
* [Chef Cookbook que instala e configura PHP e o sistema de xestión de paquetes PEAR][Chef_cookbook]
* [Serie de tutorial de vídeo de Chef][Chef_tutorial]

### Integración Continua

> A Integración Continua é unha práctica de desenvolvemento de software onde os membros dun equipo integran o seu traballo frecuentemente,
> xeralmente cada persoa integra polo menos diariamente — levando a múltiples integracións por día. Moitos equipos atopan que este
> enfoque leva a problemas de integración significativamente reducidos e permite a un equipo desenvolver software cohesivo máis
> rapidamente.

*-- Martin Fowler*

Hai diferentes formas de implementar integración continua para PHP. [Travis CI] fixo un gran traballo de
facer a integración continua unha realidade mesmo para proxectos pequenos. Travis CI é un servizo de integración continua hospedado.
Pode ser integrado con GitHub e ofrece soporte para moitas linguaxes incluíndo PHP.
GitHub ten fluxos de traballo de integración continua con [GitHub Actions][github_actions].

#### Lectura adicional:

* [Integración Continua con Jenkins][Jenkins]
* [Integración Continua con PHPCI][PHPCI]
* [Integración Continua con PHP Censor][PHP Censor]
* [Integración Continua con Teamcity][Teamcity]

[buildautomation]: https://wikipedia.org/wiki/Build_automation
[Phing]: https://www.phing.info/
[Apache Ant]: https://ant.apache.org/
[Capistrano]: https://capistranorb.com/
[Ansistrano]: https://ansistrano.com
[phpdeploy_deployer]: https://www.sitepoint.com/deploying-php-applications-with-deployer/
[Chef]: https://www.chef.io/
[chef_vagrant_and_ec2]: https://web.archive.org/web/20190307220000/http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/
[Chef_cookbook]: https://github.com/sous-chefs/php
[Chef_tutorial]: https://www.youtube.com/playlist?list=PL11cZfNdwNyNYcpntVe6js-prb80LBZuc
[apache_ant_tutorial]: https://code.tutsplus.com/tutorials/automate-your-projects-with-apache-ant--net-18595
[Travis CI]: https://www.travis-ci.com/
[Jenkins]: https://jenkins.io/
[PHPCI]: https://github.com/dancryer/phpci
[PHP Censor]: https://github.com/php-censor/php-censor
[Teamcity]: https://www.jetbrains.com/teamcity/
[Deployer]: https://deployer.org/
[Magallanes]: https://www.magephp.com/
[deploying_php_applications]: https://deployingphpapplications.com/
[Ansible]: https://www.ansible.com/
[Puppet]: https://puppet.com/
[ansible_for_devops]: https://leanpub.com/ansible-for-devops
[ansible_for_aws]: https://leanpub.com/ansible-for-aws
[an_ansible_tutorial]: https://serversforhackers.com/an-ansible-tutorial
[github_actions]: https://docs.github.com/en/actions
