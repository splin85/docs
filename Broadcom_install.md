# broadcom iproc 安装编译

## 安装gcc4.7
* sudo apt-get install gcc-4.7 g++-4.7

## host主机需要安装的部分软件包 
* `sudo apt-get install ncurses-dev`
* `sudo apt-get install bison flex texinfo`


## 编译SDK
    tar -xzvf iProcLDK_3.5.5-RC1.package.tgz
    cd 3.5.5-RC1/
    tar -xvf iProcLDK_src_3.5.5-RC1.tgz
    cd buildroot
    make HOSTCXX=g++-4.7 HOSTCC=gcc-4.7

## 编译错误
* recipe for target 'doc/gcc.info' failed

    [解决方法]<https://git.busybox.net/buildroot/commit/?id=62322acb2ce186d544ab21fe253ccc8561a68a48>

   `Diffstat`  
    `-rw-r--r--	toolchain/gcc/gcc-uclibc-4.x.mk	3`	
    

    1 files changed, 3 insertions, 0 deletions
    diff --git a/toolchain/gcc/gcc-uclibc-4.x.mk b/toolchain/gcc/gcc-uclibc-4.x.mk
    index 1b7f222..9d131d5 100644
    --- a/toolchain/gcc/gcc-uclibc-4.x.mk
    +++ b/toolchain/gcc/gcc-uclibc-4.x.mk
    @@ -254,6 +254,7 @@ $(GCC_BUILD_DIR1)/.configured: $(GCC_DIR)/.patched
        mkdir -p $(GCC_BUILD_DIR1)
        (cd $(GCC_BUILD_DIR1); rm -rf config.cache; \
            $(HOST_CONFIGURE_OPTS) \
    +		MAKEINFO=missing \
            $(GCC_DIR)/configure $(QUIET) \
            --prefix=$(HOST_DIR)/usr \
            --build=$(GNU_HOST_NAME) \
    @@ -324,6 +325,7 @@ $(GCC_BUILD_DIR2)/.configured: $(GCC_DIR)/.patched
        mkdir -p $(GCC_BUILD_DIR2)
        (cd $(GCC_BUILD_DIR2); rm -rf config.cache; \
            $(HOST_CONFIGURE_OPTS) \
    +		MAKEINFO=missing \
            $(GCC_DIR)/configure $(QUIET) \
            --prefix=$(HOST_DIR)/usr \
            --build=$(GNU_HOST_NAME) \
    @@ -404,6 +406,7 @@ $(GCC_BUILD_DIR3)/.configured: $(GCC_SRC_DIR)/.patched $(GCC_STAGING_PREREQ)
        ln -snf ../include/ $(HOST_DIR)/usr/$(GNU_TARGET_NAME)/sys-include
        (cd $(GCC_BUILD_DIR3); rm -rf config.cache; \
            $(HOST_CONFIGURE_OPTS) \
    +		MAKEINFO=missing \
            $(GCC_SRC_DIR)/configure $(QUIET) \
            --prefix=$(HOST_DIR)/usr \
            --build=$(GNU_HOST_NAME) \
            
* Makefile:785: recipe for target '../objects/lib_gen.o' failed

    ```_16608.c:835:2: error: expected ‘)’ before ‘int’  
    Makefile:785: recipe for target '../objects/lib_gen.o' failed  
    make[2]: *** [../objects/lib_gen.o] Error 1
    
    解决方法：
    splin@splin-VirtualBox:~/3.5.5-RC1/iproc/buildroot$ find -name curses.tail  
    ./output/build/host-ncurses-5.9/include/curses.tail  
    ./output/build/ncurses-5.9/include/curses.tail  
    splin@splin-VirtualBox:~/3.5.5-RC1/iproc/buildroot$ vim output/build/host-ncurses-5.9/include/curses.tail  
    104行后的注释删除掉：  
    +extern NCURSES_EXPORT(bool)    mouse_trafo (int*, int*, bool);
    ```

## buildroot编译注意点
* 并行编译配置.config    
    `BR2_JLEVEL=2`

## glibc工具链

## Build without buildroot
    export ARCH=arm
    export CROSS_COMPILE=/home/splin/3.5.5-RC1/iproc/buildroot/host/usr/bin/arm-linux-
    
    编译内核时：
    cp ../../buildroot/board/broadcom/hurricane2/linux-3.6.5-flash.config .config
    make HOSTCXX=g++-4.7 HOSTCC=gcc-4.7 oldconfig
    make HOSTCXX=g++-4.7 HOSTCC=gcc-4.7
    
    1. scripts/kconfig/conf --oldconfig Kconfig
    ../../bcmdrivers/Kconfig:39: can't open file "../../bcmdrivers/pka/Kconfig"
    /home/splin/3.5.5-RC1/iproc/kernel/linux-3.6.5/scripts/kconfig/Makefile:30: recipe for target 'oldconfig' failed
    注释pka的编译
    
    2. Can't use '!defined(@array)' (Maybe you should just omit the defined()?) at kernel/timeconst.pl line 373.
    将if (!defined(@val)) 改为if (!(@val))
    
## 编译uboot
    make O=./build-output distclean
    make O=./build-output hurricane2_config
    make O=./build-output all
   
## nand分区

 | name| start| size | notes|
 |:---:|:----:|:----:|:----:|
 |uboot image|  0x00000000| 0x00200000|     2M
 |uboot   env|  0x00200000|0x00400000|      4M
 |kern  image|  0x00600000|0x00a00000|     10M
 |dev    tree|  0x01000000|0x00100000|      1M
 |hard   info|  0x01100000|0x00100000|      1M
 |rootfs     |  0x01200000|0x05000000|     80M
 |apps/libs  |  0x06200000|0x10000000|    256M
 |conf       |  0x16200000|0x02000000|     32M
 |user     fs|  0x18200000|0x14000000|    320M
 |log        |  0x2c200000|0x13d00000|    317M



telnet root用户登录：
/etc/security

## ramdisk 内核配置
1. 配置blk及支持ramdisk

2. shell数组表示方法

## gpio

  | gpio|  usage  |
  |:----:|:-----:|
  |gpio0|手动复位，未使用|
  |gpio1|看门狗喂狗信号|
  |gpio2|看门狗使能信号|
  |gpio3|百兆phy复位|
  |gpio4|温度传感器告警输入|
  |gpio5|散热器风扇开关|
  |gpio6| 网卡旁路信号|
  |gpio7| 网卡旁路信号|
    
    