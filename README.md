# splunk-gns3

## Instalación de Splunk y recogida de logs de máquinas Mikrotik, Ubuntu, Vyos, CentOS en Splunk creadas mediante GNS3.

Vamos a realizar un ejercicio donde instalaremos splunk en una máquina virtual Debian, el programa que utilizaremos para virtualizar dicha máquina será VMWare.


### Instalación de Splunk

Tenemos un Debian 10 actualizado y virtualizado en VMWare, para instalar Splunk es bastante sencillo, nos iremos a la [página de descargas de Splunk](https://www.splunk.com/en_us/download/splunk-enterprise.html).
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

Se nos pedirá aceptar la licencia y crear un usuario administrador para poder operar con splunk, una vez hecho ya podremos acceder a la web mediante el puerto 8000.

![](./splunk1.jpg)


### Instalación de GNS3

GNS3 es una aplicación que nos permite jugar con escenarios complejos de redes, en este caso lo vamos a utilizar para virtualizar las máquinas Mikrotik, Ubuntu, Vyos y CentOS pedidas en el ejercicio.

Para instalarlo simplemente nos vamos a la [página de descargas de GNS3](https://www.gns3.com/software/download), en mi caso instalé la de Windows que es la máquina donde tengo la máquina virtual de Splunk instalada.

Muy importante escoger la opción de GNS3 VM y ponerla en VMWare que es donde mejor funciona la virtualización.

Una vez instalado tendremos esta ventana:
![](./gns3-1.png)

Crearemos un nuevo proyecto en la pestaña File -> New Blank Project y elegimos el nombre que queramos para el proyecto.

Para la instalación de las máquinas, primero debemos darle a File -> New Templates -> Install an appliance from the GNS3 server.

Escogeremos la imagen que queramos, en este caso nos descargaremos las de Cisco, Mikrotik, Vyos y Ubuntu, y nos quedaría así:

![](./gns3-2.png)
![](./gns3-3.png)


#### Creación de Interfaz Loopback

Para conectar todas las máquinas en una red y que pueda acceder a nuestro servidor de Syslog, debemos crear una interfaz loopback en nuestro ordenador, para ello daremos a la tecla Windows+R y escribiremos hdwwiz

En dicha pestaña elegiremos la opción de Buscar e instalar software automáticamente -> Adaptadores de Red -> Microsoft -> Adaptador de bucle invertido KV-TEST de Microsoft.

Una vez tengamos la red nos saldrá en nuestros adaptadores de redes:
![](./loopback1.png)

Ahora simplemente debemos compartir nuestra red con dicha interfaz, para ello damos click derecho a nuestra interfaz de red internet/ethernet -> Propiedades -> Uso Compartido y elegimos nuestra interfaz Loopback

![](./loopback2.png)

#### Creación de Red Loopback en GNS3

Para crear una red que se conecte a nuestro Loopback, simplemente vamos a Browse End Devices -> Cloud y lo arrastramos al escenario.

Le damos a click derecho -> Configure -> Show special Ethernet interfaces y elegimos nuestra interfaz loopback y le damos a add, si queremos podemos eliminar las otras que ya están.

![](./loopback3.png)

Simplemente tendremos que conectar las máquinas a cada Cloud y ya las tendremos para configurar en la misma red.

![](./loopback4.png)