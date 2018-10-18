## Creacion Server Postgress

### Como levantar server de postgress en un server

Para el funcionamiento correcto de ciertas aplicaciones como es el caso de faltas y suplencias es necesario un server de postgress. Por ello se crea un contenedor con el server de postgress, la creacion es muy sencilla solo basta la ejecución de el siguiete comando  

`docker run --name postgres -dit --restart unless-stopped --network general-ebc-network -v /home/rflgs418/backup_postgres:/var/lib/postgresql/data -p 5432:5432 -e POSTGRES_USER=postgres -d postgres`

En donde se pasa como variable de entorno POSTGRES_USER con el user que se desea dar de alta. Este puede ser cualquier otro pero para mantener la convencion se elige este nombre. 

Asi mismo se crea un volumen para que toda la info de las bases sean almacenadas en el directorio que se muestra, este es un firectorio del file system del server host, y por ultimo se agrega a la red de ebc de docker para que todos los contenedores puedan acceder a la base sin problema.