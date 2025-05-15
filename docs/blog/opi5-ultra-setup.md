---
title: Orange PI 5 Ultra setup
tags: ["debian", "sbc", "pi"]
---

## Setup instruction
- Download the debian image from orange PI official website for debian installation
- Untar the image and flash it on sd card using balena itcher
- attach the ssd to the pi from backside
- attach hdmi cable and keyboard for first time use
- attach flashed sd card and start turn on
- connect to the internet using `nmtui` or `nmcli device wifi connect "ssid" password "password"`
- `sudo vim /usr/bin/orangepi-config` and replace `baidu` with `google` for internet check
- set timezone using `sudo timedatectl set-timezone Asia/Kolkata`
- now do system upgrade using `sudo apt update && sudo apt -y upgrade`
- prepare the disk using
    - `sudo fdisk -l` will show you all devices
    - `sudo fdisk -l /dev/mtdblock0` press `d` and delete all the partitions --> then press `w` to write the changes
    - `sudo fdisk -l /dev/nvme0n1` press `d` and delete all the partitions --> then press `w` to write the changes
    - `scp .\image_name.img root@192.168.200.164:/home/orangepi` this will copy the image in sd card
- tell orangepi to use 16MB spi flash storage for u-boot `sudo orangepi-config`.
    - choose `system` -> `install` -> `Install/Update the bootloader on SPI Flash`
- finally finish of with this command --> `sudo dd bs=1M if=image_name.img of=/dev/nvme0n1 status=progress` and `sudo sync`
- turnoff using `sudo poweroff` and remove the sd card

## Seting up ssd
- connect to the internet using `nmtui` or `nmcli device wifi connect "ssid" password "password"`
- `sudo vim /usr/bin/orangepi-config` and replace `baidu` with `google` for internet check
- set timezone using `sudo timedatectl set-timezone Asia/Kolkata`
- now do system upgrade using `sudo apt update && sudo apt -y upgrade`
- `sudo auto_login_cli.sh root` automatically login as root
- `sudo auto_login_cli.sh -d` to disable autologin
- `sudo reboot` to restart the pi and select root user
- `usermod -l myname orangepi` rename the existing orangepi user to username you provided
- `usermod -m -d /home/myname myname` rename the homedir
- `groupmod -n myname orangepi` rename the group to be what your user is
- `passwd myname` changes the current user password to created replace myname with user name
- `passwd` changes the root user password
- reboot and login as user you created
- `chsh -s /usr/bin/zsh` and `sudo chsh -s /usr/bin/zsh`
- done it's ready to use now
