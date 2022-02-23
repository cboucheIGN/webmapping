# Cartographie Web

* Architecture d'une appli-carto
  * Séparation des responsabilités client-serveur
  * Le client -> affichage et manipulation des données
  * Le serveur -> diffusion des données
* [Afficher une carte sur une page web](cours_client.md)
  * Présentation de la librairie javascript Leaflet
  * Exo - Création d'une première carte
  * Exo - Exploration des outils carto - applat de couleurs
* Diffuser des données cartographiques sur le web
  * [Les standards de l'OGC](cours_serveur_ogc.md)
  * Exo - Manipulation des services
  * [Présentation de géoserver](cours_serveur_geoserver.md)
  * Exo - Installation et utilisation de géoserver

***Connaissances à maitriser***

* Principes : client et server
* Langages : HTML, CSS, Javascript, SQL
* Outils: librairies javascrit, framework nodejs, geoserver, console web

## Architecture d'une appli-carto

> TODO schema d'ensemble

Une application cartographique est un outil pour explorer des données géoréférencés.

Les usages sont nombreux et variés.
* Application d'itinéraire : voiture, transport en commun, avion...
* Application thématique : carte statistique
* Et encore d'autre usage....

La partie proche de l'utilisateur c'est l'application web qui s'affiche sur PC, téléphone, dans l'ordinateur de bord de votre voiture. Dans notre cours c'est la librairie javascript Leaflet qui nous permettra d'afficher une carte.

La partie loin de l'utilisateur c'est le serveur qui stocke les données. Dans notre cours c'est le logiciel Geoserver qui permettra de diffuser des données depuis une base PostgreSQL.

Entre ces deux parties, il peux y avoir un certain nombre d'intermédiaires qui participe à la transformation et la diffusion de la donnée.

Un developpeur peux travailler sur tous ces aspects (full-stack) ou se concentrer sur une partie (front-end / back-end).

### Le Client

> TODO schema architecture client

Côté client, il est possible de représenter de la données géographique de plusieurs manière.

Avec des cartes ! Voici quelques librairies cartographique.
* [Leaflet](https://leafletjs.com/index.html)
* [OpenLayers](https://openlayers.org/)
* [d3js](https://observablehq.com/@d3/bivariate-choropleth)
* Mais aussi de la cartographie en 3D [iTowns](http://www.itowns-project.org/itowns/examples/index.html#source_stream_wfs_25d)

Des graphiques pour accompagner les cartes.
* [Chartjs](https://www.chartjs.org/)
* [d3js](https://observablehq.com/@d3/diverging-stacked-bar-chart)

Sans oublier tout ce qu'on sait faire en HTML et CSS pour diffuser du texte, des images, des vidéos...

### Le Serveur

> TODO schema architecture serveur

Dans beaucoup de cas on sera consommateur de données. Par exemple nous ne geront pas le fond cartographique.

Mais si nous sommes producteur de données cartographique il nous faut un ensemble d'outil pour assurer la diffusion.

Un logiciel de gestion de base de données.
* [PostgreSQL](https://www.postgresql.org/)
* [MongoDB](https://www.mongodb.com/)

Un logiciel de diffusion de données
* [Geoserver](http://geoserver.org/)

Un Api Nodejs pour tout nos usages métiers autour des données.
* [Node.js](https://ensg_dei.gitlab.io/web-az/js/nodejs/)

