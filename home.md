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

