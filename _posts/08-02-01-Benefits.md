---
isChild: true
anchor:  templating_benefits
---

## Beneficios {#templating_benefits_title}

O principal beneficio de usar plantillas é a clara separación que crean entre a lóxica de presentación e o resto da
túa aplicación. As plantillas teñen a única responsabilidade de mostrar contido formateado. Non son responsables de
búsqueda de datos, persistencia ou outras tarefas máis complexas. Isto leva a código máis limpo e lexíbel que é especialmente
útil nun ambiente de equipo onde os desenvolvedores traballan no código do lado do servidor (controladores, modelos) e os deseñadores traballan no
código do lado do cliente (marcado).

As plantillas tamén melloran a organización do código de presentación. As plantillas tipicamente son colocadas nunha carpeta "views", cada
unha definida dentro dun único arquivo. Este enfoque fomenta a reutilización de código onde bloques máis grandes de código son rotos en pezas máis pequenas
e reutilizábeis, a miúdo chamadas parciais. Por exemplo, o cabeceira e pé do teu sitio poden ser definidos como plantillas,
que entón son incluídas antes e despois de cada plantilla de páxina.

Finalmente, dependendo da biblioteca que uses, as plantillas poden ofrecer máis seguridade escapando automaticamente o contido
xerado polo usuario. Algunhas bibliotecas incluso ofrecen sand-boxing, onde os deseñadores de plantillas só teñen acceso a variables
e funcións de lista branca.