<!-- TITLE: Docker -->
<!-- SUBTITLE: Breu resum de docker amb ordres principals -->

# Docker
## Docker-compose
Per poder desenvolupar codi seguint aquest funcionament es segueix sempre el mateix esquema:

*  Per aixecar tots els serveis: `docker-compose up --build`
*  Per aixecar un servei concret: `docker-compose up --build <nom_servei1> <nom_serveiN>`
*  En cas que es necessitin definir variables d'entorn es farà en la mateixa comanda: `ENV=xxx IMAGE_TAG=xxx docker-compose up --build`


## Comandes vàries
Un seguit de comandes per treballar amb docker / docker-compose:

*  Eliminar totes les imatges, volums, i xarxes que no s'estiguin utilitzant **actualment**: `docker system prune --all`
*  Crear una xarxa dins de docker (normalment només cal fer-ho una vegada): `docker network create <nom_xarxa>`
*  Veure quins containers estan en funcionament: `docker ps`
*  Veure consum de recursos de cada container: `docker stats`
*  Inspeccionar en profunditat un container concret: `docker inspect <id_container>`


### Creació d'un Swarm
Per crear un Swarm seguint l'esquema explicat fins ara s'han de seguir els següents passos:

*  Crear el manager i màquina on s'executarà el gitlab-runner a través de la AMI predefinida a EC2. Un cop s'ha creat s'hi entra i s'inicialitza el swarm seguint les següents instruccions:
```shell
sudo usermod -aG docker $USER
docker swarm init
docker network create --driver=overlay public
docker node update --label-add special=monitoring <id_manager>
```

*  Crear els workers a través de EC2. Per tal que s'afegeixin els nodes automàticament al swarm s'ha d'executar l'ordre: `docker swarm join-token worker` al manager previament creat. Després s'enganxa aquest codi en l'apartat de **Advanced details** al crear la màquina, de tal manera que quedi així (per exemple):
```shell
#!/bin/bash

sudo docker swarm join --token SWMTKN-1-3wgcctmd8irr94wcrh1k9y2dnutl5gasxlr1fm7a6aa2d4q0hb-b492uielyctm6g8lwjwz6bium 172.31.37.136:2377
```

*  (OPCIONAL) Crear els managers seguint el mateix procediment anterior canviant worker per manager.

Altres ordres importants:

```sh
docker stack ls
docker stack ps [service]
docker service logs -f -t --tail=50 ppui0jbx2d24
```


Amb aquests senzills passos ja tenim el swarm creat i a punt per començar a posar els diferents projectes a través de Gitlab.

Per comprovar els serveis:

`docker stack services imbee2fb`

Per reiniciar un contenidor dins de un swarm:

`docker service scale imbee2fb_imbee2fb=0`
`docker service scale imbee2fb_imbee2fb=1`

# Wiki.js
## Configuració

```text
davidcrx@davidcrx:~$ nodejs wiki.js --help

Usage: node wiki.js <cmd> [args]

Comandos:
  start             Start Wiki.js process
  stop              Stop Wiki.js process
  restart           Restart Wiki.js process
  configure [port]  Configure Wiki.js using the web-based setup wizard

Opciones:
  --help     Muestra ayuda                                            [booleano]
  --version  Muestra número de versión                                [booleano]

Read the docs at https://wiki.requarks.io
```











