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
