## Instalacion Jenkins CD 

### Instalacion Master

Lo primero que se debe realizar para la instalación del master de jenkins es crear la carpeta la el respaldo de la info (Volumen) del contenedor.

`/u01/jenkins_home_cd`

Para que el contendor pueda acceder a la carpeta y almacenar la info necesaria debemos ejecutar el siguiente comando para darle permisos a la carpeta al usuario jenkins 

`chown jenkins:jenkins  jenkins_home_cd`

Y porteriormente vamos a correr el nuevo contenedor copn el siguiente comando

`docker run -dit --restart unless-stopped -d --name jenkins_cd -e JNLP_PROTOCOL_OPTS=-Dorg.jenkinsci.remoting.engine.JnlpProtocol3.disabled=false -p 8082:8080 -p 50001:50000 -v /u01/jenkins_home_cd:/var/jenkins_home jenkins/jenkins:lts`


Con ellos tendremos el jenkins arriba, en este caso en el puerto 8082 del server en el que se esta instalando.

### Instalacion Slave del Jenkins CD

La instalacion del slave es el mismo que para la del jenkins principal de la EBC 

[Creación del Jenkins Slaves](instalacion-de-jenkins-slaves.md)

### Intalacion de elixir y erlang para el slave

Este proceso de instalacion debe realizarse dentro del contenedor del slave, entramos con el siguiente comando `docker exec -u root -i -t slave-cd-2 /bin/bash` si nos damos cuenta estamos entrando con el usuario root ya que necesitamos permisos para la instalacion dentro del contenedor

#### Preinstalacion de erlang 

Antes de iniciar la instalacion es recomendable realizar la actualizacion del apt-get 

`apt-get update`

`apt-get upgrade`

Se necesita alguna bibliotecas para la inatacion correcta de erlang y elixir 

`apt-get install libxml2-utils xsltproc fop unixodbc unixodbc-bin unixodbc-dev`

Despues de esto ahora si podemos empezar la instalacion de erlang

#### Instalacion de Erlang y Elixir 

Realizacion la descarga del archivo .deb de erlang 

`wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb`

Eh instalamos el mismo 

`dpkg -i erlang-solutions_1.0_all.deb`

Actualizamos apt-get `apt-get update` y posteriormente instalamos Erlang (Nota este proceso puede durar varios minutos).

`apt-get install esl-erlang`

Con ello ya tendremos instalado erlang.

Despues realizamos la instalacion de Elixir.

`apt-get install elixir`

Una vez la instalacion exitosa terminamos el proceso de instalacion de Erlang y Elixir

#### Post Instalacion de Elixir 

Debemos salir e igresar nuevamente al contenedor `docker exec -i -t slave-cd-2 /bin/bash` pero ahora sin acceso root es decir con el usuario jenkins, esto para inciar algunos comandos de elixir 

`mix local.hex`


Listo con ellos se tendria listo el slave y jenkins de CD