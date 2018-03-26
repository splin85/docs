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