# 龙芯2K1000 PMON及Kernel移植

## 设置工具链环境变量
    export PATH=/home/splin/loongson/opt/gcc-4.4-gnu/bin/:$PATH
    export ARCH=mips
    export CROSS_COMPILE=mipsel-linux-
    
## 编译PMON
    1. make CROSS_COMPILE=mipsel-linux- clean
    2. make tgt=rom cfg all CROSS_COMPILE=mipsel-linux- 
    3. make dtb CROSS_COMPILE=mipsel-linux- 
    
## 编译内核
    1. cp arch/mips/configs/loongson2k1000_defconfig .config
    2. make ARCH=mips CROSS_COMPILE=mipsel-linux- menuconfig
    3. make ARCH=mips CROSS_COMPILE=mipsel-linux- -j2
    
## PMON设置mac地址及ip地址
    set ethaddr 02:03:04:05:06:07; ifconfig syn0 up; ifconfig syn0 10.0.0.38
    
## 升级PMON
    load -r -f 0xbfc00000 tftp://10.0.0.36/gzrom-dtb.bin
    
## 加载内核
    load tftp://10.0.0.36/vmlinux;g console=ttyS0,115200 root=/dev/sda1
    
## 串口调试
    1. 根据板子，配置内核.config中的串口个数为4
        CONFIG_SERIAL_8250_NR_UARTS=4
        
    2. 修改pmon的dts， 添加串口设备
        serial0x@0x1fe00000{
            device_type = "serial";                                                          
            compatible = "ns16550";
            reg = <0x1fe00000 0x100>;
            clock-frequency = <125000000>;                                                   
            interrupt-parent = <&icu>;                                                       
            interrupts = <8>;                                                                
        };                                                                                   

        serial3x@0x1fe00300{
            device_type = "serial";                                                          
            compatible = "ns16550";
            reg = <0x1fe00300 0x100>;
            clock-frequency = <125000000>;                                                   
            interrupt-parent = <&icu>;                                                       
            interrupts = <8>;                                                                
        };                                                                                   

        serial4x@0x1fe00400{
            device_type = "serial";                                                          
            compatible = "ns16550";
            reg = <0x1fe00400 0x100>;
            clock-frequency = <125000000>;                                                   
            interrupt-parent = <&icu>;                                                       
            interrupts = <9>;                                                                
        };                                                                                   

        serial5x@0x1fe00500{
            device_type = "serial";                                                          
            compatible = "ns16550";
            reg = <0x1fe00500 0x100>;
            clock-frequency = <125000000>;                                                   
            interrupt-parent = <&icu>;                                                       
            interrupts = <9>;                                                                
        };                          
        
    3. 设置串口属性:
        stty -F /dev/ttyS1 speed 115200 -parenb -ixon cs8
   
    
## PMON源码
    1, 通过usb，sd卡启动操作系统，需要设置root_delay，延迟VFS挂载。
    2, 内存加载文件系统，使用initrd，pmon使用initrd命令或者把文件系统编译进文件系统里面。
    3, 自动加载到内存，启动操作系统，变量设置：
        PMON> env
        installdelay = 5         
        FR = 1         
        rd = /dev/fs/ext2@sdcard0/rootfs.cpio.gz
        al = /dev/fs/ext2@sdcard0/vmlinux
        al1 = /dev/fs/ext2@sdcard0/vmlinux
        append = console=ttyS0,115200
        netaddr = 10.0.0.38 
        netmask = 255.255.255.0
        broadcast = 10.0.0.255
        ifconfig = 10.0.0.38 
        activecom = 0x00      
        em_enable = 0x00      
        ethaddr = 02:03:04:05:06:07
        memsize = 240       
        highmemsize = 1792      
        cpuclock = 999880000 
        busclock = 66000000  
        systype = FCR       
        brkcmd = "l -r @cpc 1"
        datasize = -b          [-b -h -w -d]
        dlecho = off         [off on lfeed]
        dlproto = none        [none XonXoff EtxAck]
        bootp = no          [no sec pri save]
        hostport = tty0      
        inalpha = hex         [hex symbol]
        inbase = 16          [auto 8 10 16]
        moresz = 10        
        prompt = "PMON> "
        regstyle = sw          [hw sw]
        regsize = 32          [32 64]
        rptcmd = trace       [off on trace]
        trabort = ^K        
        ulcr = cr          [cr lf crlf]
        uleof = %         
        showsym = yes         [no yes]
        fpfmt = both        [both double single none]
        fpdis = yes         [no yes]
        mtdparts = nand-flash:30M@0(kernel),-(rootfs);spinand_flash:30M@0(kernel),-(rootfs)
        bootdelay = 3
