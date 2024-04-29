### SSH server

[cyberciti](https://www.cyberciti.biz/faq/how-to-install-ssh-on-ubuntu-linux-using-apt-get/)  
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

### Docker compose

[docker.docs](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)  

uninstall packages
```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

setup docker's repository
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

install latest version
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

verify installation
```
sudo docker run hello-world
```
### Mount

install nfs-common
```
sudo apt install nfs-common
sudo apt install cifs-utils
```

create new mount point
```
sudo mkdir /mnt/wdc
```

mount the drive named /dev/sdb1 at /mnt/wdc
```
sudo mount /dev/sdb1 /mnt/wdc
# verify using df command or mount command
df -H
mount
```

edit fstab for ext4
```
/dev/sdb1    /mnt/wdc   ext4    defaults     0        2
```



