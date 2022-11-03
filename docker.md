## Containers
- [ ] Deluge  
- [x] Code-Server  
- [x] Mosquitto
- [ ] ESPHome
- [x] Portainer
- [ ] WatchTower
- [ ] InfluxDB
- [x] Home Assistant
- [x] Zigbee2MQTT
- [ ] Node-Red 
- [ ] Traefik
- [ ] Gitea
- [x] Piwigo
- [ ] Calibre
- [ ] Calibre-web
- [ ] Diun
- [ ] Postgres
- [ ] Ampache
- [ ] Airsonic
- [x] Adminer
- [ ] Vaultwarden
- [ ] AdGuard
- [ ] Pi-Hole
- [x] MariaDB

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

### InfluxDB

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

### Traefik

### GiTea

https://docs.gitea.io/en-us/install-with-docker-rootless/

### Piwigio

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

### Diun

### Postgres

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
      - diun.watch_repo=true
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
      - MARIADB_ROOT_PASSWORD=password
    volumes:
      - $DOCKERDIR/mariadb/:/var/lib/mysql
    restart: always
```

