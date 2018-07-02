# [OpEdRo] An-Open-Educational-(RPi)-Robot
An Educational Robotic Platform, Raspberry Pi based, using Open Technologies, remote controled from Scratch

***
*`This project is in active development. Additions will be taking place on a regular basis`*
***
###`OpEdRo`
List of main components used:
  * A robot chassis appropriate to host the rest of the parts
  * A Rapsberry Pi 3 model B
  * 2 micro servo motors fitable to robot chassis
  * 2 photoelectric sensors
  * 2 encoder disks
  * 1 battery holder for 4xAA to power the servos
  * 1 power bank for Raspberry Pi
  * 1 small portable speaker with 3.5 mm jack (for the speech engine)
  
  
Raspberry Pi Software used: 

  * Operating system
    * Raspbian Jessie Lite (Lite version uses lower computer resources)
  * Python 2.7.x (normally comes with the OS)
  * Python packages / modules
    * [RPi.GPIO](https://sourceforge.net/p/raspberry-gpio-python/wiki/Home/ "RPi.GPIO Wiki") (a class to control the GPIO on a Raspberry Pi, included with OS)
    * [pigpio](http://abyz.me.uk/rpi/pigpio/index.html "The pigpio Documentation") (a library supporting hardware timed servo pulses)
    * [scratchpy](https://github.com/pilliq/scratchpy) (a python client for Scratch)
    * [espeak](http://espeak.sourceforge.net/ "espeak Documentation") (a text to speech engine)
  
###`The Control computer:`
  * Any computer capable to run Scratch 1.4 (the version supporting the [Mesh](https://en.scratch-wiki.info/wiki/Mesh) method)
  * Connected to the same LAN as Raspberry Pi
