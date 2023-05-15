# GeoDataGoogle

## Etape1. Récupérer son historique de position

* Se rendre sur le site **https://takeout.google.com/settings/takeout**

* Cocher uniquement Historique de position
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/1.PNG)

* **Passer à l'étape suivante**

<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/2.PNG)

* **Exporter le ficher avec vos données** (par mail par exemple)
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/3.PNG)


* **Télécharger le  ficher avec vos données puis le décompresser**
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/4.PNG)


* **Trouver dans le dossier le ficher Records.json** (qui contien tout votre historique de position)
<br> <br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/5.PNG)

<br> <br>
## Etape2. Préparer les données

Le format proposé par Google est le JSON qui n'est pas très pratique pour explorer des données spatiales, de plus les coordonnées géographiques ne sont pas utilisables.
<br/>

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/JSON.PNG)


Ce petit **script R** permet de préparer la données brutes (json) en donnée utilisable (csv)

```{r}
#Package nécessaire
install.packages("jsonlite")
install.packages("tityverse")

library(jsonlite)
library(tidyverse)


#Importer le fichier json fournit par Google
data <- fromJSON("Records.json")

#Créer un csv pour visualiser vos données
locations = data$locations
locations$lat = locations$latitudeE7 / 1e7
locations$lon = locations$longitudeE7 / 1e7
Historiquedepositions <- locations %>% select(timestamp, dispositif = deviceTag, source, lat,lon)

write.csv(Historiquedepositions, 'Historiquedepositions.csv')
```

Voilà un joli **jeux de données bien structuré** !

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/Dataframe.PNG)

## 3. Explorer ses données de localisation nGoogle dans une carte en ligne

Pour explorer en détail votre historique de positions Google vous pouvez utiliser le site https://kepler.gl/demo.

Ce site présente plusieurs avantages comme géolocaliser directement le csv, possibilité de visualiser à plusieurs échelle, affichage de fond de carte satellite et surtout les données restent stockées sur votre ordinateur !

Bonne exploration !

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/Explorer.PNG)

