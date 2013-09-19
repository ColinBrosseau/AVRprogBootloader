# Description

Bootloader for ATMEL ATmega Controllers. It allows, once installed in the microcontroler (uC), to reprogram itself without the need of an external programmer.

This is based on http://gandalf.arubi.uni-kl.de/avr_projects/#avrprog_boot (version 0.85)

#Instructions

See readme.txt for full instructions.

## Set configuration

As is, these files suppose that

**the microcontroler board has these settings**

main.c

* uC model: ATmega16
* Frequency of the uC: 12 MHz
* Serial port Baudrate: 57600

**and that the external programmer had these settings**

makefile

* Type: stk500v1
* Port name: /dev/ttyUSB0
* Port speed: 19200 

If it's not the case. Edit corresponding lines in these files.

## Compile

       make

## To program the uC with the external programmer

Plug the external programmer to the uC so we have something like:  

       PC -> External Programmer -> uC

## Upload to uC

	make program

## Set fuse bits

Something like  
	
	avrdude -p MCU -c PROG_NAME -v -b PROG_SPEED -F -P PROG_PORT -U lfuse:w:LOW:m -U hfuse:w:HIGH:m

## To program the uC directly

Connect uC's UART pins to PC

       PC -> uC       

* Reset the AVR while fullfilling the bootloader start-condition.
* Start AVRDUDE (to upload the hex file to the uC)  
  Where the hex file is the program we want the uC to execute.
