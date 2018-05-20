# hints for rasberry pi

## dowload image

[download images](https://www.raspberrypi.org/downloads/raspbian/)

## prepare sd card

[prepare overview](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
[prepare for linux](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)

## enable ssh on ssd card remote

[enable ssh with remote computer](https://www.raspberrypi.org/documentation/remote-access/ssh/)


## found ip from headless raspberry if the device is started and connected on your LAN network

```bash
> sudo nmap -sn 192.168.178.32/24 |grep raspberry
Nmap scan report for raspberrypi.fritz.box (192.168.178.38)
```

## connect via ssh to raspberry

```bash
> ssh pi@<IP OF RASPBERRY>
> ssh pi@192.168.178.38
```

- The password is **raspberry** for the default image :-)


## update the software to the newest version

```bash
> sudo apt-get update && sudo apt-get upgrade && sudo apt-get autoremove
# it is recommend you are reboot the device after each software installation
> reboot
```

- this tak a moment longer

## install spi software

- for this sample used we this images

```bash
1862270976 Apr 18 02:08 2018-04-18-raspbian-stretch-lite.img
```

- we will fowling this instruction from adafruit

[install spi](https://learn.adafruit.com/ssd1306-oled-displays-with-raspberry-pi-and-beaglebone-black?view=all)


```bash
> sudo apt-get update
> sudo apt-get install build-essential python-dev python-pip
> sudo pip install RPi.GPIO
> sudo apt-get install python-imaging python-smbus
> sudo apt-get install git
> git clone https://github.com/adafruit/Adafruit_Python_SSD1306.git
> cd Adafruit_Python_SSD1306
> sudo python setup.py install
```

## enable spi driver

- sudo raspi-config
5 Interfacing Options
P4 SPI
enable

- uncomment dtparam=spi=on in the file /boot/config.txt
- reboot the device
- Reboot your Pi and you should see the files /dev/spidev0.0 and /dev/spidev0.1 are now available

```bash
> reboot
> ls -l /dev/spidev*
crw-rw---- 1 root spi 153, 0 May 20 22:23 /dev/spidev0.0
crw-rw---- 1 root spi 153, 1 May 20 22:23 /dev/spidev0.1
```

## ssd1306 demos

[demos](http://ssd1306.readthedocs.io/en/latest/python-usage.html)


## spi doku

[documentation>hardware>raspberrypi > spi](https://www.raspberrypi.org/documentation/hardware/raspberrypi/spi/README.md)


## check if kernel module loaded

> Hint: The module spi-bcm2708 has been replaced with the updated kernel module spi-bcm2835 for raspberry 2b

```bash
> lsmod |grep spi
spi_bcm2835             7456  0
```



## python lib for ssd130
[link](https://pypi.org/project/ssd1306/)