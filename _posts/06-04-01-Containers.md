---
isChild: true
anchor:  containers
---

## Contenedores {#containers_title}

A primeira cousa que deberías entender sobre os Contenedores de Inxección de Dependencias é que non son a mesma cousa que
a Inxección de Dependencias. Un contenedor é unha utilidade de conveniencia que nos axuda a implementar Inxección de Dependencias, con todo, poden
ser e a miúdo son mal usados para implementar un anti-patrón, Localización de Servizos. Inxectar un contenedor DI como un Localizador de Servizos
nas túas clases argumentablemente crea unha dependencia máis dura no contenedor que a dependencia que estás substituíndo.
Tamén fai o teu código moito menos transparente e finalmente máis difícil de probar.

A maioría dos frameworks modernos teñen o seu propio Contenedor de Inxección de Dependencias que permite que conectes as túas dependencias xuntas
a través de configuración. O que isto significa na práctica é que podes escribir código de aplicación que é tan limpo e
desacoplado como o framework no que está construído.
