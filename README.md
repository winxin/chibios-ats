# ATS programing on [ChibiOS/RT](http://www.chibios.org) [![Build Status](https://travis-ci.org/fpiot/chibios-ats.svg)](https://travis-ci.org/fpiot/chibios-ats)

## Hardwares

[![](img/ArduinoMega2560_R3.jpg)](http://arduino.cc/en/Main/ArduinoBoardMega2560)

* CPU: ATmega2560 ([Atmel AVR](http://www.atmel.com/products/microcontrollers/avr/) 8-bit)
* Flash ROM: 256 KiB
* SRAM: 8 KiB

Also you could get [compatible boards](http://www.sainsmart.com/sainsmart-mega2560-r3-development-board-compatible-with-arduino-mega2560-r3.html).


## Setup environment

### [Debian GNU/Linux](https://www.debian.org/)

Install some packages.

```
$ sudo apt-get install binutils-avr gcc-avr avr-libc avrdude libgmp-dev
```

### Mac OS X

Install gmp package.

```
$ brew install gmp
```

Install avr toolchain http://www.obdev.at/products/crosspack/index.html, and set PATH env.

```
$ export PATH=$PATH:/usr/local/CrossPack-AVR/bin
$ which avr-gcc
/usr/local/CrossPack-AVR/bin/avr-gcc
```

### Windows

T.B.D.


## How to build

Install ATS2 http://www.ats-lang.org/.

```
$ wget http://downloads.sourceforge.net/project/ats2-lang/ats2-lang/ats2-postiats-0.0.8/ATS2-Postiats-0.0.8.tgz
$ tar xf ATS2-Postiats-0.0.8.tgz
$ cd ATS2-Postiats-0.0.8
$ ./configure
$ make
$ sudo make install
$ export PATSHOME=/usr/local/lib/ats2-postiats-0.0.8
```

Compile the ATS source code for Arduino.

```
$ cd chibios-ats/demos/AVR-ArduinoMega2560-GCC-ats
$ make
$ file ch.elf ch.hex
ch.elf: ELF 32-bit LSB executable, Atmel AVR 8-bit, version 1 (SYSV), statically linked, not stripped
ch.hex: ASCII text, with CRLF line terminators
```

## Write to the flash

Connect Arduino board to your PC using USB cable.
And run following commands.

```
$ ls -l /dev/ttyACM0
crw-rw---- 1 root dialout 166, 0 May  8 15:59 /dev/ttyACM0
$ cd arduino-mega2560-ats/blink_ats
$ make program
avrdude -p atmega2560 -P /dev/ttyACM0     -c stk500v2    -b 115200 -U flash:w:ch.hex 
avrdude: AVR device initialized and ready to accept instructions
Reading | ################################################## | 100% 0.02s
--snip--
avrdude: verifying ...
avrdude: 28650 bytes of flash verified
avrdude: safemode: Fuses OK (E:00, H:00, L:00)
avrdude done.  Thank you.
```


## Watch serial console

Use screen command.

```
$ ls -l /dev/ttyACM0
crw-rw---- 1 root dialout 166, 0 May  8 15:59 /dev/ttyACM0
$ screen /dev/ttyACM0 9600
*** ChibiOS/RT test suite
***
*** Kernel:       2.6.4
*** Compiled:     May  9 2014 - 22:35:52
*** Compiler:     GCC 4.8.2
*** Architecture: AVR
*** Core Variant: MegaAVR
*** Port Info:    None
*** Platform:     ATmega
*** Test Board:   Arduino

----------------------------------------------------------------------------
--- Test Case 1.1 (Threads, enqueuing test #1)
--- Result: SUCCESS
```


## How to debug using gdb

[![](/img/avr_dragon.jpg)](http://www.atmel.com/tools/avrdragon.aspx)

T.B.D.
