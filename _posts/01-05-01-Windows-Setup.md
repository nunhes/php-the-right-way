---
isChild: true
anchor:  windows_setup
---

## Configuración de Windows {#windows_setup_title}

Podes descargar os binarios desde [windows.php.net/download][php-downloads]. Despois da extracción de PHP, recoméndase configurar o [PATH][windows-path] á raíz da túa carpeta PHP (onde está localizado php.exe) para que poidas executar PHP desde calquera lugar.

Para aprender e desenvolvemento local, podes usar o servidor web integrado con PHP 5.4+ polo que non necesitas preocuparte por
configuralo. Se queres un "todo-en-un" que inclúa un servidor web completo e MySQL tamén, entón ferramentas como
[XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] e [WAMP][wamp] axudarán
a conseguir unha entorna de desenvolvemento en Windows funcionando rapidamente. Dito isto, estas ferramentas serán un pouco diferentes do
entorno de produción, polo que ten coidado coas diferenzas de ambiente se estás a traballar en Windows e desplegando en Linux.

Se necesitas executar o teu sistema de produción en Windows, entón IIS7 che dará a mellor estabilidade e rendemento. Podes
usar [phpmanager][phpmanager] (un plugin GUI para IIS7) para facer a configuración e xestión de PHP simple. IIS7 ven con
FastCGI integrado e listo para usar, só necesitas configurar PHP como un manexador. Para soporte e recursos adicionais
hai unha [área dedicada en iis.net][php-iis] para PHP.

Xeralmente executar a túa aplicación en diferentes ambientes en desenvolvemento e produción pode levar a estraños bugs aparecendo cando
vas en vivo. Se estás a desenvolver en Windows e desplegando en Linux (ou calquera cousa non-Windows) entón deberías considerar usar unha [Máquina Virtual](/#virtualization_title) ou [Windows Subsystem for Linux (WSL)][wsl].

Chris Tankersley ten unha entrada de blog moi útil sobre que ferramentas usa para [desenvolvemento PHP usando Windows][windows-tools].

[easyphp]: https://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: https://ospanel.io/
[wamp]: https://www.wampserver.com/en/
[php-downloads]: https://windows.php.net/download/
[php-iis]: https://php.iis.net/
[windows-path]: https://www.windows-commandline.com/set-path-command-line/
[windows-tools]: https://ctankersley.com/2016/11/13/developing-on-windows-2016/
[xampp]: https://www.apachefriends.org/
[wsl]: https://learn.microsoft.com/en-us/windows/wsl/