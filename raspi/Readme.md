# Raspi as homeserver

## About

- simple raspi setup with some common services and almost automatic setup via ansible
- currently serving 
  - [wireguard](#wireguard) vpn endpoint into home network

## Hardware infos

- raspi 4b with 4GB ram and 64GB Class10 MicroSD

## Installing ubuntu 20.04 LTS on raspi

- download image for correct device over [download page](https://ubuntu.com/download/raspberry-pi)
- follow [install istruction](https://ubuntu.com/download/raspberry-pi/thank-you?version=20.04&architecture=arm64+raspi), eg for [mac](https://ubuntu.com/tutorials/create-an-ubuntu-image-for-a-raspberry-pi-on-macos#1-overview)

```bash
# list your devices
diskutil list
# umount your removable sd card (check if you have also /dev/disk2!!)
diskutil unmountDisk /dev/disk2
# use previously downloaded image
sudo sh -c 'gunzip -c ~/Downloads/ubuntu-20.04-preinstalled-server-arm64+raspi.img.xz | sudo dd of=/dev/disk2 bs=32m'
```

- put sd card into raspi, connect to wireless ethernet and power on

## First Startup

- find ip from raspi in your router or use ubuntu as hostname to ssh for first connection 
- basic setup

```bash
# rename host name
sudo hostnamectl set-hostname raspi
```

## Setup via basic ansible playbook

- create simple [hosts.yml](hosts.yml) from example under [hosts.example.yml](hosts.example.yml) with adjusting vars to your needs
- defined setup tasks into [raspi.yml](raspi.yml)
- run setup via

```bash
ansible-playbook raspi.yml
```

- currently installed roles
  - [wireguard](#Wireguard)
  - [traefik](#Traefik)
  - [pihole](#Pihole)

## Wireguard

### Infos & Tutorials for using wireguard

- [Private IPv6 address range](https://simpledns.plus/private-ipv6)
- [WireGuard VPN Server einrichten (Ubuntu, Raspberry Pi, Linux, Android)](https://www.bitblokes.de/wireguard-vpn-server-einrichten-ubuntu-raspberry-pi-linux-android/)
- [Wireguard VPN und Ubuntu 20.04](https://www.sebastian-fritz.net/2019/01/28/wireguard-vpn-und-ubuntu-18-04/)

### setup wiregurad peers on raspi

- after playbook run basic wireguard setup is activ
- listening on default udp port 51820
- to add peer config, eg. mobile device, make following steps

```bash
# create dir for every peer
ubuntu@raspi:~/wg_users$ mkdir peer && cd peer
# generate kees for peer
ubuntu@raspi:~/wg_users/peer$ umask 077
ubuntu@raspi:~/wg_users/peer$ wg genkey | tee privatekey | wg pubkey | tee pubkey
ubuntu@raspi:~/wg_users/peer$ wg genpsk > preshared_peer
# copy sample client.conf and edit this (fill in keys, adjust server, eg dns)
ubuntu@raspi:~/wg_users/peer$ cp ../client.conf.sample client.conf
ubuntu@raspi:~/wg_users/peer$ vi client.conf
# display config as qrcode to scan from mobile
ubuntu@raspi:~/wg_users/peer$ qrencode -t ansiutf8  < client.conf
# add to wg config
ubuntu@raspi:~/wg_users/peer$ cat pubkey 
ubuntu@raspi:~/wg_users/peer$ sudo wg set wg0 peer `cat pubkey` preshared-key ./preshared_peer allowed-ips 192.168.222.2/32,fd1a:3dd3:851e:3645::2/64
ubuntu@raspi:~/wg_users/peer$ sudo wg-quick save wg0
```

## Traefik

- [traefik](https://docs.traefik.io) router as docker-compose setup installed

## Pi-Hole

- [Pi-hole](https://pi-hole.net) basic setup
- use pi_hole inventory variable, to define host how pi-hole should be reachable over traefik