---
title:   Estrutura de Directorios Común
isChild: true
anchor:  common_directory_structure
---

## Estrutura de directorios común {#common_directory_structure_title}

Unha pregunta común entre aqueles que comezan a escribir programas para a web é, "onde poño as miñas cousas?" Ao longo dos anos, esta resposta foi consistentemente "onde está o `DocumentRoot`." Aínda que esta resposta non é completa, é un gran lugar para comezar.

Por razóns de seguridade, os arquivos de configuración non deberían ser accesibles polos visitantes dun sitio; polo tanto, os scripts públicos mantéñense nun directorio público e as configuracións e datos privados mantéñense fóra dese directorio.

Para cada equipo, CMS, ou framework no que se traballa, cada unha desas entidades usa unha estrutura de directorios estándar. Con todo, se un está a comezar un proxecto só, saber que estrutura de sistema de arquivos usar pode ser desalentador.

[Paul M. Jones] fixo algunha investigación fantástica sobre prácticas comúns de decenas de miles de proxectos de github no ámbito de PHP. Compilou unha estrutura estándar de arquivos e directorios, o [Standard PHP Package Skeleton], baseado nesta investigación. Nesta estrutura de directorios, `DocumentRoot` debería apuntar a `public/`, as probas unitarias deberían estar no directorio `tests/`, e as librarías de terceiros, como as instaladas por [composer], pertencen ao directorio `vendor/`. Para outros arquivos e directorios, seguir o [Standard PHP Package Skeleton] terá máis sentido para os colaboradores dun proxecto.

[Paul M. Jones]: https://paul-m-jones.com/
[Standard PHP Package Skeleton]: https://github.com/php-pds/skeleton
[Composer]: /#composer_and_packagist
