---
isChild: true
anchor:  linux_setup
---

## Configuración de Linux {#linux_setup_title}

A maioría das distribucións GNU/Linux veñen con PHP dispoñible desde os repositorios oficiais, pero eses paquetes xeralmente están un pouco atrasados respecto á versión estable actual. Hai múltiples formas de obter versións máis recentes de PHP en tales distribucións.

### Distribucións baseadas en Ubuntu

En Ubuntu e distribucións GNU/Linux baseadas en Debian, por exemplo, as mellores alternativas para paquetes nativos son proporcionadas e mantidas por [Ondřej Surý][Ondrej Sury Blog], a través do seu Personal Package Archive (PPA) en Ubuntu e DPA/bikeshed en Debian. Atopa instrucións para cada un destes abaixo.

Para distribucións Ubuntu, o [PPA de Ondřej Surý][Ondrej Sury PPA] proporciona versións soportadas de PHP xunto con moitas extensións PECL. Para engadir este PPA ao teu sistema, executa os seguintes pasos no teu terminal:

1. Primeiro, engade o PPA ás fontes de software do teu sistema usando o comando:

   ```bash
   sudo add-apt-repository ppa:ondrej/php
   ```

2. Despois de engadir o PPA, actualiza a lista de paquetes do teu sistema:

   ```bash
   sudo apt update
   ```

Isto asegurará que o teu sistema poida acceder e instalar os paquetes PHP máis recentes dispoñibles no PPA.

### Distribucións baseadas en Debian

Para distribucións baseadas en Debian, Ondřej Surý tamén proporciona un [bikeshed][bikeshed] (equivalente de Debian dun PPA). Para engadir o bikeshed ao teu sistema e actualizalo, segue estes pasos:

1. Asegúrate de que tes acceso root. Se non, poderías necesitar usar `sudo` para os seguintes comandos.

2. Actualiza a lista de paquetes do teu sistema:

   ```bash
   sudo apt-get update
   ```

3. Instala `lsb-release`, `ca-certificates`, e `curl`:

   ```bash
   sudo apt-get -y install lsb-release ca-certificates curl
   ```

4. Descarga a chave de sinatura para o repositorio:

   ```bash
   sudo curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
   ```

5. Engade o repositorio ás fontes de software do teu sistema:

   ```bash
   sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
   ```

6. Finalmente, actualiza a lista de paquetes do teu sistema de novo:

   ```bash
   sudo apt-get update
   ```

Con estes pasos, o teu sistema poderá instalar os paquetes PHP máis recentes desde o bikeshed.

### Distribucións baseadas en RPM

En distribucións baseadas en RPM (CentOS, Fedora, RHEL, etc.) podes usar o [repositorio RPM de Remi][remi-repo] para instalar a versión máis recente de PHP ou para ter múltiples versións de PHP dispoñibles simultaneamente.

Hai un [asistente de configuración][remi-wizard] dispoñible para configurar a túa distribución baseada en RPM.

Todo isto dito, sempre podes usar contedores ou compilar o código fonte de PHP desde cero.

[Ondrej Sury Blog]: https://deb.sury.org/
[Ondrej Sury PPA]: https://launchpad.net/~ondrej/+archive/ubuntu/php
[bikeshed]: https://packages.sury.org/php/
[remi-repo]: https://rpms.remirepo.net/
[remi-wizard]: https://rpms.remirepo.net/wizard/
