---
isChild: true
anchor:  object_caching
---

## Caché de Obxectos {#object_caching_title}

Hai veces cando pode ser beneficioso cachear obxectos individuais no teu código, como con datos que son custosos
de obter ou chamadas de base de datos onde o resultado é improbable que cambie. Podes usar software de caché de obxectos para manter estas
pezas de datos en memoria para acceso extremadamente rápido máis tarde. Se gardas estes elementos nun almacén de datos despois de recuperalos,
entón tíralos directamente do caché para peticións seguintes, podes obter unha mellora significativa no
rendemento así como reducir a carga nos teus servidores de base de datos.

Moitas das solucións populares de caché de bytecode permiten que cachees datos personalizados tamén, polo que hai aínda máis razón para aproveitar
delas. APCu e WinCache ambos proporcionan APIs para gardar datos do teu código PHP ao seu caché de memoria.

Os sistemas de caché de obxectos en memoria máis comunmente usados son APCu e memcached. APCu é unha excelente elección para caché de obxectos,
inclúe unha API simple para engadir os teus propios datos ao seu caché de memoria e é moi fácil de configurar e usar. A
única limitación real de APCu é que está vinculado ao servidor no que está instalado. Memcached por outra banda está
instalado como un servizo separado e pode ser accedido a través da rede, significando que podes almacenar obxectos nun
almacén de datos hiper-rápido nunha localización central e moitos sistemas diferentes poden tirar del.

Nota que se o caché é compartido a través de procesos PHP depende de como PHP é usado. Cando executas PHP vía PHP-FPM,
o caché é compartido a través de todos os procesos de todos os pools. Cando executas PHP como unha aplicación (Fast-)CGI dentro do teu
servidor web, o caché non é compartido, é dicir cada proceso PHP terá os seus propios datos APCu. Cando executas PHP na liña de
comandos, o caché non é compartido e só existirá durante a duración do comando, polo que tes que ser consciente da túa
situación e obxectivos. Podes querer considerar usar memcached en cambio, xa que non está vinculado aos procesos PHP.

Nunha configuración en rede APCu xeralmente superará memcached en termos de velocidade de acceso, pero memcached será
capaz de escalar máis rápido e máis lonxe. Se non esperas ter múltiples servidores executando a túa aplicación, ou non
necesitas as funcionalidades extra que memcached ofrece entón APCu é probablemente a túa mellor elección para caché de obxectos.

Exemplo de lóxica usando APCu:

{% highlight php %}
<?php
// verifica se hai datos gardados como 'expensive_data' no caché
$data = apcu_fetch('expensive_data');
if ($data === false) {
    // os datos non están no caché; garda o resultado da chamada custosa para uso posterior
    apcu_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

### Aprender máis sobre sistemas populares de caché de obxectos:

* [APCu](https://github.com/krakjoe/apcu)
* [Documentación de APCu](https://www.php.net/apcu)
* [Memcached](https://memcached.org/)
* [Redis](https://redis.io/)
* [Funcións de WinCache](https://www.php.net/ref.wincache)
