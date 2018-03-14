# freescale 文件系统目录结构说明
本文档阐述freescale文件系统,涉及相关文件的部署位置，方面相关人员开发调试程序。

## rootfs目录结构
```
.  
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── linuxrc -> /bin/busybox
├── media
├── mnt
├── proc
├── run
├── sbin
├── sys
├── tmp
├── usr
└── var
```

## 文件部署
1. 应用程序  
    ```
    /home/root/apps/
    ├── igmpd
    ├── l2d
    ├── mstp
    └── wdt.sh
    ```
    APPS程序部署在/home/root/apps目录下，如l2d,igmpd等。
    
2. 配置文件部署  
    ```
    /etc/fhos/
    └── l2d.conf
    ```
    APPS程序的默认配置文件部署路径在/etc/fhos目录下，如l2d.conf等。
    
3. Libs库部署  
    ```
    /home/root/libs/
    ├── libarchive.so -> libarchive.so.13.3.2
    ├── libarchive.so.13 -> libarchive.so.13.3.2
    ├── libarchive.so.13.3.2
    ├── libcares.so -> libcares.so.2.2.0
    ```
    系统使用的动态库部署在/home/root/libs目录下，如上图所示。
    
4. modules部署  
    ```
    /home/root/mods/
    ├── linux-bcm-knet.ko
    ├── linux-kernel-bde.ko
    └── linux-user-bde.ko
    ```
    linux内核modules部署在/home/root/mods目录下，如上图所示。
    
5. 运行文件部署  
    ```
    /var/run/fhos
    └── l2d.pid
    ```
    程序运行时需要的文件部署在/var/run/fhos目录下，如l2d.pid 文件。
    
6. 日志文件部署
    ```
    /tmp/log/
    └── xxx.log
    ```
    程序的日志文件写到/tmp/log目录下，由后台进程刷新到flash中。
 
## 参考
* [freescale文件系统构建说明](http://10.0.0.3:9000/zhangjm/fhos/wikis/Design/fsl_rootfs_build)
  
## 问题反馈
在使用过程中有任何疑问或者bug，欢迎反馈:

* 作者: splin
* 邮箱: linshunping@yuqiinf.com  



