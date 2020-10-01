# splunk-gns3

## Instalación de Splunk y recogida de logs de máquinas Mikrotik, Ubuntu, Vyos, CentOS en Splunk creadas mediante GNS3.

Vamos a realizar un ejercicio donde instalaremos splunk en una máquina virtual Debian, el programa que utilizaremos para virtualizar dicha máquina será VMWare.


### Instalación de Splunk

Tenemos un Debian 10 actualizado y virtualizado en VMWare, para instalar Splunk es bastante sencillo, nos iremos a la página de descargas de [Splunk](https://www.splunk.com/en_us/download/splunk-enterprise.html).
En este caso elegiremos la versión gratuita de Enterprise.

Nos descargaremos la versión de Linux .deb, ya que estamos usando una máquina Debian.

Al tenerlo descargado simplemente para instalarlo ejecutamos como superusuario:
```
dpkg -i splunk-8.0.6-152fb4b2bb96-linux-2.6-amd64.deb
```

Una vez termine, la instalación será realizada en /opt/splunk de nuestra máquina.

Para encender splunk y tener nuestra aplicación web simplemente realizamos el siguiente comando:

```
/opt/splunk/bin/splunk start
```

Se nos pedirá aceptar la licencia y crear un usuario administrador para poder operar con splunk, una vez hecho ya podremos acceder a la web mediante el puerto 8000