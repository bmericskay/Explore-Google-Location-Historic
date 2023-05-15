# GeoDataGoogle

## Récupérer son historique de position

![alt text]([http://url/to/img.png](https://github.com/bmericskay/GeoDataGoogle/blob/main/1.PNG))


## Préparer les données

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


## Visualiser ses données Google dans une carte en ligne
