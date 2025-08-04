---
isChild: true
title:   Extensión MySQL
anchor:  mysql_extension
---

## Extensión MySQL {#mysql_extension_title}

A extensión [mysql] para PHP é increíblemente antiga e foi suplantada por dúas outras extensións:

- [mysqli]
- [pdo]

Non só o desenvolvemento se detivo hai moito tempo [mysql], 
**foi [eliminado oficialmente en PHP 7.0][mysql_removed]**.

Para asegurar a busca nas túas opcións de `php.ini` para ver que módulo estás usando, unha opción é buscar `mysql_*`
no editor que escollas. Se algunha función como `mysql_connect()` e `mysql_query()` aparecen, entón `mysql` está en uso.

Mesmo se aínda non estás a usar PHP 7.x ou posterior, non considerar esta actualización canto antes levará a maiores dificultades cando se produza a actualización de PHP. A mellor opción é substituír o uso de MySQL por [mysqli] ou [PDO] nas túas aplicacións dentro dos teus propios programas de desenvolvemento para non ter présas máis tarde.

**Se estás a actualizar desde [mysql] a [mysqli], coidado coas guías de actualización preguiceiras que suxiren que podes simplemente atopar e substituír `mysql_*` con `mysqli_*`. Non só é unha simplificación excesiva, senón que tamén pasa por alto as vantaxes que ofrece [mysqli], como a vinculación de parámetros, que tamén se ofrece en [PDO][pdo].**

* [Sentenzas preparadas de MySQLi][mysqli_prepared_statements]
* [PHP: Escolla dunha API para MySQL][mysql_api]

[mysql]: https://www.php.net/mysqli
[mysql_removed]: https://www.php.net/manual/migration70.removed-exts-sapis.php
[mysqli]: https://www.php.net/mysqli
[pdo]: https://www.php.net/pdo
[mysql_api]: https://www.php.net/mysqlinfo.api.choosing
[mysqli_prepared_statements]: https://websitebeaver.com/prepared-statements-in-php-mysqli-to-prevent-sql-injection
