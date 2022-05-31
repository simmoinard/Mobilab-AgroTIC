# Mobilab-AgroTIC



## Ajout d'une gateway
https://docs.google.com/document/d/15u7gVZ0O7rmBvpWaHETV42GnluCNkuVWq6kZX1yau00/edit


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
