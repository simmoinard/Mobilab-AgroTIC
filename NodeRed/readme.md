# NodeRed

NodeRed est un puissant outil No Code permettant de faire des liens entre plusieurs "Nodes". 

Note : Il faut d'abord se connecter en SSH au Raspberry pour pouvoir écrire les lignes de commandes de ce tuto.

## Installer NodeRed

On installe via le script officiel, puis on modifie le sysyemctl pour lancer NodeRed au démarrage. Enfin, on lance node-red : 

    bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
    sudo systemctl enable nodered.service
    node-red-start
    
NodeRed est alors accessible depuis n'importe quel ordinateur dans le réseau WiFi du Raspberry ! 
L'adresse URL est [IP]:1880 (par exemple, 192.168.104.163:1880)

## Sécuriser NodeRed

    node-red admin hash-pw

On renseigne le mot de passe de son choix. Il faut ensuite copier (```ctrl``` + ```C```) le mot de passe crypté qui en ressort. Attention, il y a un espace à la fin du mot de passe crypté, il faudra penser à l'enlever si vous l'avez séléctionné par erreur !

On se dirige ensuite dans le fichier de configuration ```settings.js```

    sudo nano ~/.node-red/settings.js
    
Appuyez sur ```Alt```+```C``` pour afficher le numéro des lignes. Descendre à la ligne n°76 pour modifier adminAuth : Il faut ici enlever les ```//``` en début de chaque ligne, puis choisir le username ainsi que le mot de passe crypté : 

    /** To password protect the Node-RED editor and admin API, the following
     * property can be used. See http://nodered.org/docs/security.html for details.
     */
    adminAuth: {
        type: "credentials",
        users: [{
            username: "moinards",
            password: "$2b$08$tYSS7NSXQ2ktIPEeo/53YeAn2HNEtMOnFOJz7hlXKv24ifX640FOK",
            permissions: "*"
        }]
    },

## Installer un plugin NodeRed

Les plugins de NodeRed sont disponibles dans la "palette" située dans le menu (3 barres horizontales en haut à droite), puis dans Manage Palette (accessible également via le raccourci ```Alt``` + ```↑``` + ```P```). Il faut ensuite cliquer sur l'onglet Install pour installer un nouveau Node.

Les modules commencent toujours par node-red-contrib. Les plus utilisés dans les projets du mobilab AgroTIC : 

- aedes : un  broker MQTT
- influxdb : Gérer la base de données Influx
- telegrambot : Communiquer avec un bot Telegram
