## Realizar el depurado de Docker

### Purge de las imagenes inecesarias

Para el purgado de la informacion de docker existen diferentes comandos, entre uno de ellos se encuentra 

`docker system prune`

Sin embargo este comando no es muy recomendable ya que practicamente limpia todo a excepción los contenedores que estan corriendo.

El siguiente comando funciona para el limpiado de las imagenes en cache y imagenes que no se usan para la creacion de un contenedor. Es un limpiado sin probocar ningun problema.

`docker rmi $(docker images -q -f dangling=true)`

Para complementar este funcion, se creo una tarea en el jenkins para programar un tarea de ejecucion cada cierto tiempo (configurable se quedo con una ejecucion cada hora). ejecuntando un sh para detonante de el comando anterior.

![](/assets/jenkinsCleanDocker.png)
![](/assets/shDockerClean.png)

El archico clean docker es el siguiente 

```
#!/bin/sh

docker rmi $(docker images -q -f dangling=true)

exit 0;
```

Los servers que quedan configurados son el 172.31.100.25(DEVL CLOUD), 172.31.100.24(QA CLOUD), 10.31.23.60(QA local)

