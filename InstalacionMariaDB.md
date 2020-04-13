# INSTALACIÓN DE MariaDB

Para poder instalar MariaDB, tenemos que añadir un repositorio de MariaDB en el sistema. Para ello, hay que realizar **3 pasos antes de comenzar la instalación** utilizando una serie de comandos en la terminal.

**1.** Instalar las propiedades de software comunes: 

[
`sudo apt-get install software-properties-common` ](/mariaDB1.PNG)

**2.** Añadir la clave del repositorio al sistema:

[`sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8`](/mariaDB3.PNG)

**3.** Añadir el repositorio. Una vez importada la clave PGP, procederemos a añadir la URL del repositorio a nuestro servidor Ubuntu 18.04:

[`sudo add-apt-repository "deb [arch=amd64,arm64,ppc64el] http://mariadb.mirror.liquidtelecom.com/repo/10.4/ubuntu $(lsb_release -cs) main"`](/mariaDB3.PNG)

Después de ejecutar estos comandos, podremos pasar a la **instalación** del server MariaDB. Primero haremos un update para que liste el repositorio que hemos añadido, y luego ejecutaremos el comando de instalación:

[`sudo apt update`](/mariaDB5.PNG)

[`sudo apt -y install mariadb-server mariadb-client`](/mariaDB5.PNG)

A continuación aparecerá una ventana que pedirá proporcionar una contraseña de root de MariaDB. Si no pidió establecer una contraseña de root, debemos ejecutar el comando:

[`sudo mysql_secure_installation`](/mariaDB6.PNG)

Una vez ejecutado el comando nos pedirá una configuración inicial. En todas las preguntas sobre la configuración, escribiremos la opción **Y** (*yes*). A continuación deberá aparecer el siguiente [mensaje](/mariaDB9.PNG):

>Cleaning up...

> All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

>Thanks for using MariaDB!

**Por último**, el siguiente comando nos permitirá el acceso a MariaDB con el usuario root. Pedirá la contraseña de root que establecimos anteriormente: 

[`mysql -u root -p`](/mariaDB9.PNG)

La línea de comandos habrá cambiado para indicarnos que estamos [dentro de MariaDB](/mariaDB10.PNG) (`MariaDB [(none)]>  `).
