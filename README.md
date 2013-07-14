Software and User Guide
==========================================================


Authors
----------

[codeshredder](https://github.com/codeshredder)


Reference
----------


http://linux-sunxi.org/

https://github.com/cubieboard2/

https://github.com/linux-sunxi

http://source.android.com/source/initializing.html


About Cubieboard
----------


http://cubieboard.org/

http://cn.cubieboard.org/


Tools
----------

* TTL and console




* LiveSuit





Linux
----------


* install tool chain(ubuntu 12.04 64bit)

        apt-get install gcc-arm-linux-gnueabi gcc-arm-linux-gnueabihf build-essential
        apt-get install u-boot-tools
        apt-get install linaro-image-tools

* build kernel

        make distclean ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make cubieboard2_defconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make menuconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make uImage -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make modules -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        cp -rf arch/arm/boot/uImage ../output
        make modules_install INSTALL_MOD_PATH=../output ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-


* build gpu driver

        http://linux-sunxi.org/Mali400
        http://linux-sunxi.org/Binary_drivers


* make hwpack




* make image





Android
----------

* prepare java environment (ubuntu 12.04 64bit)

        #remove old java
        
        apt-get update
        apt-cache search java | awk '{print($1)}' | grep -E -e '^(ia32-)?(sun|oracle)-java' -e '^openjdk-' -e '^icedtea' -e '^(default|gcj)-j(re|dk)' -e '^gcj-(.*)-j(re|dk)' -e 'java-common' | xargs sudo apt-get -y remove
        apt-get -y autoremove
        dpkg -l | grep ^rc | awk '{print($2)}' | xargs sudo apt-get -y purge
        bash -c 'ls -d /home/*/.java' | xargs sudo rm -rf
        rm -rf /usr/lib/jvm/*
        
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

* prepare android environment (ubuntu 12.04 64bit)

        apt-get install git gnupg flex bison gperf build-essential \
        zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
        libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
        libgl1-mesa-dev g++-multilib mingw32 tofrodos \
        python-markdown libxml2-utils xsltproc zlib1g-dev:i386
        
        ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so


* download sdk

        http://cubiebook.org/index.php?title=Cubieboard2/Building_your_own_Android_image

* make

        $cd lichee
        $./build.sh -p sun7i_android
        $cd ../android42
        $source build/envsetup.sh
        $lunch (select sugar-cubieboard2)
        $extract-bsp
        $make -j4



Licensing
----------

This project is licensed under Creative Commons License.

To view a copy of this license, visit [ http://creativecommons.org/licenses/ ].


Contacts
----------

codeshredder  : evilforce@gmail.com
