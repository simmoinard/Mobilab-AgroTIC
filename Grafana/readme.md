
# Grafana

Grafana est un logiciel qui permet de visualiser les données issues d'une base de données (comme Influx). 

## Installation de Grafana
 ~~sudo apt-get install apt-transport-https curl~~
 
    curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
    echo "deb https://dl.bintray.com/fg2it/deb stretch main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
    sudo apt-get update
    sudo apt-get install grafana
    
    sudo systemctl enable grafana-server.service 
    sudo systemctl start influxdb.service

Il faut enfin configurer le fichier grafana.ini. On ouvre l'editeur de texte nano :

    sudo nano /etc/grafana/grafana.ini

Il faut descendre avec les flèches du clavier jusqu'a trouver "server", puis enlever les 2 ```;``` comme ci-dessous : 
    
    [server]
    # Protocol (http, https, socket)
    protocol = http

    # The ip address to bind to, empty will bind to all interfaces
    ;http_addr =

    # The http port  to use
    http_port = 3000
 
Pour sortir de l'éditeur nano , ```Ctrl```+```X```, puis ```Y```, puis ```Entrée```

## Changer le logo Grafana : 
```
cd /usr/share/grafana/public/img/

```
renomer grafana_icon.svg
Found [here](https://community.grafana.com/t/how-can-i-customize-login-page/17441/4)
