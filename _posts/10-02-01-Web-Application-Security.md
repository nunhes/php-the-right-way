---
isChild: true
anchor:  web_application_security
---

## Seguridade de Aplicacións Web {#web_application_security_title}

É moi importante para cada desenvolvedor PHP aprender [os básicos da seguridade de aplicacións web][4], que se poden dividir
en unha mancheada de temas amplos:

1. Separación código-datos.
   * Cando os datos son executados como código, obtés Inxección SQL, Cross-Site Scripting, Inclusión Local/Remota de Arquivos, etc.
   * Cando o código é impreso como datos, obtés filtrado de información (divulgación de código fonte ou, no caso de programas C,
     información suficiente para evitar [ASLR][5]).
2. Lóxica da aplicación.
   * Controles de autenticación ou autorización faltantes.
   * Validación de entrada.
3. Ambiente operativo.
   * Versións de PHP.
   * Bibliotecas de terceiros.
   * O sistema operativo.
4. Debilidades de criptografía.
   * [Números aleatorios débiles][6].
   * [Ataques de texto cifrado elixido][7].
   * [Filtrado de información de canais laterais][8].

Hai xente mala lista e disposta a explotar a túa aplicación web. É importante que tomes as precaucións
necesarias para endurecer a seguridade da túa aplicación web. Afortunadamente, a boa xente de
[The Open Web Application Security Project][1] (OWASP) compilou unha lista completa de problemas de seguridade coñecidos e
métodos para protexerte contra eles. Isto é unha lectura obrigatoria para o desenvolvedor consciente da seguridade. [Survive The Deep End: PHP Security][3] por Padraic Brady é tamén outra boa guía de seguridade de aplicacións web para PHP.

* [Ler a Guía de Seguridade OWASP][2]


[1]: https://www.owasp.org/
[2]: https://www.owasp.org/index.php/Guide_Table_of_Contents
[3]: https://phpsecurity.readthedocs.io/en/latest/index.html
[4]: https://paragonie.com/blog/2015/08/gentle-introduction-application-security
[5]: https://www.techtarget.com/searchsecurity/definition/address-space-layout-randomization-ASLR
[6]: https://paragonie.com/blog/2016/01/on-design-and-implementation-stealth-backdoor-for-web-applications
[7]: https://paragonie.com/blog/2015/05/using-encryption-and-authentication-correctly
[8]: https://blog.ircmaxell.com/2014/11/its-all-about-time.html
