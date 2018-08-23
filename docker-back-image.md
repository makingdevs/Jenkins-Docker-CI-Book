## Realizar respaldos y cargas de imagenes en docker


* Realizar un respaldo
* Recuperar una imagen respaldada

### Realizar un respaldo

Se puede repaldar imagenes de docker para moverlas de docker host o simplemente para respaldarlas

`docker images`

![](/assets/dockerImages.png)

`docker save centos > centos.tar `

![](/assets/backupImages.png)

El resultado es un tar con el respaldo de la imagen, en el server de 23 y 24 (Jenkins y QA) se encuentran los respaldos de la imagenes (/u01/backup_images)

### Recuperar una imagen respaldada

Ahora si deseamos recuperar la imagen ya respaldada con el siguiente comando logramos recuperarla 

`docker load < centos.tar`

y con ello recuperamos automaticamente la imagen respaldada