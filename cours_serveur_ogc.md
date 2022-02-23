# Cartographie Web

* Diffuser des données cartographiques sur le web
  * Les standards de l'OGC
  * Exo - Manipulation des services
  * Outil - Présentation de géoserver
  * Exo - Installation et utilisation de géoserver

## Diffuser des données cartographique

### Les standards de l'OGC

__Protocole de communication__ respectant des spécifications (définies par l'OGC)

### WMS

Web Map Service

Trois opérations ("requests") disponibles dans un service WMS retournant différents types de résultats :

* __GetCapabilities__ : méta-données (contenu du service et paramètres acceptés)
* __GetMap__ : __image__ d'une carte paramétrée relativement
* __GetFeatureInfo__ : informations sur un objet représenté sur la carte

#### Exemple de requête WMS

`protocole://nom_de_domaine(machine):port/serveur/workspace/service?parametres`

ou sinon

```
http://espace-revendeurs3-geoserver.ign.fr:8080/geoserver/espace_revendeurs/wms?
service=WMS&
version=1.1.0&
request=GetMap&
layers=espace_revendeurs:routier-france-departementale&
styles=&
bbox=-5.2,41.3,9.5,51.1&
width=768&
height=511&
srs=EPSG:4326&
format=image/gif
```

#### Paramètres

* _version_ : numéro de version WMS.
* _request_ : opération
* _format_ : format de sortie de l'image (exemple : image/png)
* _bbox_ : bounding box de la carte
* _width_ : largeur de l'image
* _height_ : hauteur de l'image
* _layers_ : liste des couches désirées
* _srs_ : système de projection
* _service_ : nom du service OGC (WMS donc)
* _styles_ : liste des styles utilisés pour chacune des LAYERS

##### Tests 

Modifier certains paramètres 
* width
* height
* bbox
* srs
* layers (affichage de 2 autres couches)
* format

#### Stylisation

Comme on envoie une __image__, on doit définir le style sur le serveur.
On utilise le SLD (Styled Layer Descriptor).

##### Exemple

```xml
<FeatureTypeStyle>
  <Rule>
    <PointSymbolizer>
      <Graphic>
        <Mark>
          <WellKnownName>circle</WellKnownName>
          <Fill>
            <CssParameter name="fill">#FF0000</CssParameter>
          </Fill>
          <Stroke>
            <CssParameter name="stroke">#000000</CssParameter>
            <CssParameter name="stroke-width">2</CssParameter>
          </Stroke>
        </Mark>
        <Size>6</Size>
      </Graphic>
    </PointSymbolizer>
  </Rule>
</FeatureTypeStyle>
```

Rendu

![sld](img/sld.png "sld")


##### Commentaires utiles

Il est possible de filtrer les objets que l'on veut afficher et leur affecter des styles selon leur type.

http://docs.geoserver.org/stable/en/user/styling/sld/cookbook/

#### Requete WMS dynamique

```
http://espace-revendeurs3-geoserver.ign.fr:8080/geoserver/espace_revendeurs/wms?
service=WMS&
version=1.1.0&
request=GetMap&
layers=espace_revendeurs:top-75-grid&
viewparams=grid:13001&
width=768&
height=511&
styles=&
bbox=-5.2,41.3,9.5,51.1&
srs=EPSG:4326&
format=application/openlayers
```

Changer de couche et de commune

### WMTS

Web Map Tile Service

Ressemblant au WMS mais se focalisant sur la perfomance : les __images__ sont des tuiles déjà calculées (par opposition au WMS : reprojection) que le serveur met à disposition

### WFS

Web Feature Service

5 opérations ("requests") pour envoyer des requêtes au serveur et obtenir des informations sur :

* __GetCapabilities__ : les capacités du serveur (quelles opérations sont supportées et quels objets sont fournis)
* __DescribeFeatureType__ : la structure de chaque entité susceptible d’être fournie par le serveur
* __GetFeature__ : la livraison d'objets
* __Transaction__ : la modification d'un objet (CRUD)
* __LockFeature__ : le bloquage des objets lors d'une transaction

#### Exemple de requête WFS

```
http://espace-revendeurs3-geoserver.ign.fr:8080/geoserver/espace_revendeurs/ows?
service=WFS&
version=1.0.0&
request=GetFeature&
typeName=espace_revendeurs:serie-bleue&
maxFeatures=50&
outputFormat=application/json
```

#### Paramètres

* _bbox_ : étendue des données
* _version_ : version
* _service_ : service (WFS)
* _srs_ : système de projection
* _request_ : opération
* _typeName_ : nom de la couche
* _maxFeatures_
* _outputFormat_
* filter

#### Filtrage 

```
http://espace-revendeurs3-geoserver.ign.fr:8080/geoserver/espace_revendeurs/ows?
service=WFS&
version=1.0.0&
request=GetFeature&
typeName=espace_revendeurs:top-25&
maxFeatures=100&
outputFormat=application/json&
filter=<filter><PropertyIsLessThan><PropertyName>sale</PropertyName><Literal>100</Literal></PropertyIsLessThan></filter>
```

#### Stylisation

La mise en style des données se fait côté client. Ce sera donc dans le script JavaScript que le style sera appliqué. 

## Autres services & standards

### KML

__Keyhole Markup Language__ basé sur le xml

#### Exemple

```kml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
<Document>
<Placemark>
  <name>ENSG</name>
  <description>École nationale des sciences géographiques</description>
  <Point>
    <coordinates>2.587327,48.841023,0</coordinates>
  </Point>
</Placemark>
</Document>
</kml>
```

### CSW

__Catalog Service for the Web__ pour faire la liste des données géographiques.

### Et bien d'autres

* Web Coverage Service (WCS)

* Web Processing Service (WPS)

* Styled Layer Descriptor (SLD)
