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
mkdir -p "$HOME/.local/share/srv/docker/wireguard/volumes"
git clone "https://github.com/dockermgr/wireguard" "$HOME/.local/share/CasjaysDev/dockermgr/wireguard"
cp -Rfva "$HOME/.local/share/CasjaysDev/dockermgr/wireguard/volumes/." "$HOME/.local/share/srv/docker/wireguard/volumes/"
```

## via command line  

```shell
docker pull casjaysdevdocker/wireguard:latest && \
docker run -d \
  --name=casjaysdevdocker-wireguard-latest \
  --env TZ=America/New_York \
  --privileged \
  --cpus 2 \
  --shm-size=128M \
  --restart=always \
  --tty \
  --hostname vpn.$HOSTNAME \
  --network bridge \
  --env PASSWORD='my_very_secure_password' \
  --env ENV_PORTS="51820 51821" \
  --env WG_HOST="vpn.$HOSTNAME" \
  --env WG_PORT='51820' \
  --env WG_MTU='1420' \
  --env WG_PERSISTENT_KEEPALIVE='30' \
  --env WG_DEFAULT_ADDRESS='10.8.0.x' \
  --env WG_DEFAULT_DNS='10.0.0.1, 150.230.183.65, 1.1.1.1' \
  --env WG_ALLOWED_IPS='0.0.0.0/0, ::/0' \
  --env WG_PRE_UP='' \
  --env WG_POST_UP='iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE' \
  --env WG_PRE_DOWN='' \
  --env WG_POST_DOWN='iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE' \
  --cap-add CAP_CHOWN \
  --cap-add SYS_TIME \
  --cap-add SYS_ADMIN \
  --cap-add SYS_MODULE \
  --cap-add CAP_NET_ADMIN \
  --sysctl "net.ipv4.conf.all.src_valid_mark=1" \
  --sysctl "net.ipv4.ip_forward=1" \
  --volume /root/.local/share/srv/docker/wireguard/volumes/config/wireguard:/etc/wireguard \
  --volume /root/.local/share/srv/docker/wireguard/volumes/data:/data:z \
  --volume /root/.local/share/srv/docker/wireguard/volumes/config:/config:z \
  --volume /lib/modules:/lib/modules \
  --publish 0.0.0.0:51820:51820/udp \
  --publish 127.0.0.10:50453:51821 \
  casjaysdevdocker/wireguard:latest
```

## via docker-compose  

```yaml
version: '3.3'
services:
    wireguard:
        container_name: casjaysdevdocker-wireguard-latest
        privileged: true
        hostname: vpn.$HOSTNAME
        network_mode: bridge
        environment:
            - TZ=America/New_York
            - PASSWORD=my_very_secure_password
            - WG_HOST=vpn.$HOSTNAME
            - WG_PORT=51820
            - WG_MTU=1420
            - WG_PERSISTENT_KEEPALIVE=30
            - WG_DEFAULT_ADDRESS=10.8.0.x
            - WG_DEFAULT_DNS='10.0.0.1, 150.230.183.65, 1.1.1.1'
            - WG_ALLOWED_IPS='0.0.0.0/0, ::/0'
            - WG_PRE_UP=
            - WG_POST_UP='iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE'
            - WG_PRE_DOWN=
            - WG_POST_DOWN='iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE'
        volumes:
            - '/root/.local/share/srv/docker/wireguard/volumes/config/wireguard:/etc/wireguard'
            - '/root/.local/share/srv/docker/wireguard/volumes/data:/data:z'
            - '/root/.local/share/srv/docker/wireguard/volumes/config:/config:z'
            - '/lib/modules:/lib/modules'
        ports:
            - '0.0.0.0:51820:51820/udp'
            - '127.0.0.10:50453:51821'
        image: 'casjaysdevdocker/wireguard:latest'
```

## Author  

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🤖 casjaysdevdocker: [Github](https://github.com/casjaysdevdocker) [Docker](https://hub.docker.com/r/casjaysdevdocker) 🤖  
