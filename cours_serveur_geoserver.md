# Cartographie Web

* Diffuser des données cartographiques sur le web
  * Les standards de l'OGC
  * Exo - Manipulation des services
  * Outil - Présentation de géoserver
  * Exo - Installation et utilisation de géoserver

## GeoServer

A nous de créer nos flux de données

### Première connexion

On se connecte sur l'interface d'administration du GeoServer : [http://localhost:8080/geoserver](http://localhost:8080/geoserver)

Les identifiants sont : admin/geoserver

### Présentation de l'interface

De nombreuses actions sont possibles sur le GeoServer du paramétrage de configuration jusqu'à l'identification des utilisateurs.

Le sous-menu qui nous intéresse plus particulièrement c'est __Données__

* Prévisualisation de la couche : visualisation des couches de données
* Espaces de travail : gestion des différents projets
* Entrepôts : répertoire de données
* Couches : les données en elles-même 
* Agrégations de couches : mise sur une même couche de plusieurs couches
* Styles : styles en SLD 

### Ajout de nos données

On va donc ajouter les données qui ont été présentées précédemment dans un même espace de travail que l'on va nommer `world-overview`. 
Il existe plusieurs méthodes de chargement des données : 

#### Shapefile

On va ajouter les données _rivers_ et _ports_ en tant qu'entrepôt Shapefile

#### Postgis

On va ajouter les données _railroads_ et  _airports_ en tant qu'entrepôt PostGIS

### Symbolisation WMS

Ajouter à chacune de ces couches un style partculier => créer les styles sld propres à chaque couche

### Visualisation

On va visualiser nos couches dans QGIS

### Filtrage

#### Statique

http://espace-revendeurs3-geoserver.ign.fr:8080/geoserver/espace_revendeurs/wms?service=WMS&version=1.1.0&request=GetMap&layers=espace_revendeurs:routier-france-regionale&styles=&bbox=-5.2,41.3,9.5,51.1&width=768&height=511&srs=EPSG:4326&format=application/openlayers

Appuyer sur les '...' en haut à gauche de la carte

Dans le filtre CQL, `edition_number = 1` 

revient à ajouter 

`&filter=<filter><PropertyIsEqualTo><PropertyName>edition_number</PropertyName><Literal>1</Literal></PropertyIsEqualTo></filter>`

à la fin de la requête.

#### Dynamique

Dans l'interface de notre GeoServer, on va créer une vue qui va filtrer les ports en fonction de leur `scalerank`

_NB_ : on peut ajouter plusieurs viewparams qui sont séparés par des `;`

### Re-Visualisation

On va re-visualiser et tester nos couches dans QGIS
