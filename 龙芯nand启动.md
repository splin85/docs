# 龙芯nand加载内核及文件系统
## 修改linux
    1. 打上龙芯公司提供的补丁
    2. 修改drivers/mtd/nand/nand_ids.c，增加：
        /* add for loongson by splin */                                                                                            
        EXTENDED_ID_NAND("NAND 2GiB 3,3V 8-bit", 0x48, 2048, LP_OPTIONS),
    
## 修改PMON
    1. 修改dts的nand配置：
        partition@0 {                                                                                                      
            label = "kernel_partition";                                                                                    
            reg = <0x0000000 0x01e00000>;                                                                                  
         };                                                                                                                 
                                                                                                                            
        partition@0x01400000 {                                                                                             
            label = "rootfs_partition";                                                                                    
            reg = <0x01e00000 0x0>;                                                                                        
        };
     
    2. nand源码修改前期调试已经修改完成
            
## 烧写nand flash
    1. PMON烧写nand
        devcp tftp://10.0.0.36/vmlinx /dev/mtd/kernel
        由于使用该命令，系统会不断循环打印网卡收到异常中断的错误消息；
        麻烦上海同事在你们的开发板上测试下，排除板子的差异(龙芯反馈参考板没有复现该问题)。
        
    2. linux烧写nand
        采用sd启动方式，进入linux系统，然后烧写vmlinux及rootfs至nand flash
        mtd_debug erase /dev/mtd0 0x0 0x1e00000
        nandwrite -p /dev/mtd0 vmlinux
        
        mtd_debug erase /dev/mtd1 0x0 0x20000000
        nandwrite -p /dev/mtd1 rootfs
    
## PMON启动内核配置
    1. 设置PMON从nand加载系统：
        rd = /dev/mtd/rootfs@0,30035872
        al = /dev/mtd/kernel@0,0x1e00000
        al1 = /dev/mtd/kernel@0,0x1e00000
        
    注：3005872为你的rootfs的大小
