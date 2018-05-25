<!-- markdownlint-disable MD041 -->
> I would greatly appreciate it if you kindly give me some feedback if you found an error
> [Send feedback to me](mailto:feedback@mathias-stadler.de)
<!-- markdownlint-enable MD041 -->

# orangepi-H3-spi

used OLED 96x64 on orangepi H3 with Armbian

## only for my thought


## environment

- [orange pi one](http://www.orangepi.org/orangepione/)
- [Armbian OS Lagency kernel 3.4.y](https://www.armbian.com/orange-pi-one/)
- Stadard powersuply from orange pi
- [Oled display SSD1306](0.95 Inch SPI Full Color OLED Display DIY Module 96x64 LCD For Arduino SSD1306 Driver IC Top Quality)



## kernel 
```bash
> uanme -a
Linux orangepione 3.4.113-sun8i #6 SMP PREEMPT Sun Sep 17 20:56:29 UTC 2017 armv7l armv7l armv7l GNU/Linux
```

- i'm hold all kernel update via set hold kernel update via sudo armbian-config

## install spi driver

```bash

-- download boot-sunxi.cmd script

>wget https://raw.githubusercontent.com/igorpecovnik/lib/master/config/bootscripts/boot-sunxi.cmd -O /boot/boot.cmd
```

-- make new boot.scr image

```bash
> mkimage -C none -A arm -T script -d /boot/boot.cmd /boot/boot.scr
```

- add overlays and parameter to /boot/armbianEnv.txt

```bash
overlays=spi-spidev
param_spidev_spi_bus=0
param_spidev_max_freq=100000000
```

-- and REBOOT the sbc

## check spi driver installation


- **after reboot this device**
- you should see a spi devive under /dev

```bash
> ls -l /dev/spi*
crw------- 1 root root 153, 0 May 18 10:48 /dev/spidev0.0
```

## enable I2C on your Pi 


## wiring up the display

- header layout 
[header layout h3](http://linux-sunxi.org/Orange_Pi_One#Orientation_of_the_GPIO_header)


- [wiring raspi](https://learn.adafruit.com/ssd1306-oled-displays-with-raspberry-pi-and-beaglebone-black?view=all)



Definition of SPI Connector Display side:
1.GND-Gound
2.VCC-Positive Voltage
3.SCL-Clock Line
4.SDA-Data Line
5.RES-Reset
6.DC-Data/Demand
7.CS-Chip Select

P01 : 3.3V  <--> 2
P25 : GND   <--> 1
P15 : CE    <--> 7 CS
P19 : MOSI  <--> 4 SDA-Data
P21 : MISO
P23 : SCLK <--> 3 SCL-Clock Line
P24 : CSN 



## install software

```bash
sudo apt-get install python-dev
git clone https://github.com/lthiery/SPI-Py

sudo apt-get install build-essential python-dev python-pip


```

## sources

[install spi instruction from willmore](https://forum.armbian.com/topic/3772-how-to-enable-hardware-spi/)


http://www.orangepi.org/orangepibbsen/forum.php?mod=viewthread&tid=202

## Errors

[Board index Programming Python Python.h not found. error command 'arm-linux-gnueabihf-gcc' failed with exit status 1](https://www.raspberrypi.org/forums/viewtopic.php?t=202028)

- **if** you install gcc ?? Check with

```bash
> arm-linux-gnueabihf-gcc --version
```

[Python.h: No such file or directory](https://stackoverflow.com/questions/21530577/fatal-error-python-h-no-such-file-or-directory)

- **important** Have you a clean install
- check with

```bash
> sudo apt-get update
> sudo apt-get upgrade
```

- should run without errors



## eth0:avahi

```txt
Avahi is a daemon (a service) which is responsible for several things, including attributing you an IP address when DHCP (automatic IP address from a DHCP server on the network) fails. The fact that eth0:avahi appears means that the system failed to get an IP on the eth0 interface (your wired network interface).
```

[from here 2nd article](https://askubuntu.com/questions/3159/delete-eth0-avahi-from-the-ifconfig-list)

### troubleshooting no dhcp ip address

- fix your /etc/network/interfaces e.g. to

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

- and restart your network services

```bash
> sudo /etc/init.d/networking restart
```

## connect serial console

```bash
> picocom -b 115200 /dev/ttyUSB0
```


## dhcp dump

- on each client in the network

```bash
> sudo tcpdump -lenx -i enp0s25 -s 1500 port bootps or port bootpc
```


## rest
https://www.youtube.com/watch?v=XNPoO3JLppA

