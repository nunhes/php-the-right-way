---
isChild: true
anchor:  password_hashing
---

## Hash de Contrasinais {#password_hashing_title}

Eventualmente todos constrúen unha aplicación PHP que depende do login de usuario. Os nomes de usuario e contrasinais son almacenados nunha
base de datos e máis tarde usados para autenticar usuarios ao facer login.

É importante que [_haxees_][3] correctamente os contrasinais antes de almacenalos. Haxear e encriptar son [dúas cousas moi diferentes][7]
que a miúdo se confunden.

Haxear é unha función irreversible e unidireccional. Isto produce unha cadea de lonxitude fixa que non pode ser factiblemente revertida.
Isto significa que podes comparar un hash contra outro para determinar se ambos veñen da mesma cadea fonte, pero non
podes determinar a cadea orixinal. Se os contrasinais non están haxeados e a túa base de datos é accedida por un terceiro
non autorizado, todas as contas de usuario están agora comprometidas.

A diferenza do haxear, a encriptación é reversible (sempre que teñas a chave). A encriptación é útil noutras áreas, pero é unha pobre
estratexia para almacenar contrasinais de forma segura.

Os contrasinais tamén deberían ser individualmente [_salados_][5] engadindo unha cadea aleatoria a cada contrasinal antes de haxear. Isto prevén ataques de dicionario e o uso de "táboas arco da vella" (unha lista inversa de hashes criptográficos para contrasinais comúns).

Haxear e salar son vitais xa que a miúdo os usuarios usan o mesmo contrasinal para múltiples servizos e a calidade do contrasinal pode ser pobre.

Ademais, deberías usar [un algoritmo especializado de _hash de contrasinal_][6] en lugar dunha función de hash criptográfico rápida e de propósito xeral
(ex. SHA256). A lista curta de algoritmos aceptábeis de hash de contrasinal (a partir de xuño de 2018)
para usar son:

* Argon2 (dispoñíbel en PHP 7.2 e máis recente)
* Scrypt
* **Bcrypt** (PHP proporciona este para ti; vexa abaixo)
* PBKDF2 con HMAC-SHA256 ou HMAC-SHA512

Afortunadamente, hoxe en día PHP fai isto fácil.

**Haxear contrasinais con `password_hash`**

En PHP 5.5 `password_hash()` foi introducido. Neste momento está usando BCrypt, o algoritmo máis forte actualmente
soportado por PHP. Será actualizado no futuro para soportar máis algoritmos segundo sexa necesario. A libraría `password_compat`
foi creada para proporcionar compatibilidade cara adiante para PHP >= 5.3.7.

Abaixo haxeamos unha cadea, e entón verificamos o hash contra unha nova cadea. Porque as nosas dúas cadeas fonte son diferentes
('secret-password' vs. 'bad-password') este login fallará.

{% highlight php %}
<?php
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Contrasinal Correcto
} else {
    // Contrasinal incorrecto
}
{% endhighlight %}

`password_hash()` coida do salado de contrasinais para ti. O sal está almacenado, xunto co algoritmo e "custo", como parte do hash. `password_verify()` extrae isto para determinar como verificar o contrasinal, polo que non necesitas un campo separado de base de datos para almacenar os teus sales.

* [Aprender sobre `password_hash()`] [1]
* [`password_compat` para PHP >= 5.3.7 && < 5.5] [2]
* [Aprender sobre haxear en relación á criptografía] [3]
* [Aprender sobre sales] [5]
* [RFC de PHP `password_hash()`] [4]


[1]: https://www.php.net/function.password-hash
[2]: https://github.com/ircmaxell/password_compat
[3]: https://wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
[5]: https://wikipedia.org/wiki/Salt_(cryptography)
[6]: https://paragonie.com/blog/2016/02/how-safely-store-password-in-2016
[7]: https://paragonie.com/blog/2015/08/you-wouldnt-base64-a-password-cryptography-decoded

