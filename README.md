# Codigos utiles en docker

## Docker container

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
* `docker container run -p 40:80 --name webhost -d nginx`
* `docker container port webhost` : muestra el puerto por el cual esta montada la aplicacción
* `docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost` : muestra la direccion ip del contenedor
* `docker container run -d --name new_nginx --network my_app_net`: crea un contenedor con una red
* `docker container run --rm -it centos:7 bash` : crea un contenedor y se elimina cuando se sale del bash.

## Network

* `docker network ls` : lista todas las redes que hay
* `docker network inspect <networkId>`: Muestra el detalle de una red
* `docker network create --driver <networkName>`: Crea una red con el nombre <networkName> y le asigna el controlador a la red
* `docker network connect <networkId> <networkName>`: Asigna la red <networkName> a <containerName>
* `docker network disconnect <networkId> <networkName>`: Elimina la red <networkName> de <containerName>
* `docker network create <networkName>` : Crea una red con el nombre <networkName>
  
## DNS

* `docker network create dude`: Crea una red llamada dude
* `docker container run -d --network dude --network-alias search elasticsearch:2`: Crea un contenedor de la imagen elasticseach, le asigna la red dude y un alias en la red de search
* `docker container run -d --network dude --network-alias search elasticsearch:2`: Crea un contenedor de la imagen elasticseach, le asigna la red dude y un alias en la red de search
* `docker container run --rm --network dude alpine nslookup search`: ejecuta el comando nslookup en el contenedor y lo elimina

## Dockerfile

* FROM: imagen minima para empezar, aphine, debian, ubuntu, centos, defora
* ENV: environment variables
* RUN: corre los script que necesitemos
* EXPOSE: expone el puerto en la coneccion virtual de docker
* CMD: configura el comando a correr
* WORKDIR: escoge la carpeta de trabajo
* COPY : copia toda los archivos locales en la imagen

## volumens

* `docker volume create <nombre_volume>` : crea un volumen nuevo con el nombre <nombre_volumen>
* `docker container run -v <nombre_volume>:<workdir_destination>`: corre un contenedor con el nombre con un volumen
### bind mounts
* `docker container run -v <path_host>:<path_container>`: crea una montura de la carpeta <path_host> y lo copia todo en <path_container>

------------------------

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
* `docker service rm <ID>`: elimina el servio y tambien todos los contenedores asociados al servicio
* `docker swarm join-token manager`: obtiene el script para asignar mas nodos
* `docker node update --role manager <nodeId>`: actualiza el rol del node
* `dockern network create --driver overlay <Name>`: crea una red con el driver overlay y el nombre <name>
* `docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=mypass postgres`: crea un servicio con el nombre psql conectandolo a la red mydrupal y usando la imagen postgres
*  `docker service inspect <serviceName>`: muestra en detalle la configuracion del servicio

## Docker secrets

* `docker secret create <secretName> <value>`: crea un secreto con el nombre <secretName> y el valor <value> el valor puede estar en un archivo txt
* `docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres`: crea un servicio con los secretos de docker secrets
  
