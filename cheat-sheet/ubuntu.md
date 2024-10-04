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

### SSH keys
[ssh keys](https://ubuntu.com/server/docs/openssh-server)  
generate keys 
```
ssh-keygen -t rsa
```
or
```
ssh-keygen -t rsa -b 4096
```

public key is saved in ~/.ssh/id_rsa.pub
private key is saved in ~/.ssh/id_rsa
copy id_rsa.pub file to the remote host and append it to ~/.ssh/authorized_keys
```
ssh-copy-id username@remotehost
```
check permissions authorized_keys file
```
chmod 600 .ssh/authorized_keys
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

#### Post install step  
enable non-root user  

create docker group
```
sudo groupadd docker
```

add user to the docker group
```
sudo usermod -aG docker $USER
```
activate changes
```
newgrp docker
```
verify that you can run docker without sudo
```
docker run hello-world
```

#### Docker network
create new network
```
docker network create  <network>
```

### Mount
[cyberciti](https://www.cyberciti.biz/faq/mount-drive-from-command-line-ubuntu-linux/)  
[DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-20-04)


install nfs-common
```
sudo apt install nfs-common
sudo apt install cifs-utils
```
list path to drives
```
lsblk -lf
```
#### Mount a drive

create new mount point
```
sudo mkdir -p /mnt/wdc
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
mount based on /etc/fstab file content
```
sudo mount -av
```

#### Mount an NFS
create new mount point
```
sudo mkdir -p /mnt/wdc/music
```

mount the the network share
```shell
sudo mount host_ip:/media/music /mnt/wdc/music
```

check status
```
df -h
du -sh /mnt/wdc/music
```

mount the remote directory at boot
```
sudo nano /etc/fstab
```

/etc/fstab
```
host_ip:/media/music               /mnt/wdc/music      nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0

```

unmounting an NFS remote share
```
sudo umount /mnt/wdc/music
```
check status
```
df -h
```


