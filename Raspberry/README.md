# Raspberry

Raspberry est un petit ordinateur monocarte. Il permet d'automatiser plein de systèmes, visualiser des données, etc. 

## Flasher une carte SD pour Raspberry

Insérer la carte SD dans l'ordinateur.
Télécharger [Raspberry Pi Imager](https://downloads.raspberrypi.org/imager/imager_latest.exe)

Ouvrir ce logiciel puis choisir le premier OS ainsi que la carte SD. Cliquer ensuite sur l'engrenage et paramétrer comme ceci : 

<p align="center">
  <img src="https://user-images.githubusercontent.com/24956276/170987045-2e109392-74fc-4108-ad41-e181b20df4a6.png">
</p>

- ```Set Hostname``` permet de définir le nom du Raspberry (ici raspberrypi.local)
- ```Enable SSH``` permet de se connecter à distance au Raspberry
- ```set username and password``` permet de définir un nom d'utilisateur et un mot de passe. Ici, le ```Username``` est pi. Le mot de passe vous sera demandé plusieurs fois dans la suite des tutoriels.
- ```Configure Wireless LAN``` : cette partie permet de se connecter directement à un réseau WiFi. Le ```SSID``` est le nom du WiFi et ```password``` le mot de passe
- ```Wireless LAN Country``` est optionnel
- ```Set locale settings``` est optionnel

Lancer l'écriture et patienter jusqu'a 2 min. Vous pouvez enfin mettre la carte SD dans le Raspberry, puis brancher l'alimentation du Raspberry.

## Se connecter en SSH au Raspberry dans un réseau local

Important : il faut que l'ordinateur et le Raspberry soient connectés au même réseau ! Le Raspberry s'est connecté automatiquement au réseau Wifi renseigné avec Raspberry Pi Imager. Il faut maintenant que l'ordinateur soit également dans ce réseau !

appuyer sur la touche ```Windows```+```R``` puis entrer ```cmd``` dans la barre de recherche, puis entrer 

    ssh pi@raspberrypi.local

(note : la commande est ```username```@```hostname``` comme ils ont été défini plus haut au moment du flash de la carte SD)

S'il est marqué 'l'hôte est introuvable', il faut plutot chercher l'adresse IP du raspberry. On peut la trouver en tapant :

    for /L %a in (1,1,254) do start ping 192.168.1.%a
    arp -a
    
L'une des adresses Internet (ou IP) affichées de type 'dynamique' est celle du Rasbperry. De façon générale, les adresses physiques des Raspberry commencent toujours par ```e4-5f-01```, ```DC-A6-32```, ```B8-27-EB``` ou ```28-CD-C1```. Il faut donc faire le lien pour retrouver l'adresse IP.

<p align="center">
  <img src="https://user-images.githubusercontent.com/24956276/171141408-7703d013-2f3f-4543-9d85-f77c418300b1.png">
</p>

D'après l'image, l'adresse IP que je cherche est ```192.168.104.163```, associée à l'adresse physique commencant par ```e4-5f-01```. La commande a utiliser est donc : 

    ssh pi@192.168.104.163

Le mot de passe est demandé (il a été paramétré au préalable). Bienvenue dans le Raspberry !!

### Fonctions de base : 

Dans cette fenêtre noire, on peut entrer une multitude de commandes. On peut essayer les suivantes : 
 - ```ls``` : lister les documents présents dans le répértoire courant
 - ```cd``` : Changer de répértoire
 - ```cd ..``` : revenir dans le répértoire parent
 - ```ls -l``` : lister les documents présents dans le répértoire courant avec plus d'informations (grâce au flag "-l")
 - ```mkdir``` : Créer un dossier
 - ```nano fichier.txt``` : Créer un fichier 'fichier.txt'. Pour sortir de l'éditeur, ```Ctrl```+```X```, puis ```Y```, puis ```Entrée``` 
 - ```sudo reboot``` : Redémarrer le Raspberry (sudo est pour Super User DO : on se met en mode admin, après avoir renseigné le mot de passe)
 - ```ifconfig``` : Redémarrer le Raspberry (sudo est pour Super User DO : on se met en mode admin, après avoir renseigné le mot de passe)

Note : L'auto-complétion se fait en appuyant sur la touche ```tab```. C'est très pratique : par exemple, pour la commande ```ifconfig``` on peut taper ```if``` puis double ```tab``` pour voir toutes les propositions. S'il ne reste qu'une proposition (par exemple en tapant ```ifc``` puis un ```tab```), l'autocomplétion va se faire et il n'est pas nécessaire de terminer la commande !

## Installer un serveur NodeRed / Grafana / Influx sur Raspberry

Dans le mobilab AgroTIC, plusieurs logiciels sont très utilisés : 

- InfluxDB pour stocker les données dans une base : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/InfluxDB/README.md)
- NodeRed pour connecter des objets a des programmes : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/NodeRed/README.md)
- Grafana pour visualiser ces données : [tuto d'installation](https://github.com/simmoinard/Mobilab-AgroTIC/blob/main/Raspberry/Grafana/README.md)

