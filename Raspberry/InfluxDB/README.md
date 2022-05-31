# InfluxDB

InfluxDB est une base de données temporelle, qui permet de stocker les données de capteurs etc.
Note : Il faut d'abord se connecter en SSH au Raspberry pour pouvoir écrire les lignes de commandes de ce tuto.

## Installation de InfluxDB

On commence toujours pas mettre à jour son Raspberry avant de commencer à installer des logiciels :

    sudo apt update
    sudo apt full-upgrade

   ~~sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install apt-transport-https
    sudo apt-get install curl
    curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -~~
    
    echo "deb https://repos.influxdata.com/debian stretch stable" | sudo tee /etc/apt/sources.list.d/influxdb.list 
    sudo apt-get update
    sudo apt-get install influxdb
    
    sudo systemctl enable influxdb.service
    sudo systemctl start influxdb.service

## Configuration de Influx
Il faut enfin configurer le fichier influxdb.conf. On ouvre l'editeur de texte nano :

    sudo nano /etc/influxdb/influxdb.conf

Appuyez sur ```Alt```+```C``` pour afficher le numéro des lignes. Descendre à la ligne n°249 pour modifier la balise [HTTP] : Il faut ici enlever les ```#``` en début de 3 lignes, comme ceci : 

    [http]
      # Determines whether HTTP endpoint is enabled.
      enabled = true

      # The bind address used by the HTTP service.
      bind-address = ":8086"

      # Determines whether user authentication is enabled over HTTP/HTTPS.
      auth-enabled = false
 
Pour sortir de l'éditeur nano , ```Ctrl```+```X```, puis ```Y```, puis ```Entrée```
