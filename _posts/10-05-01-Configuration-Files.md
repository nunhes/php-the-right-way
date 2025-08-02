---
isChild: true
anchor:  configuration_files
---

## Arquivos de Configuración {#configuration_files_title}

Cando creas arquivos de configuración para as túas aplicacións, as mellores prácticas recomiendan que un dos seguintes métodos sexa
seguido:

- Recoméndase que almacenes a túa información de configuración onde non poida ser accedida directamente e extraída
vía o sistema de arquivos.
- Se debes almacenar os teus arquivos de configuración no directorio raíz do documento, nomea os arquivos cunha extensión `.php`. Isto asegura
que, mesmo se o script é accedido directamente, non será saído como texto plano.
- A información nos arquivos de configuración debería ser protexida adecuadamente, sexa a través de encriptación ou permisos de arquivo de grupo/usuario
do sistema.
- É unha boa idea asegurar que non comites arquivos de configuración que conteñan información sensíbel ex. contrasinais ou tokens de API ao control de código fonte.
