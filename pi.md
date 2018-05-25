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


## spi loopback test

- Put a wire between MOSI and MISO. It does not test CE0 and CE1

```bash
wget https://raw.githubusercontent.com/raspberrypi/linux/rpi-3.10.y/Documentation/spi/spidev_test.c
gcc -o spidev_test spidev_test.c
./spidev_test -D /dev/spidev0.0
spi mode: 0
bits per word: 8
max speed: 500000 Hz (500 KHz)

FF FF FF FF FF FF
40 00 00 00 00 95
FF FF FF FF FF FF
FF FF FF FF FF FF
FF FF FF FF FF FF
DE AD BE EF BA AD
F0 0D
```

## check if kernel module loaded

> Hint: The module spi-bcm2708 has been replaced with the updated kernel module spi-bcm2835 for raspberry 2b

```bash
> lsmod |grep spi
spi_bcm2835             7456  0
```



## python lib for ssd130
[link](https://pypi.org/project/ssd1306/)


## Raspberry interactive pin layout

[link](https://pinout.xyz/)

## python luma

[link](https://luma-oled.readthedocs.io/en/latest/hardware.html#pre-requisites)






lsmod | grep spi
   94  sudo usermod -a -G spi,gpio pi
   95  reboot
   96  sudo reboot
   97  sudo apt-get install python-dev python-pip libfreetype6-dev libjpeg-dev build-essential
   98  sudo -H pip install --upgrade luma.oled


## 96 x 64 display python
https://gist.github.com/TheRayTracer/dd12c498e3ecb9b8b47f


SSD1331


## python examples/clock.py --interface spi --width 96 --height 64 --display ssd1331

python examples/demo.py --interface spi --width 96 --height 64 --display ssd1331

colors

python examples/colors.py --interface spi --width 96 --height 64 --display ssd1331

python examples/video.py --interface spi --width 96 --height 64 --display ssd1331

tweet_scroll.py

python examples/tweet_scroll.py --interface spi --width 96 --height 64 --display ssd1331


90  ./spidev_test -D /dev/spidev0.0
   91  cd Adafruit_Python_SSD1306/examples/
   92  sudo python shapes.py 
   93  lsmod | grep spi
   94  sudo usermod -a -G spi,gpio pi
   95  reboot
   96  sudo reboot
   97  sudo apt-get install python-dev python-pip libfreetype6-dev libjpeg-dev build-essential
   98  sudo -H pip install --upgrade luma.oled
   99  history 
  100  sudo apt install libsdl-dev libportmidi-dev libsdl-ttf2.0-dev libsdl-mixer1.2-dev libsdl-image1.2-dev
  101  cd
  102  git clone https://github.com/rm-hull/luma.examples.git
  103  cd luma.examples/
  104  sudo -H pip install -e .
  105  python examples/3d_box.py
  106  python examples/3d_box.py --interface spi
  107  python examples/3d_box.py --interface spi --width 96 --height 64 
  108  python examples/clock.py --interface spi --width 96 --height 64 
  109  python examples/clock.py --interface spi 
  110  ps -ef
  111  ps -ef |grep py
  112* python examples/clock.py 
  113  python examples/clock.py --interface spi --width 96 --height 64 --display ssd1331
  114  python examples/cldemo.py -interface spi --width 96 --height 64 --display ssd1331
  115  python examples/demo.py -interface spi --width 96 --height 64 --display ssd1331
  116  python examples/demo.py  -i spi -d ssd1331 -w 96 -h 64
  117  python examples/demo.py  -i spi -d ssd1331 --weight 94 --height 64
  118  python examples/demo.py  -i spi -d ssd1331 --width 94 --height 64
  119  python examples/clock.py --interface spi --width 96 --height 64 --display ssd1331
  120  python examples/demo.py --interface spi --width 96 --height 64 --display ssd1331
  121  ls examples/
  122  python examples/colors.py --interface spi --width 96 --height 64 --display ssd1331
  123  python examples/copilogo.py --interface spi --width 96 --height 64 --display ssd1331
  124  python examples/video.py --interface spi --width 96 --height 64 --display ssd1331
  125  sudo -H pip install av
  126  python examples/tweet_scroll.py --interface spi --width 96 --height 64 --display ssd1331
  127  history 