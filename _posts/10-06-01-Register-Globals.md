---
isChild: true
anchor:  register_globals
---

## Register Globals {#register_globals_title}

**NOTA:** A partir de PHP 5.4.0 a configuración `register_globals` foi eliminada e xa non pode ser usada. Isto só está
incluído como unha advertencia para calquera no proceso de actualizar unha aplicación legada.

Cando está habilitada, a configuración `register_globals` fai dispoñíbeis varios tipos de variables (incluíndo as de
`$_POST`, `$_GET` e `$_REQUEST`) no ámbito global da túa aplicación. Isto pode facilmente levar a problemas de seguridade
xa que a túa aplicación non pode efectivamente dicir de onde veñen os datos.

Por exemplo: `$_GET['foo']` estaría dispoñíbel vía `$foo`, que pode sobrescribir variables que foron declaradas.

Se estás usando PHP < 5.4.0 __asegúrate__ de que `register_globals` está __desactivado__.
