# Table of Contents

* [What is OpEdRo](#opedro-an-open-educational-rpi-robot)
* [Main Components](#main-components)
* [Circuit Diagram](#circuit-diagram)
* [(Raspberry Pi) Software Prerequisites](#raspberry-pi-software-prerequisites)
  * [Step 1: Installing and Setting up Raspberry Pi's Operating System](#step-1-installing-and-setting-up-raspberry-pis-operating-system)
  * [Step 2: Installing Necessary Python Libraries](#step-2-installing-necessary-python-libraries)
* [Remote Access Rapsberry Pi's Command Line Interface (CLI)](#remote-access-rapsberry-pis-command-line-interface-cli)
* [The Control Computer](#the-control-computer-----)
* [Scratch Project](#scratch-project-----)
* [Licenses](#licenses)

---

# [OpEdRo] An-Open-Educational-(RPi)-Robot

An Educational Robotic Platform, Raspberry Pi based, using Open Technologies. Remotely programmable from Scratch to move specific distances, to turn specific angles, to get distance from obstacle, to get environment temperature, to speak text and contents of variables in more than 30 languages.


---

*`This project is in active development. Additions will be taking place on a regular basis`*

---

## `OpEdRo:-----`
  ![Circuit diagram](/docs/images/OpEdRo_1.png) ![Circuit diagram](/docs/images/OpEdRo_2.png) ![Circuit diagram](/docs/images/OpEdRo_3.png) ![Circuit diagram](/docs/images/OpEdRo_4.png)
### Main Components:

![chassis](/docs/images/Robot_chassis96.png) ![Raspberry Pi 3](/docs/images/Raspberry-Pi-3.png) ![servo motor](/docs/images/Servo_motor96.png) ![photoelectric](/docs/images/Photoelectric_sensor96.png) ![Encoder disk](/docs/images/Encoder_disk96.png) ![servo wheel](/docs/images/Servo_wheel96.png) ![digital thermometer](/docs/images/DS18B20.png) ![ultrasonic sensor](/docs/images/HC-SR04.png) ![ball caster](/docs/images/Ball_caster96.png) ![Battery holder](/docs/images/Battery_holder96.png)

  * A robot chassis appropriate to host the following parts
  * A Rapsberry Pi 3 model B
  * 2 continuous rotation micro servo motors, fitable to robot chassis
  * 2 photoelectric sensors
  * 2 encoder disks
  * 2 servo mount wheels
  * 1 digital thermometer (DS18B20)
  * 1 ultrasonic distance sensor (HC-SR04)
  * 1 ball caster
  * 1 battery holder for 4xAA to power the servos
  * 1 power bank for Raspberry Pi
  * 1 small portable speaker with 3.5 mm jack (for the speech engine)
  
### Circuit Diagram
  ![Circuit diagram](/docs/images/Circuit_Snapshot_1.png)
  
### (Raspberry Pi) Software Prerequisites: 

  * Operating system
    * Raspbian Jessie or Stretch Lite (Lite version uses lower computer resources)
  * Python 2.7.x (inclluded with OS)
  * Python packages / modules:
    * [RPi.GPIO](https://sourceforge.net/p/raspberry-gpio-python/wiki/Home/ "RPi.GPIO Wiki") (a class to control the GPIO on a Raspberry Pi, included with OS)
    * [pigpio](http://abyz.me.uk/rpi/pigpio/index.html "The pigpio Documentation") (a library supporting hardware timed servo pulses)
    * [scratchpy](https://github.com/pilliq/scratchpy "Python interface to Scratch") (a python client for Scratch)
    * [espeak](http://espeak.sourceforge.net/ "espeak Documentation") (a text to speech engine)
    * [w1thermsensor](https://github.com/timofurrer/w1thermsensor "Python package for the DS18B20 sensor") (a library for the DS18B20 temperature sensor)
  
---
### Step 1: Installing and Setting up Raspberry Pi's Operating System
---
  1. > Download [Raspbian Stretch Lite](https://www.raspberrypi.org/downloads/raspbian/) image file
  2. > Unzip the compressed file
  3. > Use the [Etcher](https://etcher.io/) SD card utility (or a similar one) to transfer the Raspbian to the SD card
  4. > Connect Raspberry Pi to an internet network using an Ethernet cable and boot
  5. > Log in as *pi* user
  6. > Invoke the configuration utility *raspi-config*, by typing at the command line interface:
     > ```
     > sudo raspi-config
     > ```
  7. > Enable remote command line access using ssh, in order to allow remote access to the robot:
  
     > 7a. Select *Interfacing Options:*
     > ![Step 7a](/docs/images/2.png)
     
     > 7b. Select *SSH:*
     > ![Step 7b](/docs/images/3.png)

  8. > Set WiFi SSID and pass phrase of the network where robot will be connected:
  
     > 8a. Select *Network Options:*
     > ![Step 8a](/docs/images/4.png)
     
     > 8b. Select *Wi-fi:*
     > ![Step 8b](/docs/images/6.png)
  9. > Check the wlan (wireless lan) IP assigned.
     
     > Exit raspi-config and type:
     > ```
     > ifconfig
     > ```
     > At the *wlan0:* part of the command output, the new IP should appear:
     >
     > ![Step 9](/docs/images/7.png)
  10. > Set a Static IP for the Raspberry Pi [Optional]
  
      > You will need:
      > - a valid static IP address (at the example below, *192.168.2.200*)
      > - the router's and domain_name_servers' IP addresses (usually same IP for both, at the example below *192.168.2.1*)
      >
      
      > At the command line type:
      > ```
      > sudo nano /etc/dhcpcd.conf
      > ```
      > Go to the end of the file and type (adjust accordingly to your IPs):
      > ```
      > interface wlan0
      > static ip_address=192.168.2.200/24
      > static routers=192.168.2.1
      > static domain_name_servers=192.168.2.1
      > ```
      > Save changes, exit nano and reboot by typing:
      >
      > <p><kbd>Ctrl</kbd> + <kbd>O</kbd>  to confirm write to the file</p>
      > <p><kbd>Ctrl</kbd> + <kbd>X</kbd>  to exit the nano editor</p>
      >
      > `sudo reboot` for changes to take effect 
      
---
### Step 2: Installing Necessary Python Libraries
---
  1. > Update and upgrade installed packages:
  
     > ```
     > sudo apt-get update
     > sudo apt-get upgrade
     > ```
  2. > Install scratchpy:
  
     > Firstly obtain the python package manager, *pip*
     > ```
     > sudo apt-get install python-pip
     > ```
     
     > Then continue with the scratchpy:
     > ```
     > pip install scratchpy
     > ```
  3. > Install the pigpio library:
  
     > ```
     > wget abyz.co.uk/rpi/pigpio/pigpio.zip
     > unzip pigpio.zip
     > cd PIGPIO
     > make
     > sudo make install
     > ```
  4. > Install the espeak package:
  
     > ```
     > sudo apt-get install python-espeak
     > ```
  5. > Setting the DS18B20 thermometer:
     
     > 5a. Install the w1thermsensor package:
     > ```
     > sudo apt-get install python-w1thermsensor
     > ```
     
     > 5b. Allow hardware initialisation for the sensor.
           At the command line type:
      
     > ```
     > sudo nano /boot/config.txt
     > ```
     > Go to the end of the file and type:
     > ```
     > dtoverlay=w1-gpio
     > ```
     > Save changes, exit nano and reboot by typing:
     >
     > <p><kbd>Ctrl</kbd> + <kbd>O</kbd>  to confirm write to the file</p>
     > <p><kbd>Ctrl</kbd> + <kbd>X</kbd>  to exit the nano editor</p>
     >
     > `sudo reboot` for changes to take effect
  
---
### Remote Access Rapsberry Pi's Command Line Interface (CLI)
---
Knowing the IP address of the Raspberry Pi, from Step 1 [9. & 10.] above (assume that is ~192.168.2.200~ for demonstration purposes), one could connect to its CLI from another computer of the same network
  * If you are on a Windows environment, you will firstly need to install an *ssh terminal client* program (e.g. [PuTTY](https://www.putty.org/)) and configure it to connect to ~192.168.2.200~
  * If you are on a Unix environment, open a terminal window and type:
  
    `ssh pi@192.168.2.200`

## `The Control Computer:-----`
Any computer capable to run Scratch 1.4 (the version supporting the [Mesh](https://en.scratch-wiki.info/wiki/Mesh) method), connected to the same LAN as Raspberry Pi, could become the robot control center:

  1. > [Download Scratch 1.4](https://scratch.mit.edu/scratch_1.4/)
  2. > After opening the application, follow the [instructions](https://en.scratch-wiki.info/wiki/Mesh#Mesh_by_Modification_of_Scratch) for modifying Scratch to enable **Mesh.** You may require administrator privileges
       
        or
     
     > if you are on Windows environment, replace your *scratch.image* file in the **scratch** directory (Program files folder), with the one having Mesh enabled [Windows only](/docs/scratch.image)
  3. > If **Mesh** is not activated, *Host Mesh* by pressing and mouse clicking: <p><kbd>Shift</kbd> + <kbd>Share</kbd> from Scratch menu
  
     > ![enabling Mesh](/docs/images/mesh.png)
  
## `Scratch Project:-----`
**Examples**: -
Press on one of the images below to download the whole Scratch project
(there will be an english version soon..)

The four images correspond to the four sprites of the file *OpEdRo_Examples.sb*

[![scratch examples](/docs/images/robot_settings_1.png)](/docs/OpEdRo_Examples.sb)
[![scratch examples](/docs/images/course.png)](/docs/OpEdRo_Examples.sb)
[![scratch examples](/docs/images/keyboard_control.png)](/docs/OpEdRo_Examples.sb)
[![scratch examples](/docs/images/temperature_obstacle.png)](/docs/OpEdRo_Examples.sb)

## Licenses
Software License:

[![License](/docs/images/gplv3-127x51.png)](https://www.gnu.org/licenses/gpl-3.0.txt)

Non Software material License:

[![non Software License](https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-sa.png)](https://creativecommons.org/licenses/by-sa/4.0/)
