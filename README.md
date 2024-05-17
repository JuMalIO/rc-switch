# rc-switch
[![Build Status](https://travis-ci.org/Attila-FIN/rc-switch.svg?branch=master)](https://travis-ci.org/Attila-FIN/rc-switch)


Use your Arduino or Raspberry Pi to operate remote radio controlled devices

## Download
Original:
https://github.com/sui77/rc-switch/releases/latest

rc-switch is also listed in the arduino library manager.

Modified to support Nexa and Everflourish
https://github.com/perivar/rc-switch

Modified to support for Cixi Yidong Electronics protocol.
Remote control switches are sold under brands AXXEL, Telco, EVOLOGY, CONECTO, mumbi, Manax etc.
More info about the protocol:
http://ipfone.hu/reverse-engineering-the-433mhz-cixi-yidong-electronics-protocol/

Modified to support for Shi Qiong - 1+32 bit protocol.
(https://www.alibaba.com/product-detail/Germany-type-Remote-Control-Socket-outdoor_60651648731.html)
Remote control switches are sold under brands AXXEL in Finland. The switch receives 1+32 bit message. The 1st bit is a normal "1" bit as start. The following 32 bits consists of the 24 bits data + 8 bits checksum. Currently the checksum calculation formula is unknown, it is not any standard CRC, reverse engineering using tool reveng has been unsuccessful. Of course, replaying the code received from the remote will always work. Also using simple trial and error method can reveal new acceptable codes. You need to find ON message only, the OFF message is simply inverting the 2nd bit in the last two bytes (2nd and 10th in the 32 bit data, counted from the LSB). Example working turn ON messages: 656A1EAE 656A1AAA 656A16A6 656A0EB6 C96A1E46 FF6A1E72  FF6C1E74 FF6E1E76 FF701E60 FF721E62 FF021E1C  0F021E94 01021E9C  01020E8C.
1st and 2nd bytes can get many different values (perhaps remote/group ID), but 3rd byte (A, B, C, D or ALL buttons) seems to work only with value 0x1E, 0x1A 0x16, 0x0E, 0x08, where 0x08 is the turn ON ALL switches, where they were taught with the same remote/group ID.

## Wiki
https://github.com/sui77/rc-switch/wiki

## Info
### Send RC codes

Use your Arduino or Raspberry Pi to operate remote radio controlled devices.
This will most likely work with all popular low cost power outlet sockets. If
yours doesn't work, you might need to adjust the pulse length.

All you need is a Arduino or Raspberry Pi, a 315/433MHz AM transmitter and one
or more devices with one of the supported chipsets:

 - SC5262 / SC5272
 - HX2262 / HX2272
 - PT2262 / PT2272
 - EV1527 / RT1527 / FP1527 / HS1527 
 - Intertechno outlets
 - HT6P20X
 - Everflourish like EMW100T
 - Nexa like LMLT-711

### Receive and decode RC codes

Find out what codes your remote is sending. Use your remote to control your
Arduino.

All you need is an Arduino, a 315/433MHz AM receiver (altough there is no
instruction yet, yes it is possible to hack an existing device) and a remote
hand set.

For the Raspberry Pi, clone the https://github.com/ninjablocks/433Utils project to
compile a sniffer tool and transmission commands.
