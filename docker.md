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
PUID=1000  #docker user UID
PGID=1000  #group ID of docker user
TZ=<country>/<city>
DOCKERDIR=/home/<docker user>/docker
$VS_USER_PASSWORD=123456
```

Extensions
[Home Assistant Config Helper](https://marketplace.visualstudio.com/items?itemName=keesschollaart.vscode-home-assistant)
long live token needed

[Log File Highliter](https://marketplace.visualstudio.com/items?itemName=emilast.LogFileHighlighter)

[ESPHome](https://marketplace.visualstudio.com/items?itemName=ESPHome.esphome-vscode)
manual installation needed


[Material Design Icons Intellisense](https://marketplace.visualstudio.com/items?itemName=lukas-tr.materialdesignicons-intellisense)

[indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)

[YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)

[vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)


