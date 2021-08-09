# Raspberry Jottings
Notes how to compile and install on raspberry pi
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
	
## orbunculum

```
git clone https://github.com/orbcode/orbuculum
cd orbuculum
apt-get install libelf-dev libiberty-dev  binutils-dev
make 
```	

## bmtrace

(from Black Magic Probe Book)

```
apt-get install libbsd-dev libglfw3-dev libusb-1.0.0-dev libgtk-3-dev git
git clone https://github.com/compuphase/Black-Magic-Probe-Book
cd Black-Magic-Probe-Book/source
GLFW_LIBNAME=glfw make -f Makefile.linux
```

## STM32CubeMX

Download and install [Oracle java 1.8.0, arm32 hard float](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)
```
 cd /opt; tar xvf jdk-8u251-linux-arm32-vfp-hflt.tar.gz
```
Download and unzip [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) for linux:
```
unzip en.stm32cubemx-lin_v6-3-0.zip
```
Start installer
```
/opt/jdk1.8.0_251/bin/java -jar ./SetupSTM32CubeMX-6.3.0
```
Execute STM32CubeMX from install directory
```
/opt/jdk1.8.0_251/bin/java -jar ./STM32CubeMX
```
The STM32CubeMX starts up, but stops at The linux STM32CubeMX installs its own JRE runtime environment. Unfortunately, the JRE is for x86, not arm. Replace x86 binary with an arm binary, and make sure the arm binary will not be overwritten.
```
$ cd ~/.stm32cubemx/plugins/updater/loadedSoftware/jre/bin
$ file java
java: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.18, not stripped
$ rm java
$ sudo cp /etc/alternatives/java .
$ rm unpack200
$ sudo cp /usr/bin/unpack200 .
```
At this point, STM32CubeMX should work:
```
java -jar ./STM32CubeMX
```


Uninstaller:
```
/opt/jdk1.8.0_251/bin/java -jar STM32CubeMX/Uninstaller/uninstaller.jar
```
