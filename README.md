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

* install tool chain(ubuntu 12.04 64bit)
 


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
