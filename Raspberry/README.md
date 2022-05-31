# Raspberry

Raspberry est un petit ordinateur monocarte. Il permet d'automatiser plein de systèmes, visualiser des données, etc. 

## Flasher une carte SD pour Raspberry
Télécharger [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
Paramétrer comme ceci : 

<p align="center">
  <img src="https://user-images.githubusercontent.com/24956276/170987045-2e109392-74fc-4108-ad41-e181b20df4a6.png">
</p>

Lancer l'écriture et patienter jusqu'a 2 min. Vous pouvez enfin mettre la carte SD dans le Raspberry, puis brancher l'alimentation du Raspberry.

## Se connecter en SSH au Raspberry dans un réseau local

Important : il faut que l'ordinateur et le Raspberry soient connectés au même réseau ! Le Raspberry s'est connecté automatiquement au réseau Wifi renseigné avec Raspberry Pi Imager. Il faut maintenant que l'ordinateur soit également dans ce réseau !

appuyer sur la touche ```Windows``` + ```R``` puis entrer ```cmd``` dans la barre de recherche

    ssh pi@raspberrypi.local

S'il est marqué 'l'hôte est introuvable', il faut plutot chercher l'adresse IP du raspberry. On peut la trouver en scannant le réseau via l'application Network Analyser sur telephone.

    ssh pi@192.168.104.163

Le mot de passe est demandé (il a été paramétré au préalable). Bienvenue dans le Raspberry !!

### Fonctions de base : 

Dans cette fenêtre noire, on peut entrer une multitude de commandes. On peut essayer les suivante : 
 - ```ls``` : lister les documents présents dans le répértoire courant
 - ```cd``` : Changer de répértoire
 - ```cd ..``` : revenir dans le répértoire parent
 - ```ls -l``` : lister les documents présents dans le répértoire courant avec plus d'informations (grâce au flag "-l")
 - ```mkdir``` : Créer un dossier
 - ```nano fichier.txt``` : Créer un fichier 'fichier.txt'. Pour sortir de l'éditeur, ```Ctrl```+```X```, puis ```Y```, puis ```Entrée``` 
 - ```sudo reboot``` : Redémarrer le Raspberry (sudo est pour Super User DO : on se met en mode admin, après avoir renseigné le mot de passe)
 - ```ifconfig``` : Redémarrer le Raspberry (sudo est pour Super User DO : on se met en mode admin, après avoir renseigné le mot de passe)

Note : L'auto-complétion se fait en appuyant sur tab. C'est très pratique : par exemple, pour la commande ```ifconfig``` on peut taper ```if``` puis double ```tab``` pour voir toutes les propositions. S'il ne reste qu'une proposition (par exemple en tapant ```ifc``` puis un ```tab```), l'autocomplétion va se faire et il n'est pas nécessaire de terminer la commande !

## Installer un serveur NodeRed / Grafana / Influx sur Raspberry

Dans le mobilab AgroTIC, plusieurs logiciels sont très utilisés : 

- NodeRed pour connecter des objets a des programmes : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/NodeRed/README.md)
- InfluxDB pour stocker les données dans une base : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/InfluxDB/README.md)
- Grafana pour visualiser ces données : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/Grafana/README.md)

