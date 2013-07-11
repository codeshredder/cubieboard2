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


About Cubieboard
----------


http://cubieboard.org/

http://cn.cubieboard.org/



Linux
----------


* Install Tool Chain

        apt-get install gcc-arm-linux-gnueabi gcc-arm-linux-gnueabihf build-essential
        apt-get install u-boot-tools
        apt-get install linaro-image-tools

* Compile Kernel

        make distclean ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make cubieboard2_defconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make menuconfig ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        make uImage -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        make modules -j8 ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-
        
        cp arch/arm/boot/uImage ../output
        make modules_install INSTALL_MOD_PATH=../output ARCH=arm CROSS_COMPILE=arm-linux-gnueabi-


* Make hwpack




* Make image





Android
----------

* Reference

        http://releases.linaro.org/latest/android/galaxynexus



Licensing
----------

This project is licensed under Creative Commons License.

To view a copy of this license, visit [ http://creativecommons.org/licenses/ ].


Contacts
----------

codeshredder  : evilforce@gmail.com
