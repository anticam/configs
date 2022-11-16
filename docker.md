## Containers
- [ ] Deluge  
- [x] Code-Server  
- [x] Mosquitto
- [ ] ESPHome
- [x] Portainer
- [x] WatchTower
- [x] InfluxDB
- [x] Grafana
- [x] Home Assistant
- [x] Zigbee2MQTT
- [ ] Node-Red 
- [ ] Traefik
- [ ] Gitea
- [x] Piwigo
- [ ] Calibre
- [ ] Calibre-web
- [ ] Cloudflared
- [ ] Diun
- [ ] Dozzle
- [ ] Duplicati
- [x] Postgres
- [ ] PG Admin
- [ ] Ampache
- [ ] Airsonic
- [x] Adminer
- [ ] Vaultwarden
- [ ] AdGuard
- [ ] Pi-Hole
- [x] MariaDB
- [ ] MongoDB / Mongo Express
- [ ] Bookstack
- [ ] Fail2Ban
- [ ] DokuWiki

### Deluge
deluge [docker container](https://hub.docker.com/r/linuxserver/deluge)  

### Code-Server
[BeardedTinker](https://www.youtube.com/c/BeardedTinker) [Installation](https://www.youtube.com/watch?v=sarfQVmWlr0&list=TLPQMzAxMDIwMjJ1jA0SUXRoLQ&index=1)

docker
https://hub.docker.com/r/linuxserver/code-server

docker-compose
```
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ
      - PASSWORD=$VS_USER_PASSWORD #optional
      #- HASHED_PASSWORD= #optional
      - SUDO_PASSWORD=$VS_SHADOW_PASSWORD #optional
      #- SUDO_PASSWORD_HASH= #optional
      #- PROXY_DOMAIN=code-server.my.domain #optional
      - DEFAULT_WORKSPACE=/config/vscode #optional
    volumes:
      - $DOCKERDIR:/config
    ports:
      - 8443:8443
    restart: unless-stopped
```

where environment variables are stored in .env file:
```
# USER
PUID=1000  #docker user UID
PGID=1000  #group ID of docker user
TZ=<country>/<city>
DOCKERDIR=/home/<docker user>/docker

# VSCode
VS_USER_PASSWORD=123456
```

Extensions
1. [Home Assistant Config Helper](https://marketplace.visualstudio.com/items?itemName=keesschollaart.vscode-home-assistant)
2. [Log File Highliter](https://marketplace.visualstudio.com/items?itemName=emilast.LogFileHighlighter)
3. [ESPHome](https://marketplace.visualstudio.com/items?itemName=ESPHome.esphome-vscode)
(manual installation needed)
4. [Material Design Icons Intellisense](https://marketplace.visualstudio.com/items?itemName=lukas-tr.materialdesignicons-intellisense)
5. [indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)
6. [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)
7. [vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)


### Mosquitto
BeardedTinker [Eclipse MQTT 2.x in Docker + user credentials on Synology](https://www.youtube.com/watch?v=ABb-63y0Em4)  
[Mosquitto (MQTT) in Docker for Home Assistant on Synology](https://www.youtube.com/watch?v=eJjkgkS_Wqw&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=35)  
Docker image [eclipse-.misquitto](https://hub.docker.com/_/eclipse-mosquitto)  

Create folders under docker
```
mkdir mqtt
mkdir mqtt/config
mkdir mqtt/data
mkdir mqtt/log
```

In mqtt/config create mosquitt.conf file
```
touch mqtt/config/mosquitto.conf
```
content
```
persistence true
persistence_location /mosquitto/data
log_dest file /mosquitto/log/mosquitto.log
#password_file /mosquitto/config/pwfile
allow_anonymous true
listener 1883
```


docker-compose file
```
  mosquitto:
    image: eclipse-mosquitto
    container_name: mosquitto
    environment:
      - TZ=$TZ
    volumes:
      - $DOCKERDIR/mqtt/config:/config
      - $DOCKERDIR/mqtt/data:/data
      - $DOCKERDIR/mqtt/log:/log
      - $DOCKERDIR/mqtt/config/mosquitto.conf:/mosquitto/config/mosquitto.conf
    ports:
      - 1883:1883
      - 9001:9001
    restart: unless-stopped
```
open console to container
```
docker-compose exec mosquitto ash
```
in shell create password file and populate with users
```
cd mosquitto/config
touch pwfile
```

populate the pwfile with user/password pairs:
```
mosquitto_passwd -c pwfile hass
Password:
Reenter password:
```
or  
```
mosquitto_passwd -b pwfile home assistant
```

The mosquiotto.conf can be updated to use the password file:
```
persistence true
persistence_location /mosquitto/data
log_dest file /mosquitto/log/mosquitto.log
password_file /mosquitto/config/pwfile
#allow_anonymous true
listener 1883
```
### ESPHome

### Portainer

create portainer folder under docker
```
mkdir docker/portainer
mkdir docker/portainer/data
```

docker-compose [docker hub](https://hub.docker.com/r/portainer/portainer-ce)
```
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    ports:
      - 9000:9000
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ
    labels:
      - "diun.enable=true"
    command: -H unix:///var/run/docker.sock
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - $DOCKERDIR/portainer/data:/data
    restart: always      
```      

### WatchTower

docker-compose [watchtower](https://containrrr.dev/watchtower/)
```
  watchtower:
    image: containrrr/watchtower:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      #- /etc/localtime:/etc/localtime:ro
    environment:
      TZ: $TZ
      WATCHTOWER_LABEL_ENABLE: 'true'
      WATCHTOWER_POLL_INTERVAL: 86400
      WATCHTOWER_INCLUDE_STOPPED: 'true'
      WATCHTOWER_CLEANUP: 'true'
      WATCHTOWER_REVIVE_STOPPED: 'false'
      WATCHTOWER_NOTIFICATIONS: email
      WATCHTOWER_NOTIFICATION_EMAIL_FROM: $SMTP_FROM
      WATCHTOWER_NOTIFICATION_EMAIL_TO: $SMTP_TO
      WATCHTOWER_NOTIFICATION_EMAIL_SERVER: $SMTP_HOST
      WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PORT: $SMTP_PORT
      WATCHTOWER_NOTIFICATION_EMAIL_SERVER_USER: $SMTP_USER
      WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PASSWORD: $SMTP_PASSWORD
      WATCHTOWER_NOTIFICATION_EMAIL_DELAY: 2
```
containers to update:
```
label:
  - com.centurylinklabs.watchtower.enable=true
```  
containers to monitor:
```
label:
  - com.centurylinklabs.watchtower.monitor-only=true
```

### InfluxDB

BeardedTinker [Portainer, Watchtower and InfluxDB for Home Assistant on Synology](https://www.youtube.com/watch?v=jtVelxopKTM&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=37)

https://github.com/docker-library/docs/blob/master/influxdb/README.md


create inlfuxdb under docker
```
mkdir docker/influxdb2
mkdir docker/influxdb2/data
mkdir docker/influxdb2/config
```

docker-compose
```
  influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - 8086:8086
    volumes:
      - $DOCKERDIR/influxdb2/data:/var/lib/influxdb2
      - $DOCKERDIR/influxdb2/config:/etc/influxdb2
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=$INFLUX_INIT_USER
      - DOCKER_INFLUXDB_INIT_PASSWORD=$INFLUX_INIT_USER_PASSWORD
      - DOCKER_INFLUXDB_INIT_ORG=$INFLUX_INIT_ORG
      - DOCKER_INFLUXDB_INIT_BUCKET=$INFLUX_INIT_BUCKET
    labels:
      - diun.enable=true
        #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true
    restart: always        
```

### Grafana

docker - https://hub.docker.com/r/grafana/grafana/
[installation](https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/#configure-docker-image)
[configuration](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/)

create grafana folder under docker
```
mkdir docker/grafana
```

docker-compose
```
  grafana:
    image: grafana/grafana-oss
    container_name: grafana
    ports:
      - 3080:3000
    volumes:
      - $DOCKERDIR/grafana:/var/lib/grafana
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ
      - GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-simple-json-datasource
    labels:
    - diun.enable=true
    - com.centurylinklabs.watchtower.monitor-only=true
    restart: unless-stopped   
```

### Home Assistant

BeardedTinker - [Home Assistant on Synology inside Docker](https://www.youtube.com/watch?v=pcnvmAOah_Y&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=38&t=505s)

Create home-assistant folder under docker
```
mkdir home-assistant
```
docker-compose
Home Assistant [docker-compose](https://www.home-assistant.io/installation/linux#docker-compose)
[linuxserver](https://docs.linuxserver.io/images/docker-homeassistant)

```
  home-assistant:
    image: lscr.io/linuxserver/homeassistant:latest
    container_name: home-assistant
    environment:
      - PUID=$PUID
      - PGID=$PGID  
      - TZ=$TZ
    volumes:
      - $DOCKERDIR/home-assistant:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    privileged: true
    ports:
      - 8123:8123
    network_mode: host
    restart: unless-stopped
```

pull and start docker
```
docker-compose pull home-assistant
sudo docker-compose up home-assistant -d
```

Smart Home Addict
[Statistics in Home Assistant with InfluxDB and Grafana](https://www.youtube.com/watch?v=KM6UC4tMVYo)

Everything Smart Home
[NEXT LEVEL STATISTICS - Home Assistant InfluxDB and Grafana](https://www.youtube.com/watch?v=eJ-XE2tsD4U)


BeardedTinker
[Portainer, Watchtower and InfluxDB for Home Assistant on Synology ](https://www.youtube.com/watch?v=jtVelxopKTM&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=37)


BeardedTinker
[Grafana Docker for Home Assistant on Synology](https://www.youtube.com/watch?v=Q5t7ld2be3k&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=36)

Bluetooth stack reset
```
$ sudo hciconfig hci0 reset
$ sudo invoke-rc.d bluetooth restart
```

#### Migration from HASSIO to docker version
BeardedTinker - [How to migrate from hassio to Home Assistant Core on Synology](https://www.youtube.com/watch?v=reg1Hf0eKTU&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=9)


### Zigbee2MQTT
Zigbee2MQTT [docker](https://www.zigbee2mqtt.io/guide/installation/02_docker.html#creating-the-initial-configuration)
BeardedTinker [Zigbee2MQTT](https://www.youtube.com/watch?v=HbkXQErileU&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=34)

Create folders under docker
```
mkdir zigbee2mqtt
mkdir zigbee2mqtt/data
```

in zigbee2mqtt folder execute:
```
docky@docky:~/docker/zigbee2mqtt$ wget https://raw.githubusercontent.com/Koenkk/zigbee2mqtt/master/data/configuration.yaml -P data
```
it creates a configuration.yaml in data folder

get zigbee module ID
```
ls -l /dev/serial/by-id
total 0
lrwxrwxrwx 1 root root 13 okt   29 22:33 usb-Silicon_Labs_slae.sh_cc2652rb_stick_-_slaesh_s_iot_stuff_00_12_4B_00_23_93_3A_72-if00-port0 -> ../../ttyUSB0
lrwxrwxrwx 1 root root 13 okt   29 22:33 usb-Texas_Instruments_TI_CC2531_USB_CDC___0X00124B001938DD82-if00 -> ../../ttyACM0  <<< zigbee module
```

docker-compose
```
  zigbee2mqtt:
    image: koenkk/zigbee2mqtt
    container_name: zigbee2mqtt
    environment:
      - TZ=$TZ
    user: $PUID:$PGID
    group_add: 
      - dialout       
    devices:
      # Make sure this matched your adapter location
      - /dev/serial/by-id/usb-Silicon_Labs_slae.sh_cc2652rb_stick_-_slaesh_s_iot_stuff_00_12_4B_00_23_93_3A_72-if00-port0:/dev/ttyUSB0
    volumes:
      - $DOCKERDIR/zigbee2mqtt/data:/app/data
      - /run/udev:/run/udev:ro
    ports:
      # Frontend port
      - 8080:8080
    restart: unless-stopped
```

add user to theses groups
[guide](https://www.zigbee2mqtt.io/guide/installation/20_zigbee2mqtt-fails-to-start.html#method-2-add-your-user-to-specific-groups)
```
sudo usermod -a -G uucp $USER
sudo usermod -a -G tty $USER
sudo usermod -a -G dialout $USER
```

test module access as docker user
```
test -w /dev/ttyUSB0 && echo success || echo failure
```
and with sudo
```
sudo test -w /dev/ttyUSB0 && echo success || echo failure
```
in docker/zigbee2mqtt/data/configuration.yaml set port
```
serial:
  # Location of USB sniffer
  port: /dev/ttyUSB0
```

### Node-Red 

https://nodered.org/docs/getting-started/docker  
https://hub.docker.com/r/nodered/node-red  
BeardedTinker - [Node-RED in Docker for Home Assistant on Synology](https://www.youtube.com/watch?v=YdgoIdjZtKA)  
BurnsHA - [Node-Red in Docker with Home Assistant!!](https://www.youtube.com/watch?v=fxo5-iiwZXk)  
[Installing Node Red in Docker for Home Assistant](https://jordanrounds.com/installing-node-red-in-docker-for-home-assistant/)

docker-compose
```
  node-red:
    image: nodered/node-red:latest
    container_name: node-red
    environment:
      - TZ=$TZ
    user: 1000:1000
    ports:
      - "1880:1880"
    networks:
      - node-red-net
    volumes:
      - $DOCKERDIR/node-red:/data
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true  
    restart: unless-stopped    
```

### Traefik

### GiTea

https://docs.gitea.io/en-us/install-with-docker-rootless/
Just Me and Opensource - [Gitea - Git with a cup of tea - Installation and Configuration](https://www.youtube.com/watch?v=y9zDbMkuXdE)

```
# 
# https://docs.gitea.io/en-us/install-with-docker/
#
  gitea:
    image: gitea/gitea:latest
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
      #- PUID=$PUID
      #- PGID=$PGID
      #- TZ=$TZ
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true
    volumes:
      - /mnt/wdc/gitea/data:/data
      - /mnt/wdc/gitea/config:/config
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "2222:22"
    networks:
      - web
    restart: unless-stopped
```

### Piwigo

create piwigo folder under docker
```
mkdir docker/piwigo
mkdir docker/piwigo/config
mkdir docker/piwigo/gallery
```

docker-compose [linuxserver](https://docs.linuxserver.io/images/docker-piwigo)
```
  piwigo:
    image: lscr.io/linuxserver/piwigo:latest
    container_name: piwigo
    environment:
      - PUID=$PUID
      - PGID=$PUID
      - TZ=$TZ
    volumes:
      - $DOCKERDIR/piwigo/config:/config
      - $DOCKERDIR/piwigo/gallery:/gallery
    ports:
      - 608:80
    restart: unless-stopped
```

In MariaDB create piwigo_db DB (utf8mb4_general_ci)


### Calibre

### Calibre-web

### Cloudflared
docker-compose https://hub.docker.com/r/erisamoe/cloudflared

### Diun

### Dozzle

[Dozzle](https://dozzle.dev/) the docker log viewer
docker-compose [docker hub](https://hub.docker.com/r/amir20/dozzle/)
```
  dozzle:
    container_name: dozzle
    image: amir20/dozzle:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 9999:8080
```
### Duplicati

https://www.duplicati.com/
[Home Automation Guy](https://www.youtube.com/c/HomeAutomationGuy) - [Backing up Home Assistant Container](https://www.youtube.com/watch?v=pJqPhYXeulk)

[docker-compose](https://hub.docker.com/r/linuxserver/duplicati)
```
  duplicati:
    image: lscr.io/linuxserver/duplicati:latest
    container_name: duplicati
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CLI_ARGS= #optional
    volumes:
      - </path/to/appdata/config>:/config
      - </path/to/backups>:/backups
      - </path/to/source>:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```

### Postgres

https://hub.docker.com/_/postgres

create postgres folder under docker
```
mkdir docker/postgres
mkdir docker/postgres/data15
```
[docker-compose](https://geshan.com.np/blog/2021/12/docker-postgres/)
```
  postgres:
    image: postgres:15
    container_name: postgres
    restart: always
    ports:
      - 5432:5432
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - $DOCKERDIR/postgres/data15:/var/lib/postgresql/data
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true
```

### PG Admin

[pgadmin](https://www.pgadmin.org/download/pgadmin-4-container/)  

create pgadmin folder under docker
```
mkdir docker/pgadmin
```

https://github.com/khezen/compose-postgres/blob/master/docker-compose.yml
docker-compose https://hub.docker.com/r/dpage/pgadmin4/  
```
  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4
    environment:
      - PGADMIN_DEFAULT_EMAIL: $SMTP_TO
      - PGADMIN_DEFAULT_PASSWORD: $PG_ADMIN_PASSWORD
      - PGADMIN_CONFIG_SERVER_MODE: 'False'
    volumes:
       - $DOCKERDIR/pgadmin:/var/lib/pgadmin
    ports:
      - 5050:80
    restart: unless-stopped
```

### Ampache

### Airsonic

### Adminer

docker-compose [docker hub](https://hub.docker.com/_/adminer/)
```
  adminer:
    image: adminer:latest
    restart: always
    ports:
      - 7080:8080
    labels:
      - diun.enable=true
```      

### Vaultwarden
[docker image](https://hub.docker.com/r/vaultwarden/server)
BeardedTnker [VaultWarden self hosted password manager in Synology private cloud](https://www.youtube.com/watch?v=V3kJHoLuKxQ&list=PLWlpiQXaMerS9IkaN9Off6RxoYCiP5edb&index=7)

Christian Lempa - [Self Hosted Password Manager - Your data under your control!](https://www.youtube.com/watch?v=ub8jj96_Q3g)

create vaultwarden folder under docker:
```
mkdir docker/vaultwarden
```

[docker compose configuration](https://github.com/dani-garcia/vaultwarden/wiki/Using-Docker-Compose)
```
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: always
    environment:
      - PUID=$PUID
      - PGID=$PGID  
      - TZ=$TZ
      #- WEBSOCKET_ENABLED: "true"  # Enable WebSocket notifications.
    volumes:
      - $DOCKERDIR/vaultwarden/data:/data

```
Note, it needs a reverse proxy to us HTTPS.

### AdGuard

### Pi-Hole

### MariaDB

create mariadb folder under docker
```
mkdir docker/mariadb
```

docker-compose [linuxserver](https://docs.linuxserver.io/images/docker-mariadb)

```
  mariadb:
    image: lscr.io/linuxserver/mariadb:latest
    container_name: mariadb
    ports:
      - 3306:3306
    environment:
      - PUID=$PUID
      - PGID=$PGID
      - TZ=$TZ    
      - MYSQL_ROOT_PASSWORD=omeiS5oobae1yaPo
    volumes:
      - $DOCKERDIR/mariadb:/config
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true
    restart: always
```

### MongoDB / Mongo Express

https://hub.docker.com/_/mongo  
[Using MongoDB with Docker](https://earthly.dev/blog/mongodb-docker/)  
[Running MongoDB as a Docker Container](https://www.baeldung.com/linux/mongodb-as-docker-container)  
[How To Run MongoDB as a Docker Container](https://www.bmc.com/blogs/mongodb-docker-container/)  
https://www.mongodb.com/compatibility/docker  

created mongodb folder under docker
```
mkdir docker/mongodb
```

docker-compose
```
  mongodb:
    image: mongo:latest
    container_name: mongodb
    ports:
      - 27017:27017
    environment:
      - PUID=$PUID
      - PGID=$PGID    
      - MONGO_INITDB_ROOT_USERNAME=$MONGO_ROOT_USERNAME
      - MONGO_INITDB_ROOT_PASSWORD=$MONGO_ROOT_PASSWORD
    volumes:
      - $DOCKERDIR/mongodb:/data/db
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true      
    restart: unless-stopped
```

Mongo Express  
docker-compose [image](https://hub.docker.com/_/mongo-express)  

```
  mongo-express:
    image: mongo-express:latest
    container_name: mongo-express
    ports:
      - 27020:8081
    environment:
      PUID: $PUID
      PGID: $PGID
      ME_CONFIG_MONGODB_SERVER: mongodb
      ME_CONFIG_MONGODB_PORT: 27017
      ME_CONFIG_BASICAUTH_USERNAME: $ME_USERNAME 
      ME_CONFIG_BASICAUTH_PASSWORD: $ME_PASSWORD 
      ME_CONFIG_MONGODB_ADMINUSERNAME: $MONGO_ROOT_USERNAME
      ME_CONFIG_MONGODB_ADMINPASSWORD: $MONGO_ROOT_PASSWORD
    labels:
      - diun.enable=true
      #- com.centurylinklabs.watchtower.enable=true
      - com.centurylinklabs.watchtower.monitor-only=true      
    restart: unless-stopped
```
