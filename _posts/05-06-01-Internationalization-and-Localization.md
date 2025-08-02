---
title:   Internacionalización e Localización
isChild: true
anchor:  i18n_l10n
---

## Internacionalización (i18n) e Localización (l10n) {#i18n_l10n_title}

_Descargo de responsabilidade para principiantes: i18n e l10n son numerónimos, un tipo de abreviatura onde os números son usados para acurtar
palabras - no noso caso, internacionalización convértese en i18n e localización, l10n._

Primeiro de todo, necesitamos definir eses dous conceptos similares e outras cousas relacionadas:

- **Internacionalización** é cando organizas o teu código para que poida ser adaptado a diferentes linguaxes ou rexións
sen refactorizacións. Esta acción xeralmente faise unha vez - preferiblemente, ao inicio do proxecto, ou senón probablemente
necesitarás algúns cambios enormes no código fonte!
- **Localización** acontece cando adaptas a interface (principalmente) traducindo contidos, baseado no traballo i18n feito
antes. Xeralmente faise cada vez que unha nova linguaxe ou rexión necesita soporte e é actualizada cando novas pezas de interface
son engadidas, xa que necesitan estar dispoñíbeis en todas as linguaxes soportadas.
- **Pluralización** define as regras requiridas entre linguaxes distintas para interoperar cadeas que conteñen números e 
contadores. Por exemplo, en inglés cando só tes un elemento, é singular, e calquera cousa diferente diso é 
chamado plural; o plural nesta linguaxe é indicado engadindo un S despois dalgunhas palabras, e ás veces cambia partes dela.
Noutras linguaxes, como ruso ou serbio, hai dúas formas plurales ademais do singular - incluso podes
atopar linguaxes cun total de catro, cinco ou seis formas, como esloveno, irlandés ou árabe.

## Formas comúns de implementar
A forma máis fácil de internacionalizar software PHP é usando arquivos de array e usando esas cadeas en plantillas, como
`<h1><?=$TRANS['title_about_page']?></h1>`. Esta forma é, con todo, dificilmente recomendada para proxectos serios, xa que presenta
algúns problemas de mantemento ao longo do camiño - algúns poden aparecer no mesmo inicio, como a pluralización. Así que, por favor,
non tentes isto se o teu proxecto conterá máis de un par de páxinas.

A forma máis clásica e a miúdo tomada como referencia para i18n e l10n é unha [ferramenta Unix chamada `gettext`][gettext]. Data
de 1995 e aínda é unha implementación completa para traducir software. É fácil de facer funcionar, mentres
aínda ten ferramentas de soporte poderosas. É sobre Gettext do que falaremos aquí. Tamén, para axudarte a non confundirte
coa liña de comandos, presentaremos unha gran aplicación GUI que pode ser usada para actualizar facilmente a túa fonte l10n.

### Outras ferramentas

Hai bibliotecas comúns usadas que soportan Gettext e outras implementacións de i18n. Algunhas delas poden parecer máis fáciles de
instalar ou ter funcionalidades adicionais ou formatos de arquivo i18n. Neste documento, enfocámonos nas ferramentas proporcionadas co
núcleo de PHP, pero aquí listamos outras para completar:

- [aura/intl][aura-intl]: Proporciona ferramentas de internacionalización (I18N), especificamente tradución de mensaxes orientada a paquetes por localidade.
Usa formatos de array para mensaxes. Non proporciona un extractor de mensaxes, pero proporciona formateado avanzado
de mensaxes vía a extensión `intl` (incluíndo mensaxes pluralizadas).
- [php-gettext/Gettext][php-gettext]: Soporte Gettext cunha interface OO; inclúe funcións auxiliares melloradas, extractores poderosos
para varios formatos de arquivo (algúns deles non soportados nativamente polo comando `gettext`), e tamén pode exportar
a outros formatos ademais dos arquivos `.mo/.po`. Pode ser útil se necesitas integrar os teus arquivos de tradución noutras
partes do sistema, como unha interface JavaScript.
- [symfony/translation][symfony]: soporta moitos formatos diferentes, pero recomenda usar XLIFF verbosos. Non inclúe
funcións auxiliares nin un extractor integrado, pero soporta marcadores de posición usando `strtr()` internamente.
- [laminas/laminas-i18n][laminas]: soporta arquivos de array e INI, ou formatos Gettext. Implementa unha capa de caché para aforrarte de
ler o sistema de arquivos cada vez. Tamén inclúe axudantes de vista, e filtros de entrada e validadores conscientes de localidade.
Con todo, non ten extractor de mensaxes.

Outros frameworks tamén inclúen módulos i18n, pero eses non están dispoñíbeis fóra das súas bases de código:

- [Laravel] soporta arquivos de array básicos, non ten extractor automático pero inclúe un axudante `@lang` para arquivos de plantilla.
- [Yii] soporta tradución baseada en array, Gettext e base de datos, e inclúe un extractor de mensaxes. Está respaldado pola
extensión [`Intl`][intl], dispoñíbel desde PHP 5.3, e baseada no [proxecto ICU]; isto permite a Yii executar substitucións poderosas,
como deletrear números, formatear datas, tempos, intervalos, moeda e ordinais.

Se decides ir por unha das bibliotecas que non proporcionan extractores, podes querer usar os formatos gettext, para que
podes usar a cadea de ferramentas gettext orixinal (incluíndo Poedit) como descrito no resto do capítulo.

## Gettext

### Instalación
Podes necesitar instalar Gettext e a biblioteca PHP relacionada usando o teu xestor de paquetes, como `apt-get` ou `yum`.
Despois de instalado, habilítao engadindo `extension=gettext.so` (Linux/Unix) ou `extension=php_gettext.dll` (Windows) ao
teu `php.ini`.

Aquí tamén usaremos [Poedit] para crear arquivos de tradución. Probablemente o atoparás no xestor de paquetes do teu sistema;
está dispoñíbel para Unix, macOS e Windows, e pode ser [descargado gratis no seu sitio web][poedit_download]
tamén.

### Estrutura

#### Tipos de arquivos
Hai tres arquivos co que xeralmente traballas mentres traballas con gettext. Os principais son os arquivos PO (Obxecto Portábel) e
MO (Obxecto de Máquina), o primeiro sendo unha lista de "obxectos traducidos" lexíbeis e o segundo, o binario correspondente
para ser interpretado por gettext cando fai localización. Tamén hai un arquivo POT (Plantilla), que simplemente contén
todas as chaves existentes dos teus arquivos fonte, e pode ser usado como unha guía para xerar e actualizar todos os arquivos PO. Eses arquivos
de plantilla non son obrigatorios: dependendo da ferramenta que estás usando para facer l10n, podes ir ben só con arquivos PO/MO.
Sempre terás un par de arquivos PO/MO por linguaxe e rexión, pero só un POT por dominio.

### Dominios
Hai algúns casos, en proxectos grandes, onde podes necesitar separar traducións cando as mesmas palabras transmiten 
significados diferentes dado un contexto. Neses casos, sepáranos en diferentes _dominios_. Son, basicamente, grupos nomeados
de arquivos POT/PO/MO, onde o nome do arquivo é o dito _dominio de tradución_. Proxectos pequenos e medianos xeralmente,
por simplicidade, usan só un dominio; o seu nome é arbitrario, pero usaremos "main" para os nosos exemplos de código.
En proxectos [Symfony], por exemplo, os dominios son usados para separar a tradución para mensaxes de validación.

#### Código de localidade
Unha localidade é simplemente un código que identifica unha versión dunha linguaxe. Está definido seguindo as especificacións [ISO 639-1][639-1] e 
[ISO 3166-1 alpha-2][3166-1]: dúas letras minúsculas para a linguaxe, opcionalmente seguidas por un subliñado e dúas
letras maiúsculas identificando o país ou código rexional. Para [linguaxes raras][rare], úsanse tres letras.

Para algúns falantes, a parte do país pode parecer redundante. De feito, algunhas linguaxes teñen dialectos en diferentes
países, como alemán austríaco (`de_AT`) ou portugués brasileiro (`pt_BR`). A segunda parte é usada para distinguir
entre eses dialectos - cando non está presente, é tomado como unha versión "xenérica" ou "híbrida" da linguaxe.

### Estrutura de directorios
Para usar Gettext, necesitaremos adherir a unha estrutura específica de carpetas. Primeiro, necesitarás seleccionar un directorio raíz arbitrario
para os teus arquivos l10n no teu repositorio fonte. Dentro del, terás unha carpeta para cada localidade necesaria, e unha
carpeta fixa `LC_MESSAGES` que conterá todos os teus pares PO/MO. Exemplo:

{% highlight console %}
<project root>
 ├─ src/
 ├─ templates/
 └─ locales/
    ├─ forum.pot
    ├─ site.pot
    ├─ de/
    │  └─ LC_MESSAGES/
    │     ├─ forum.mo
    │     ├─ forum.po
    │     ├─ site.mo
    │     └─ site.po
    ├─ es_ES/
    │  └─ LC_MESSAGES/
    │     └─ ...
    ├─ fr/
    │  └─ ...
    ├─ pt_BR/
    │  └─ ...
    └─ pt_PT/
       └─ ...
{% endhighlight %}

### Formas plurales
Como dixemos na introdución, linguaxes diferentes poden ter regras plurales diferentes. Con todo, gettext aforranos de
este problema unha vez máis. Cando creas un novo arquivo `.po`, terás que declarar as [regras plurales][plural] para esa
linguaxe, e as pezas traducidas que son sensibles ao plural terán unha forma diferente para cada unha desas regras. Cando
chamas Gettext no código, terás que especificar o número relacionado coa frase, e funcionará a forma correcta
para usar - mesmo usando substitución de cadea se é necesario.

As regras plurales inclúen o número de plurais dispoñíbeis e unha proba booleana con `n` que definiría en que regra o
número dado cae (comezando a conta con 0). Por exemplo:

- Xaponés: `nplurals=1; plural=0` - só unha regra
- Inglés: `nplurals=2; plural=(n != 1);` - dúas regras, primeira se N é un, segunda regra en caso contrario
- Portugués brasileiro: `nplurals=2; plural=(n > 1);` - dúas regras, segunda se N é maior que un, primeira en caso contrario

Agora que entendiches a base de como funcionan as regras plurales - e se non o fixeches, por favor mira unha explicación máis profunda
no [tutorial de LingoHub][lingohub_plurals] -, podes querer copiar as que necesitas dunha [lista][plural] en lugar
de escribilas a man.

Cando chamas Gettext para facer localización en frases con contadores, terás que proporcionarlle o
número relacionado tamén. Gettext funcionará que regra debería estar en efecto e usar a versión localizada correcta.
Necesitarás incluír no arquivo `.po` unha frase diferente para cada regra plural definida.

### Exemplo de implementación
Despois de toda esa teoría, vamos facer algo práctico. Aquí hai un extracto dun arquivo `.po` - non te preocupes co seu formato,
senón co contido xeral; aprenderás como editalo facilmente máis tarde:

{% highlight po %}
msgid ""
msgstr ""
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

msgid "We are now translating some strings"
msgstr "Nós estamos traduzindo algumas strings agora"

msgid "Hello %1$s! Your last visit was on %2$s"
msgstr "Olá %1$s! Sua última visita foi em %2$s"

msgid "Only one unread message"
msgid_plural "%d unread messages"
msgstr[0] "Só uma mensagem não lida"
msgstr[1] "%d mensagens não lidas"
{% endhighlight %}

A primeira sección funciona como un cabeceira, tendo o `msgid` e `msgstr` especialmente baleiros. Describe a codificación do arquivo,
formas plurales e outras cousas que son menos relevantes.
A segunda sección traduce unha cadea simple do inglés ao
portugués brasileiro, e a terceira fai o mesmo, pero aproveitando a substitución de cadea de [`sprintf`][sprintf] para que a
tradución poida conter o nome do usuario e data de visita.
A última sección é un exemplo de formas de pluralización, mostrando
a versión singular e plural como `msgid` en inglés e as súas traducións correspondentes como `msgstr` 0 e 1
(seguindo o número dado pola regra plural). Alí, a substitución de cadea é usada tamén para que o número poida ser visto
directamente na frase, usando `%d`. As formas plurales sempre teñen dous `msgid` (singular e plural), polo que é
aconsellado non usar unha linguaxe complexa como a fonte de tradución.

### Discusión sobre chaves l10n
Como podes ter notado, estamos usando como ID fonte a frase real en inglés. Ese `msgid` é o mesmo usado
a través de todos os teus arquivos `.po`, significando que outras linguaxes terán o mesmo formato e os mesmos campos `msgid` pero
liñas `msgstr` traducidas.

Falando sobre chaves de tradución, hai dúas "escolas" principais aquí:

1. _`msgid` como unha frase real_.
    As principais vantaxes son:
    - se hai pezas do software non traducidas en calquera linguaxe dada, a chave mostrada aínda manterá algún
    significado. Exemplo: se aconteces traducir de memoria do inglés ao español pero necesitas axuda para traducir ao francés,
    podes publicar a nova páxina con frases francesas faltantes, e partes do sitio web serían mostradas en inglés
    en cambio;
    - é moito máis fácil para o tradutor entender que está pasando e facer unha tradución adecuada baseada no
    `msgid`;
    - dache l10n "gratis" para unha linguaxe - a fonte;
    - A única desvantaxe: se necesitas cambiar o texto real, necesitarías substituir o mesmo `msgid`
    a través de varios arquivos de linguaxe.

2. _`msgid` como unha chave única e estruturada_.
Describiría o papel da frase na aplicación dunha forma estruturada, incluíndo a plantilla ou parte onde a
cadea está localizada en lugar do seu contido.
    - é unha gran forma de ter o código organizado, separando o contido de texto da lóxica da plantilla.
    - con todo, iso podería traer problemas ao tradutor que perdería o contexto. Un arquivo de linguaxe fonte sería
    necesario como base para outras traducións. Exemplo: o desenvolvedor idealmente tería un arquivo `en.po`, que
    os tradutores lerían para entender que escribir en `fr.po` por exemplo.
    - as traducións faltantes mostrarían chaves sen significado na pantalla (`top_menu.welcome` en lugar de `Hello there, User!`
    na dita páxina francesa non traducida). Iso é bo xa que forzaría a tradución a ser completa antes de publicar -
    con todo, malo xa que os problemas de tradución serían notablemente terribles na interface. Algunhas bibliotecas, con todo, inclúen unha
    opción para especificar unha linguaxe dada como "fallback", tendo un comportamento similar ao outro enfoque.

O [manual de Gettext][manual] favorece o primeiro enfoque xa que, en xeral, é máis fácil para tradutores e usuarios en
caso de problemas. É así como tamén traballaremos aquí. Con todo, a [documentación de Symfony][symfony-keys] favorece
tradución baseada en palabras clave, para permitir cambios independentes de todas as traducións sen afectar as plantillas tamén.

### Uso cotián
Nunha aplicación típica, usarías algunhas funcións Gettext mentres escribes texto estático nas túas páxinas. Esas frases
entón aparecerían en arquivos `.po`, serían traducidas, compiladas en arquivos `.mo` e entón, usadas por Gettext cando renderiza
a interface real. Dado iso, vamos atar xuntos o que discutimos ata agora nun exemplo paso a paso:

#### 1. Un arquivo de plantilla de exemplo, incluíndo algunhas chamadas gettext diferentes
{% highlight php %}
<?php include 'i18n_setup.php' ?>
<div id="header">
    <h1><?=sprintf(gettext('Welcome, %s!'), $name)?></h1>
    <!-- código indentado desta forma só para lexibilidade -->
    <?php if ($unread): ?>
        <h2><?=sprintf(
            ngettext('Only one unread message',
                     '%d unread messages',
                     $unread),
            $unread)?>
        </h2>
    <?php endif ?>
</div>

<h1><?=gettext('Introduction')?></h1>
<p><?=gettext('We\'re now translating some strings')?></p>
{% endhighlight %}

- [`gettext()`][func] simplemente traduce un `msgid` ao seu `msgstr` correspondente para unha linguaxe dada. Tamén hai
a función abreviada `_()` que funciona da mesma forma;
- [`ngettext()`][n_func] fai o mesmo pero con regras plurales;
- Tamén hai [`dgettext()`][d_func] e [`dngettext()`][dn_func], que permiten que sobrescribas o dominio para unha única
chamada. Máis sobre configuración de dominio no próximo exemplo.

#### 2. Un arquivo de configuración de exemplo (`i18n_setup.php` como usado arriba), seleccionando a localidade correcta e configurando Gettext
{% highlight php %}
<?php
/**
 * Verifica se a localidade dada $locale é soportada no proxecto
 * @param string $locale
 * @return bool
 */
function valid($locale) {
   return in_array($locale, ['en_US', 'en', 'pt_BR', 'pt', 'es_ES', 'es']);
}

//configurando a localidade fonte/por defecto, para propósitos informativos
$lang = 'en_US';

if (isset($_GET['lang']) && valid($_GET['lang'])) {
    // a localidade pode ser cambiada a través da query-string
    $lang = $_GET['lang'];    //deberías sanitizar isto!
    setcookie('lang', $lang); //está almacenado nunha cookie para que poida ser reusado
} elseif (isset($_COOKIE['lang']) && valid($_COOKIE['lang'])) {
    // se a cookie está presente en cambio, só mantémola
    $lang = $_COOKIE['lang']; //deberías sanitizar isto!
} elseif (isset($_SERVER['HTTP_ACCEPT_LANGUAGE'])) {
    // por defecto: busca as linguaxes que o navegador di que o usuario acepta
    $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
    array_walk($langs, function (&$lang) { $lang = strtr(strtok($lang, ';'), ['-' => '_']); });
    foreach ($langs as $browser_lang) {
        if (valid($browser_lang)) {
            $lang = $browser_lang;
            break;
        }
    }
}

// aquí definimos a localidade do sistema global dada a linguaxe atopada
putenv("LANG=$lang");

// isto pode ser útil para funcións de data (LC_TIME) ou formateado de diñeiro (LC_MONETARY), por exemplo
setlocale(LC_ALL, $lang);

// isto fará que Gettext busque en ../locales/<lang>/LC_MESSAGES/main.mo
bindtextdomain('main', '../locales');

// indica en que codificación o arquivo debería ser lido
bind_textdomain_codeset('main', 'UTF-8');

// se a túa aplicación ten dominios adicionais, como citado antes, deberías vinculalos aquí tamén
bindtextdomain('forum', '../locales');
bind_textdomain_codeset('forum', 'UTF-8');

// aquí indicamos o dominio por defecto ao que as chamadas gettext() responderán
textdomain('main');

// isto buscaría a cadea en forum.mo en lugar de main.mo
// echo dgettext('forum', 'Welcome back!');
?>
{% endhighlight %}

#### 3. Preparando tradución para a primeira execución
Unha das grandes vantaxes que Gettext ten sobre paquetes i18n de frameworks personalizados é o seu formato de arquivo extenso e poderoso.
"¡Oh home, iso é bastante difícil de entender e editar a man, un array simple sería máis fácil!" Non te equivoques,
aplicacións como [Poedit] están aquí para axudar - _moito_. Podes obter o programa do [seu sitio web][poedit_download],
é gratis e está dispoñíbel para todas as plataformas. É unha ferramenta bastante fácil de acostumbrarse, e unha moi poderosa ao mesmo
tempo - usando todas as funcionalidades que Gettext ten dispoñíbeis. Esta guía está baseada en PoEdit 1.8.

Na primeira execución, deberías seleccionar "File > New..." do menú. Serás preguntado directamente pola linguaxe:
aquí podes seleccionar/filtrar a linguaxe que queres traducir, ou usar ese formato que mencionamos antes, como
`en_US` ou `pt_BR`.

Agora, garda o arquivo - usando esa estrutura de directorios que mencionamos tamén. Entón deberías facer clic en "Extract from sources",
e aquí configurarás varias configuracións para as tarefas de extracción e tradución. Poderás atopar todas esas
máis tarde a través de "Catalog > Properties":

- Camiños fonte: aquí debes incluír todas as carpetas do proxecto onde `gettext()` (e similares) son chamados - isto
xeralmente é a(s) túa(s) carpeta(s) de plantillas/vistas. Esta é a única configuración obrigatoria;
- Propiedades de tradución:
    - Nome do proxecto e versión, Equipo e enderezo de email do equipo: información útil que vai no cabeceira do arquivo .po;
    - Formas plurales: aquí van esas regras que mencionamos antes - hai un enlace alí con exemplos tamén. Podes
    deixalo coa opción por defecto a maioría do tempo, xa que PoEdit xa inclúe unha base de datos práctica de regras plurales para
    moitas linguaxes.
    - Charsets: UTF-8, preferiblemente;
    - Charset do código fonte: establece aquí o charset usado pola túa base de código - probablemente UTF-8 tamén, certo?
- Palabras clave fonte: O software subxacente sabe como `gettext()` e chamadas de función similares se ven en varios
linguaxes de programación, pero tamén podes crear as túas propias funcións de tradución. Será aquí onde engadirás eses
outros métodos. Isto será discutido máis tarde na sección "Consellos".

Despois de establecer eses puntos executará unha busca a través dos teus arquivos fonte para atopar todas as chamadas de localización. Despois de cada
busca PoEdit mostrará un resumo do que foi atopado e do que foi eliminado dos arquivos fonte. As novas entradas serán alimentadas
baleiras na táboa de tradución, e comezarás a escribir as versións localizadas desas cadeas. Gardao e un arquivo .mo
será (re)compilado na mesma carpeta e ta-dah: o teu proxecto está internacionalizado.

#### 4. Traducindo cadeas
Como podes ter notado antes, hai dous tipos principais de cadeas localizadas: simples e aquelas con formas
plurales. As primeiras simplemente teñen dúas caixas: cadea fonte e cadea localizada. A cadea fonte non pode ser modificada xa que
Gettext/Poedit non inclúen os poderes para alterar os teus arquivos fonte - deberías cambiar a fonte en si e rebuscar
os arquivos. Consello: podes facer clic dereito nunha liña de tradución e che dará unha pista cos arquivos fonte e liñas onde esa
cadea está sendo usada.
Por outra banda, as cadeas de forma plural inclúen dúas caixas para mostrar as dúas cadeas fonte, e pestanas para que poidas configurar
as diferentes formas finais.

Sempre que cambies as túas fontes e necesites actualizar as traducións, só fai clic en Refresh e Poedit rebuscará o código,
eliminando entradas non existentes, fusionando as que cambiaron e engadindo novas. Tamén pode tentar adiviñar algunhas
traducións, baseadas noutras que fixeches. Esas adiviñacións e as entradas cambiadas recibirán un marcador "Fuzzy",
indicando que necesita revisión, aparecendo dourado na lista. Tamén é útil se tes un equipo de tradución e alguén
tenta escribir algo do que non están seguros: só marca Fuzzy, e alguén máis revisará máis tarde.

Finalmente, é aconsellado deixar "View > Untranslated entries first" marcado, xa que che axudará _moito_ a non esquecer
ningunha entrada. Desde ese menú, tamén podes abrir partes da UI que permiten deixar información contextual para
tradutores se é necesario.

### Consellos e Trucos

#### Posíbeis problemas de caché
Se estás executando PHP como un módulo en Apache (`mod_php`), podes enfrontarte problemas co arquivo `.mo` sendo cacheado. Acontece
a primeira vez que é lido, e entón, para actualizalo, podes necesitar reiniciar o servidor. En Nginx e PHP5
xeralmente leva só un par de refrescos de páxina para refrescar o caché de tradución, e en PHP7 raramente é necesario.

#### Funcións auxiliares adicionais
Como preferido por moita xente, é máis fácil usar `_()` en lugar de `gettext()`. Moitas bibliotecas i18n personalizadas de
frameworks usan algo similar a `t()` tamén, para facer o código traducido máis curto. Con todo, esa é a única función
que ten un atallo. Podes querer engadir no teu proxecto algunhas outras, como `__()` ou `_n()` para `ngettext()`,
ou quizais un elegante `_r()` que uniría chamadas `gettext()` e `sprintf()`. Outras bibliotecas, como
[Gettext de php-gettext][php-gettext] tamén proporcionan funcións auxiliares como estas.

Neses casos, necesitarás instruír a utilidade Gettext sobre como extraer as cadeas desas novas funcións.
Non te asustes; é moi fácil. É só un campo no arquivo `.po`, ou unha pantalla de Configuracións en Poedit. No editor,
esa opción está dentro de "Catalog > Properties > Source keywords". Lembra: Gettext xa sabe as funcións por defecto
para moitas linguaxes, así que non te asustes se esa lista parece baleira. Necesitas incluír alí as especificacións desas
novas funcións, seguindo [un formato específico][func_format]:

- se creas algo como `t()` que simplemente retorna a tradución para unha cadea, podes especificalo como `t`.
Gettext saberá que o único argumento da función é a cadea a ser traducida;
- se a función ten máis dun argumento, podes especificar en cal o primeiro está a primeira cadea - e se é necesario, a
forma plural tamén. Por exemplo, se chamamos a nosa función así: `__('one user', '%d users', $number)`, a
especificación sería `__:1,2`, significando que a primeira forma é o primeiro argumento, e a segunda forma é o segundo
argumento. Se o teu número vén como o primeiro argumento en cambio, a especificación sería `__:2,3`, indicando que a primeira forma é
o segundo argumento, e así por diante.

Despois de incluír esas novas regras no arquivo `.po`, unha nova busca traerá as túas novas cadeas tan fácil como antes.

### Referencias

* [Wikipedia: i18n e l10n](https://en.wikipedia.org/wiki/Internationalization_and_localization)
* [Wikipedia: Gettext](https://en.wikipedia.org/wiki/Gettext)
* [LingoHub: tutorial de internacionalización PHP con gettext][lingohub]
* [Manual de PHP: Gettext](https://www.php.net/manual/book.gettext.php)
* [Manual de Gettext][manual]

[Poedit]: https://poedit.net
[poedit_download]: https://poedit.net/download
[lingohub]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/
[lingohub_plurals]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/#Plurals
[plural]: https://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html
[gettext]: https://en.wikipedia.org/wiki/Gettext
[manual]: https://www.gnu.org/software/gettext/manual/gettext.html
[639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[3166-1]: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[rare]: https://www.gnu.org/software/gettext/manual/gettext.html#Rare-Language-Codes
[func_format]: https://www.gnu.org/software/gettext/manual/gettext.html#Language-specific-options
[aura-intl]: https://github.com/auraphp/Aura.Intl
[php-gettext]: https://github.com/php-gettext/Gettext
[symfony]: https://symfony.com/components/Translation
[laminas]: https://docs.laminas.dev/laminas-i18n/
[laravel]: https://laravel.com/docs/master/localization
[yii]: https://www.yiiframework.com/doc/guide/2.0/en/tutorial-i18n
[intl]: https://www.php.net/manual/intro.intl.php
[ICU project]: https://icu.unicode.org/
[symfony-keys]: https://symfony.com/doc/current/translation.html#using-real-or-keyword-messages

[sprintf]: https://www.php.net/manual/function.sprintf.php
[func]: https://www.php.net/manual/function.gettext.php
[n_func]: https://www.php.net/manual/function.ngettext.php
[d_func]: https://www.php.net/manual/function.dgettext.php
[dn_func]: https://www.php.net/manual/function.dngettext.php
