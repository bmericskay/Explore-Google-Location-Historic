# GeoDataGoogle

## Etape1. Récupérer son historique de position

* Se rendre sur le site https://takeout.google.com/settings/takeout

* Cocher uniquement Historique de position
![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/1.PNG)

* Passer à l'étape suivante
![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/2.PNG)

* Exporter le ficher avec vos données (par mail par exemple)
![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/3.PNG)


* Télécharger le  ficher avec vos données puis le décompresser
![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/4.PNG)


* Trouver dans le dossier le ficher Records.json (qui contien tout votre historique de position)
![alt text](https://raw.githubusercontent.com/bmericskay/GeoDataGoogle/main/5.PNG)


## Etape2. Préparer les données

Ce petit script R permet de préparer la données brutes (json) en donnée utilisable (csv)

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
write.csv(Historiquedepositions, 'google.csv')
```


## 3. Explorer ses données de localisation nGoogle dans une carte en ligne
