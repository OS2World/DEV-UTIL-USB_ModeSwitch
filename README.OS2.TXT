usb_modeswitch.exe for OS/2
===========================

This version of usb_modeswitch has been compiled using gcc 3.3.5.  I
have compiled it using
	usb_modeswitch 1.0.2 from http://www.draisberghof.de/usb_modeswitch 
	libusb-0.1.10a-os2.zip from hobbes.nmsu.edu
	usbcalls-20090823.zip from http://ecomstation.ru/projects/developer/downloads/usbcalls-20090823.zip

NOTE: usb.h is from libusb-0.1.10a-os2.zip and *not* from usbcalls-20090823.zip

For convenience I have copied the pre-compiled libraries and headers
into this distribution.

INSTALLATION
============
Copy boot/usbresmg.sys to e:/ecs/boot 

!!!!!!Don't forget to make a backup of the original !!!!!!!
									  
Make sure that the usbresmg.sys is in config.sys as
	DEVICE=E:\ECS\BOOT\USBRESMG.SYS										  
REM out any older line in config.sys

Copy dll/usbcalls.dll to a dll directory which is in your LIBPATH.
(Make sure that there isn't an older copy)

Copy usb_modeswitch.conf to /etc directory.  I had to make an etc
directory because usb_modeswitch.exe doesn't seem to use the ETC
variable set in config.sys

Edit usb_modeswitch.conf for your device.  I have an Cricket A600
and so I uncommented 

########################################################
# Cricket A600
#
# Switches to ACM device.  Might need a ResetUSB after switching - or not
#
# Contributor: Jeffrey Hoogland

DefaultVendor=  0x1f28
DefaultProduct= 0x0021

TargetVendor=   0x1f28
TargetProduct=  0x0020

# only for reference
MessageEndpoint=0x08

MessageContent="555342431234567824000000800108df200000000000000000000000000000"

# Afterwards (optional): "usb_modeswitch -v 0x1f28 -p 0x0020 -R"

########################################################

Running
=======

Running usb_modeswitch with my Cricket A600 USB modem gives me

********************************
Looking for target devices ...
 No devices in target mode or class found
Looking for default devices ...
 Found default devices (1)
Accessing device 001 on bus 000 ...
Using endpoints 0x08 (out) and 0x87 (in)
Inquiring device details; driver will be detached ...
 Cant't do driver detection and detaching on this platform.
 Could not send INQUIRY message (error -22)

Device description data (identification)
-------------------------
Manufacturer: Cal-comp E&CC Limited
     Product: USB Micro SD Storage
  Serial No.: 215973138300
-------------------------
 Cant't do driver detection and detaching on this platform.
Setting up communication with interface 0 ...
Trying to send the message to endpoint 0x08 ...
 OK, message successfully sent
Device is gone, skipping further steps ...
-> Run lsusb to note any changes. Bye.
*********************************

Compiling
=========

Make sure you have gcc 3.3.5 installed.
Then the following command with make usb_modeswitch.exe

make -f Makefile.os2

--------------------------------------------------

Cheng-Yang Tan
cytan299@yahoo.com
25 Aug 2009


