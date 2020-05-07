# Raspberry Jottings
Notes how to compile on raspbian

## micropython
	tar xvf ~/Downloads/micropython-1.12.tar.xz
	cd micropython-1.12/
	cd mpy-cross/
	make
	cd ../ports/unix/
	make
	
## ScanTailor
	sudo apt-get update
	sudo apt-get install build-essential git cmake libqt4-dev libboost-all-dev libjpeg-dev libtiff-dev libxrender-dev zlib1g-dev libpng12-dev 
	git clone https://github.com/scantailor/scantailor.git
	cd scantailor/
	cmake -DCMAKE_INSTALL_PREFIX=/usr .
	make
	sudo make install

## openocd
	sudo apt-get install git autoconf libtool make pkg-config libusb-1.0-0 libusb-1.0-0-dev  libhidapi-dev libftdi1-dev libjaylink-dev libusb-dev
	git clone http://openocd.zylin.com/openocd
	cd openocd
	./bootstrap
	./configure --enable-sysfsgpio --enable-bcm2835gpio
	make
	make install
	
# orbunculum

```
git clone https://github.com/orbcode/orbuculum
cd orbuculum
apt-get install libelf-dev libiberty-dev  binutils-dev
make 
```	
# bmtrace

(from Black Magic Probe Book)

```
apt-get install libbsd-dev libglfw3-dev libusb-1.0.0-dev libgtk-3-dev git
git clone https://github.com/compuphase/Black-Magic-Probe-Book
cd Black-Magic-Probe-Book/source
patch -p0 <<EOD
--- bmscan.c.ORIG	2020-05-07 08:35:45.817172986 +0100
+++ bmscan.c	2020-05-07 08:36:00.636893982 +0100
@@ -27,6 +27,7 @@
 #include <stdlib.h>
 #include <string.h>
 #include "bmp-scan.h"
+#define stricmp(s1,s2)    strcasecmp((s1),(s2))
 
 
 #if !defined sizearray
EOD

GLFW_LIBNAME=glfw make -f Makefile.linux
```