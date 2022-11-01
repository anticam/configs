## Containers
- [ ] Deluge  
- [x] Code-Server  
- [x] Mosquitto
- [ ] Portainer
- [ ] WatchTower
- [ ] InfluxDB
- [ ] Home Assistant
- [ ] Zigbee2MQTT
- [ ] Node-Red 
- [ ] Traefik
- [ ] GiTea
- [ ] Piwigo
- [ ] Calibre
- [ ] Calibre-web
- [ ] Diun
- [ ] Postgres
- [ ] Ampache
- [ ] Airsonic
- [ ] Adminer

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
      - PUID=$PUID
      - PGID=$PGID
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

populate the file with user/password pairs:
```
mosquitto_passwd -c pwfile hass
Password:
Reenter password:
```
or  
```
mosquitto_passwd -b home assistant
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

### Portainer

### WatchTower

### InfluxDB

### Home Assistant

### Zigbee2MQTT

### Node-Red 

### Traefik

### GiTea

### Piwigio

### Calibre

### Calibre-web

### Diun

### Postgres

### Ampache

### Airsonic

### Adminer
