# freescale 文件系统构建说明  
    本文档阐述freescale文件系统的构建过程。
    
## 系统构建步骤
1. git工程库  
    `git clone http://git-cdyq.com:9000/zhangjm/fhos.git`
 
2. 工程构建  
    进入工程目录，source环境变量，如：
    ```
    splin@splin-VirtualBox:~/fhos_work/fhos$ source fsl_env 
    splin@splin-VirtualBox:~/fhos_work/fhos$ make -j4
    ```
   dddd 
    如果已经构建过工程，则可进入rootfs目录下，只重新生成文件系统：
    ```
    splin@splin-VirtualBox:~/fhos_work/fhos$ cd rootfs/
    splin@splin-VirtualBox:~/fhos_work/fhos/rootfs$ make -j4
    ```

    构建的文件系统rootfs在：
    ```
    splin@splin-VirtualBox:~/fhos_work/fhos/build/freescale/arm/release/rootfs$ ls -l
    total 187900
    -rw-rw-r-- 1 splin splin 64242846 3月   9 15:23 rootfs.201803091523.ext2.gz
    -rw-rw-r-- 1 splin splin 64242910 3月   9 15:23 rootfs.201803091523.ext2.gz.u-boot
    -rw-rw-r-- 1 splin splin 63914847 3月   9 15:23 rootfs.201803091523.tar.gz
    ```
   
 ##  文件系统构建对象
 本文件系统的构建依赖于工程的编译系统，编译系统首先会构建整个代码工程，生成busybox,linux内核模块,APP程序等，
 然后rootfs构建工具将这些程序打包成文件系统。
 
    
 |     文件        |        build工程路径                               |   rootfs路径    |    备注              |
 | :-------------  | :------------------------------------------------- | :-------------- | :-------             |
 | busybox         | build/freescale/arm/release/busybox                | /bin;/sbin;etc  | 暂不支持busybox的裁剪|
 | 启动脚本        | rootfs/freescale/extra_fs/etc                      | /etc            | 如sw_init.sh,preinit.sh|
 | APP程序         | build/freescale/arm/release/user                   | /home/root/apps | 如l2d |
 | APP默认配置文件 | rootfs/freescale/extra_fs/etc/fhos                 | /etc/fhos       | 如l2d.conf |
 | libs库文件      | build/freescale/arm/lib                            | /home/root/libs | 如libfrr.so |
 | modules         | hal/switch/sdk/broadcom/build/linux/user/fhos-4_1  | /home/root/mods | 如linux-kernel-bde.ko |
 
  
## 参考
* [freescale文件系统目录结构说明](http://10.0.0.3:9000/zhangjm/fhos/wikis/Design/fsl_rootfs_design)

## 问题反馈
在使用过程中有任何疑问或者bug，欢迎反馈:

* 作者: splin
* 邮箱: linshunping@yuqiinf.com 