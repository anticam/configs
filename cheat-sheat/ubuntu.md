
install ssh client, server
```
sudo apt install openssh-client
sudo apt install openss-server
```

enable ssh server
```
sudo systemctl enable ssh
sudo systemctl start ssh
```

enable firewall ssh access
```
sudo ufw allow ssh
sudo ufw enable
sudo ufw status
```

start, stop, restart ssh
```
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
```
show status
```
sudo systemctl status ssh
```
