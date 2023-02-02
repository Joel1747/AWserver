# AW Instalación y configuración
Primero deberemos crear una instantanea y le daremos a _lanzar una instantanea_ 

![instantanea1](https://github.com/Joel1747/AWserver/blob/master/imagenes/instantanea.png)

Lo siguente será generar las claves y seleccionar el tipo de instancia

![instantanea2](https://github.com/Joel1747/AWserver/blob/master/imagenes/instantanea2.png)

y por último tendremos que lanzar la instantanea

![instantanea3](https://github.com/Joel1747/AWserver/blob/master/imagenes/instantanea3.png)

## Conexión con la instancia
seleccionaremos la instancia y le daremos a conectar,donde nos llevará a la siguente ventana en la cual le daremos a _conexion mediante ssh_

![Conectar](https://github.com/Joel1747/AWserver/blob/master/imagenes/Conectar.png)

Iremos a nuestro terminal ssh y compiaremos la linea que pone ejemplo e indicaremos la ruta donde hemos guardado la clave privada.

## Habilitar root
entrar a la instancia y realizar lo siguiente 

darle permisos al root para conectar por ssh

_nano /etc/ssh/sshd_config_

cambiar la línea a esa en el fichero
_PermitRootLogin without-password_

restartear el servicio con _service sshd restart_

## Conectar con Root
hacemos _sudo su -_ para ponernos en modo superusuario

borrar los comandos anteriores a ssh-rsa del fichero  _root/.ssh/authorized_keys_
_nano .ssh/authorized_keys_

cambiamos el usuario en este caso de ec2-user a root y nos conectamos mediante shh
_ssh -i "clavesSRI.pem" root@ec2-35-181-155-57.eu-west-3.compute.amazonaws.com al entrar con el usuario_ 

Podremos entrar con root sin problemas ya

## Entrar desde visual code
Para ello debemos entrar en el visual, pulsar _f1_ el cual nos desplegará una ventanita en la cual pondremos _añadir nuevo host_ y nos pedirá dicho host, pondremos el comando que usamos para entrar mediante shh.

![visual](https://github.com/Joel1747/AWserver/blob/master/imagenes/visual.png)

## Fichero _.ssh/config_
En este fichero podremos ver los host que hemos añadidio, a los cuales podremos cambiarle el nombre y hacer mas facil el acceso

Poner bien la ruta absoluta en IdentityFile de la ubicación de la clave y comprobar que se conecta mediante ssh y el “host” que le hemos cambiado el nombre.

![ConfUser](https://github.com/Joel1747/AWserver/blob/master/imagenes/sshConf.png)

## Conexión mediante visual
Pulsaremos _f1_,pondremos conectarnos con host y en función de que queramos hacen en este caso podemos o bien conectarnos con root para temas de configuración y esas cosas, o bien con ec2-user para crear los sitios y los htmls correspondientes.
![ConexiónRoot](https://github.com/Joel1747/AWserver/blob/master/imagenes/Conexi%C3%B3nRoot.png)

Recordar cuando hagamos cambios en la configuración del nginx debemos reiniciar el sistema con el comando.
~~~
service nginx restart
~~~
### Cambio usuario que ejecuta el proceso
Si accedemos coon root y vamos a la configuración en el fichero _nginx.conf_ podremos cambiar el usuario que lanza el proceso del servicio.

![]()
## Creación sitios _nginx_ 

Para ello crearemos dos carpetas distintas en las que guardaremos en cada una un html, despues entraremos conmo root y accederemos a la configuración y crearemos un fichero de configuracion en la carpeta _conf.d_  

### Configuración fichero llamado _sitios.conf_
El fichero tendra que ser algo parecido a esto en función de lo que nos haga falta.
~~~
server {

    location /fabulosas { 
        alias /home/ec2-user/pagina1;
     }

    location /fantastica {		
        alias /home/ec2-user/pagina2;	
    }
}
~~~ 

### Prueba funcionamiento

![Foto prueba](https://github.com/Joel1747/AWserver/blob/master/imagenes/Captura%20de%20pantalla%20de%202023-02-02%2016-59-19.png)