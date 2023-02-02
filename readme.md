# AW Instalación y configuración
Primero deberemos crear una instantanea y le daremos a _lanzar una instantanea_ 
![instantanea1]()




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
![Foto prueba]()