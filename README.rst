============
User Guide
============

.. contents:: :local:


Authors
==========

`codeshredder <https://github.com/codeshredder>`_ 


Reference
==========


http://linux-sunxi.org/

https://github.com/cubieboard2/

https://github.com/linux-sunxi

http://source.android.com/source/initializing.html


About Cubieboard
==========


http://cubieboard.org/

http://cubiebook.org

Tools
==========

TTL cable
----------

1) cable	Pin on Cubieboard

PIN1 (WHITE)   -> TX

PIN2 (GREEN)   -> RX

GROUND (BLACK) -> GND

WARNING: DO NOT CONNECT THE RED LINE TO VCC.

2) install driver

pl2303 cable may have problem on win8 x86/64.(because of win8 driver auto update)
 
step1:close win8 driver auto update
 
into win8 control panel：search｜device ｜

find "device printer" -> "change update"
 
set "no"and “never install from ...”

 
step2:install driver
 
download "PL2303_Prolific_DriverInstaller_v1.5.0.exe" and install


console
----------

linux
++++++++++

#apt-get install ckermit

#vi ~/.mykermrc

set line          /dev/ttyUSB0

set speed         115200

set carrier-watch off

set handshake     none

set flow-control  none

robust

set file type     bin

set file name     lit

set rec pack      1000

set send pack     1000

set window        5



#kermit -c



LiveSuit
----------

linux version
++++++++++

* download LiveSuit 

Ubuntu x86: http://ubuntuone.com/2bf1fIHN3oFR5NRyggJqPP

Ubuntu x86-64: http://ubuntuone.com/1Q5Yi3eVAzS2xn3Ex7Ix3n


* install LiveSuit(no root)::

        ./LiveSuit.run
        cd ~/Bin
        sudo dpkg -i awdev-dkms_0.4_all.deb

        sudo vi /etc/udev/rules.d/10-local.rules

        SUBSYSTEM!="usb_device",ACTION!="add",GOTO="objdev_rules_end"
        #USBasp
        ATTRS{idVendor}=="1f3a",ATTRS{idProduct}=="efe8",GROUP="user",MODE="0666"
        LABEL="objdev_rules_end"
        #"user" must be current user

* reboot linux::

        sudo reboot

* use LiveSuit::

        cd ~/bin/LiveSuit
        ./LiveSuit.sh


Linux
==========


get kernel source
----------

* install tool chain(ubuntu 12.04 64bit)::

        git clone https://github.com/cubieboard2/linux-sunxi
        git branch -r
        git checkout -b localbranchname remotebranchname


make image
----------

* install tool chain(ubuntu 12.04 64bit)::

        apt-get install gcc-arm-linux-gnueabi gcc-arm-linux-gnueabihf build-essential
        apt-get install u-boot-tools
        apt-get install linaro-image-tools
        apt-get install libncurses5-dev

* build kernel::

        make distclean ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make cubieboard2_defconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make menuconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make uImage -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make modules -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        cp -rf arch/arm/boot/uImage ../output
        make modules_install INSTALL_MOD_PATH=../output ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-



* make rootfs




* make image


Q&A
----------

* no audio

::

   usermod -a -G audio username 


Android
==========

* prepare java environment (ubuntu 12.04 64bit)::

        #remove old java
        
        apt-get update
        apt-cache search java | awk '{print($1)}' | grep -E -e '^(ia32-)?(sun|oracle)-java' -e '^openjdk-' -e '^icedtea' -e '^(default|gcj)-j(re|dk)' -e '^gcj-(.*)-j(re|dk)' -e 'java-common' | xargs sudo apt-get -y remove
        apt-get -y autoremove
        
        apt-get purge openjdk*
        apt-get autoremove
        
        #check java no exist
        java -version
  

        #install oracle java jdk
        #download jdk1.6.0_45 from http://www.oracle.com/technetwork/java/javase/downloads/index.html
        #umcompress to /usr/local
        
        vi /etc/environment
        
        PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/jdk1.6.0_45/bin"
        JAVA_HOME="/usr/local/jdk1.6.0_45/"
        CLASSPATH=".:/usr/local/jdk1.6.0_45/lib/dt.jar:/usr/local/jdk1.6.0_45/lib/tools.jar"
        
        #check java exist
        java -version

* prepare android environment (ubuntu 12.04 64bit)::

        apt-get install git gnupg flex bison gperf build-essential \
        zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
        libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
        libgl1-mesa-dev g++-multilib mingw32 tofrodos \
        python-markdown libxml2-utils xsltproc zlib1g-dev:i386
        
        ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so


* download sdk::

        http://cubiebook.org/index.php?title=Cubieboard2/Building_your_own_Android_image

* make::

        $cd lichee
        $./build.sh -p sun7i_android
        $cd ../android42
        $source build/envsetup.sh
        $lunch (select sugar-cubieboard2)
        $extract-bsp
        $make -j4


Application
==========

* camera::

        http://forum.ubuntu.org.cn/viewtopic.php?f=74&t=400632
        http://javacxn.blog.163.com/blog/static/1832776420123685922407


Licensing
============

This project is licensed under Creative Commons License.

To view a copy of this license, visit [ http://creativecommons.org/licenses/ ].

Contacts
===========

codeshredder  : evilforce@gmail.com
