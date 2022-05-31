
# Grafana

Grafana est un logiciel qui permet de visualiser les données issues d'une base de données (comme Influx). 

Note : Il faut d'abord se connecter en SSH au Raspberry pour pouvoir écrire les lignes de commandes de ce tuto.

## Installation de Grafana
 ~~sudo apt-get install apt-transport-https curl~~
 
 On commence toujours pas mettre à jour son Raspberry avant de commencer à installer des logiciels :

    sudo apt update
    sudo apt full-upgrade
  
 On ajoute un répertoire à aller checker lors des prochains updates
 
    curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
    echo "deb https://dl.bintray.com/fg2it/deb stretch main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
 
 On met à jour et on installe Grafana 
 
    sudo apt-get update
    sudo apt-get install grafana
 On active Grafana au démarrage du Raspberry et on le démarre
 
    sudo systemctl enable grafana-server.service 
    sudo systemctl start influxdb.service

## Paramétrage de Grafana

Il faut configurer le fichier grafana.ini. On ouvre l'editeur de texte nano :

    sudo nano /etc/grafana/grafana.ini

Appuyez sur ```Alt```+```C``` pour afficher le numéro des lignes. Descendre à la ligne n°33 pour modifier la balise [server] : Il faut ici enlever les ```;``` en début de ligne, comme ceci : 

    [server]
    # Protocol (http, https, socket)
    protocol = http

    # The ip address to bind to, empty will bind to all interfaces
    ;http_addr =

    # The http port  to use
    http_port = 3000
 
Pour sortir de l'éditeur nano , ```Ctrl```+```X```, puis ```Y```, puis ```Entrée```

à partir de maintenant, on peut aller sur la page Grafana depuis un navigateur classique (Chrome, Friefox, etc) via l'adresse ```raspberrypi.local:3000```

## Changer le logo Grafana : 

    cd /usr/share/grafana/public/img/

Puis renommer grafana_icon.svg

Found [here](https://community.grafana.com/t/how-can-i-customize-login-page/17441/4)
