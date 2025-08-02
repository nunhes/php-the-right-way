---
title:  Bases de Datos
anchor: databases
---

# Bases de Datos {#databases_title}

Moitas veces o teu código PHP usará unha base de datos para persistir información. Tes unhas poucas opcións para conectar e interactuar
coa túa base de datos. A opción recomendada **ata PHP 5.1.0** era usar drivers nativos como [mysqli], [pgsql],
[mssql], etc.

Os drivers nativos son excelentes se só estás usando _unha_ base de datos na túa aplicación, pero se, por exemplo, estás usando
MySQL e un pouco de MSSQL, ou necesitas conectar a unha base de datos Oracle, entón non poderás usar os
mesmos drivers. Necesitarás aprender unha API completamente nova para cada base de datos &mdash; e iso pode volverse ridículo.


[mysqli]: https://www.php.net/mysqli
[pgsql]: https://www.php.net/pgsql
[mssql]: https://www.php.net/mssql
