## 👋 Welcome to wireguard 🚀  

wireguard README  
  
  
## Requires scripts to be installed  

```shell
 sudo bash -c "$(curl -q -LSsf "https://github.com/systemmgr/installer/raw/main/install.sh")"
 systemmgr --config && systemmgr install scripts  
```

## Automatic install/update  

```shell
dockermgr update wireguard
```

OR

```shell
mkdir -p "$HOME/.local/share/srv/docker/wireguard/rootfs"
git clone "https://github.com/dockermgr/wireguard" "$HOME/.local/share/CasjaysDev/dockermgr/wireguard"
cp -Rfva "$HOME/.local/share/CasjaysDev/dockermgr/wireguard/rootfs/." "$HOME/.local/share/srv/docker/wireguard/rootfs/"
```

## via command line  

```shell
docker pull casjaysdevdocker/wireguard:latest && \
docker run -d \
--restart always \
--privileged \
--name casjaysdevdocker-wireguard \
--hostname casjaysdevdocker-wireguard \
-e TZ=${TIMEZONE:-America/New_York} \
-v $HOME/.local/share/srv/docker/casjaysdevdocker-wireguard/rootfs/data:/data:z \
-v $HOME/.local/share/srv/docker/casjaysdevdocker-wireguard/rootfs/config:/config:z \
-p 80:80 \
casjaysdevdocker/wireguard:latest
```

## via docker-compose  

```yaml
version: "2"
services:
  ProjectName:
    image: casjaysdevdocker/wireguard
    container_name: ProjectName
    environment:
      - TZ=America/New_York
      - HOSTNAME=casjaysdevdocker-wireguard
    volumes:
      - $HOME/.local/share/srv/docker/casjaysdevdocker-wireguard/rootfs/data:/data:z
      - $HOME/.local/share/srv/docker/casjaysdevdocker-wireguard/rootfs/config:/config:z
    ports:
      - 80:80
    restart: always
```

## Author  

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🤖 casjaysdevdocker: [Github](https://github.com/casjaysdevdocker) [Docker](https://hub.docker.com/r/casjaysdevdocker) 🤖  
