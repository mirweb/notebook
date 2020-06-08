# Raspi as homeserver

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

- create simple [inentory](inventroy)
- put setup tasks into [raspi.yml]
- run setup via

```bash
ansible-playbook -i inventory raspi.yml
````

### Infos for using wireguard

- [Private IPv6 address range](https://simpledns.plus/private-ipv6)