# Codigos utiles en docker

## docker container
* `docker container run --name proxy nginx` : monta un contenerdor con la imagen nginx y el nombre proxy.
* `docker ps` : lista los contenedores que hay 
* `docker container ls` : lista los contenerdores que hay
* `docker container run -it` : start new container interactively
* `docker container exec -it` : run aditional comand in existing container
* `docker container run  -it --name proxy nginx bash`
* `docker container exec -it mysql bash` : entra al shell para ejecutar comandos
* `docker container logs -f <containerId>` : muestra los logs del contenedor
* `docker container top <containerID>` : muestra los servicios ejecutados dentro del contenedor
* `docker container inspect <containerID>` :  Muestra la configuración de todo el contenedor
* `docker container stats`: muesta el consumo en rendiemiento de todos los contenedores ejecutados

## network
* `docker container run -p 40:80 --name webhost -d nginx`
* `docker container port webhost` : muestra el puerto por el cual esta montada la aplicacción
* `docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost` : muestra la direccion ip del contenedor
* `docker network ls` : lista todas las redes que hay 
* `docker network inspect`
* `docker network create --driver`
* `docker network connect`
* `docker network disconnect`
* `docker network create my_app_net` : crea una nueva red
* `docker container run -d --name new_nginx --network my_app_net`: crea un contenedor con una red 
------------------
* `docker container run --rm -it centos:7 bash` : crea un contenedor y se elimina cuando se sale del bash.
* `docker network creade dude` : crea una nueva red llamada dude

## Dockerfile
* FROM: imagen minima para empezar, aphine, debian, ubuntu, centos, defora
* ENV: environment variables
* RUN: corre los script que necesitemos
* EXPOSE: expone el puerto en la coneccion virtual de docker
* CMD: configura el comando a correr 


* WORKDIR: escoge la carpeta de trabajo
* COPY : copia toda los archivos locales en la imagen

-----------------------
* `docker image build -t customnginx .` : crea una imagen con la configuracion del dockerfile
* `docker volume ls`: Muestra todos los volumenes que hay 
* `docker volume create --`: crea un nuevo volumen, es necesario crearlo antes de correr 'docker run'
* `docker run -p 80:4000 -v $(pwd)`
* `docker run -dp 3000:3000 -w /app -v "$(pwd):/app" node:12-alpine sh -c "yarn install  && yarn run dev"`

## docker swarm

* `docker info`: ver la configuración de docker.
* `docker swarn init`: inicia docker swarn
* `docker node ls`: muestra los nodos creados
* `docker service --help`: los servicios son lo mismo que contenedores pero estos funcionan con swarn
* `docker service ls`: lista todos los servicios
* `docker service create alpine ping 8.8.8.8`: monta un servicio con la imagen alpine
* `docker service ps <name>`: muestra información detallada del servicio name
* `docker service update <ID> --replicas 3`: actualiza el numero de replicas del servicio a 3
