# Docker-compose
- Om Nextcloud + database in een Docker-compose te laten draaien. Hebben we de vm van de vorige opdracht nodig met Docker. 

- Om te beginnen maken we een nieuw folder:

```bash
mkdir nextcloud
```
-we gaan naar de nieuw folder navigeren, plus maken een Docker-compose.yml file:

```bash
cd nextcloud && touch docker-compose.yml
```
- deze file gaan we bewerken:

```bash
nano docker-compose.yml
```
- hier in gaan we de volgende instellingen in kopiëren:

```bash
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=Welkome01
      - MYSQL_PASSWORD=Welkome01
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 1337:80
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
    environment:
      - MYSQL_PASSWORD=Welkome01
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```
- In dit bestand hebben we de data base aangemaakt, het wachtwoord ingesteld voor de database dat is Welkome01. Ook is het poort nummer naar 1337 gezet.
-Om de docker-compose aan te zetten doen we het volgende commando: 
```bash
> docker-compose up -d
```
- als dit allemaal gelukt is dan zie je de volgende pagina met nextcloud.# school
