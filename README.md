# Overview
In this repo I'm publishing a the results of a project we did a couple of years ago. We tried to read text over haptic feedback on the torso. We created a portable motor driver that is able to drive 32 vibration motors and can be connected to a smartphone or computer via bluetooth and serial console. We're not providing a detailed howto for building such a device. In fact it is quite easy to build one, it just requires a couple of hours of soldering. The images in the img folder provide some insight into the hardware.

# Results
Initially we intended to use each motor for another character in the alphabet. This failed because we were not able to haptically differentiate between the motors. We then used different combinations of motors to encode characters. After several training sessions (maybe 8 sessions with 20 minutes each) we were able to achieve speeds of up to 2 characters per second with an error rate of roughly 5%. As this was much lower than we had hoped for, we stopped the project.

# Parts
* 1x ATMEGA16-16PU
* 4x ULN2803L
* 1x HC-06 Bluetooth Serial adapter
* 1x 5V low-dropout
* 1x 3.3V low-dropout
* Smaller parts are not listed here


# Participants
* Felix Heilmeyer https://github.com/heilerich
* Armin Feistenauer https://github.com/afeistenauer
* Sven Seeberg https://github.com/sven15

# Software
The program for the ATMEGA stores the key combinations in the EEPROM and provides a simple terminal functionality. The following commands were used to flash the ATMEGA.

## Compiling

    avr-gcc -mmcu=atmega16 -Os main.c -o main.o
    avr-objcopy -j .text -j .data -O ihex  main.o  main.hex
    avrdude -C /etc/avrdude.conf -p m16 -c stk500v2 -P /dev/ttyACM3 -e -vv -U flash:w:main.hex

## Std Fuses

    avrdude -C /etc/avrdude.conf -p m16 -c stk500v2 -P /dev/ttyACM3 -e -vv -U lfuse:w:0xE1:m -U hfuse:w:0x99:m 

## 16 Mhz Fuses

    avrdude -C /etc/avrdude.conf -p m16 -c stk500v2 -P /dev/ttyACM3 -e -vv -U lfuse:w:0xFF:m -U hfuse:w:0x99:m 


## Training software
For training we used a modified version of the miniterm.py from https://github.com/pyserial/pyserial. Thanks to all contributors of that project.
