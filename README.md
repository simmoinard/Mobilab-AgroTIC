# Mobilab-AgroTIC

## Change Grafana logo : 
```
cd /usr/share/grafana/public/img/
```
rename grafana_icon.svg
Found [here](https://community.grafana.com/t/how-can-i-customize-login-page/17441/4)


## Ajout d'une gateway
https://docs.google.com/document/d/15u7gVZ0O7rmBvpWaHETV42GnluCNkuVWq6kZX1yau00/edit

# Raspberry

## Flasher une carte SD pour Raspberry
Télécharger [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
Paramétrer comme ceci : 

![image](https://user-images.githubusercontent.com/24956276/170987045-2e109392-74fc-4108-ad41-e181b20df4a6.png)

Lancer l'écriture et patienter jusqu'a 2 min. Vous pouvez enfin mettre la carte SD dans le Raspberry, puis brancher l'alimentation du Raspberry.

### Se connecter a distance au Raspberry
appuyer sur la touche ```Windows``` + ```R``` puis entrer ```cmd``` dans la barre de recherche

![image](https://user-images.githubusercontent.com/24956276/170989133-e635ebc2-8237-4ab5-8e5d-089efeb00b25.png)

    ssh pi@192.168.104.163

Le mot de passe est demandé (il a été paramétré au préalable). Bienvenue dans le Raspberry !!

### Fonctions de base : 

L'auto-complétion se fait en appuyant sur tab. C'est très pratique.

 - ```ls``` : lister les documents présents dans le répértoire courant
 - ```cd``` : Changer de répértoire
 - ```cd ..``` : revenir dans le répértoire parent
 - ```ls -l``` : lister les documents présents dans le répértoire courant avec plus d'informations (grâce au flag "-l")
 - ```mkdir``` : Créer un dossier
 - ```nano fichier.txt``` : Créer un fichier 'fichier.txt'. Pour sortir de l'éditeur, ```Ctrl```+```X```, puis ```Y```, puis ```Entrée``` 
 - ```sudo reboot``` : Redémarrer le Raspberry (sudo est pour Super User DO : on se met en mode admin, après avoir renseigné le mot de passe)

## Installer un serveur NodeRed / Grafana / Influx sur Raspberry

On commence toujours pas mettre à jour son Raspberry avant de commencer à installer des logiciels.

    sudo apt update
    sudo apt full-upgrade

### NodeRed

On installe via le script officiel, puis on modifie le sysyemctl pour lancer NodeRed au démarrage. Enfin, on lance node-red : 

    bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
    sudo systemctl enable nodered.service
    node-red-start
    
NodeRed est alors accessible depuis n'importe quel ordinateur dans le réseau WiFi du Raspberry ! 
L'adresse URL est [IP]:1880 (par exemple, 192.168.104.163:1880)

### Prometheus

[Prometheus](https://prometheus.io/download/) est une base de données temporelle. La suite est prise de ce [site](https://pimylifeup.com/raspberry-pi-prometheus/)

    wget https://github.com/prometheus/prometheus/releases/download/v2.35.0/prometheus-2.35.0.linux-amd64.tar.gz
    tar xzf prometheus-2.35.0.linux-amd64.tar.gz
    
 On nettoie ensuite l'installation :
 
    mv prometheus-2.35.0.linux-amd64/ prometheus/
    rm prometheus-2.35.0.linux-amd64.tar.gz
 
 Comme avec NodeRed, on va créer un service qui va lancer prometheus au démarrage :
 
    sudo nano /etc/systemd/system/prometheus.service   
    
 La fenêtre d'éditeur de texte "nano" s'ouvre. On copie ceci (clic-droit pour coller dans nano) :
 
 ```
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network-online.target

[Service]
User=pi
Restart=on-failure

ExecStart=/home/pi/prometheus/prometheus \
  --config.file=/home/pi/prometheus/prometheus.yml \
  --storage.tsdb.path=/home/pi/prometheus/data

[Install]
WantedBy=multi-user.target
```

Pour sortir de l'éditeur nano , ```Ctrl```+```X```, puis ```Y```, puis ```Entrée```

On fini par activer ce service : 

    sudo systemctl enable prometheus
    sudo systemctl start prometheus
    sudo systemctl enable prometheus

Prometheus est alors accessible depuis n'importe quel ordinateur dans le réseau WiFi du Raspberry ! 
L'adresse URL est [IP]:9090 (par exemple, 192.168.104.163:9090)
