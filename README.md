# Explorer son historique de positions Google

## Etape1. Récupérer son historique de position Google

* Se rendre sur le site **https://takeout.google.com/settings/takeout**

* Cocher uniquement Historique de position
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/1.PNG)

* **Passer à l'étape suivante**

<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/2.PNG)

* **Exporter le ficher avec vos données** (par mail par exemple)
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/3.PNG)


* **Télécharger le  ficher avec vos données puis le décompresser**
<br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/4.PNG)


* **Dans le dossier, trouver le ficher Records.json** (qui contient tout votre historique de position)
<br> <br> ![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/5.PNG)

<br> <br>
## Etape2. Préparer les données

Le fichier fourni par Google qui centralise vos données est dans le format JSON qui n'est pas très pratique pour explorer des données spatiales, de plus les coordonnées géographiques qui y sont renseignées ne sont pas utilisables.
<br/>

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/JSON.PNG)


Ce petit **script R** permet de préparer le fichier de données brutes (JSON) pour le transformer en jeu de données utilisable (csv)

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



## 3. Explorer ses données de localisation Google dans une carte en ligne

Pour explorer en détail votre historique de positions Google vous pouvez utiliser le site **https://kepler.gl/demo**.

Il suffit de glisser/déplacer le csv dans votre navigateur Web et vos données s'affichent automatiquement sur la carte !

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/Kepler.PNG)


Ce site présente plusieurs avantages comme géolocaliser directement le csv, possibilité de visualiser à plusieurs échelle, affichage de fond de carte satellite et surtout les données restent stockées sur votre ordinateur !

Bonne exploration !

![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/Explorer.PNG)

