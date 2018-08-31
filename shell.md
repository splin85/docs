# shell
## du
    splin@splin-VirtualBox:~/fhos_work/fhos/rootfs$ du -m -d 1
    1	./OBJS
    146	./rootfs_201808151118
    7	./common
    88	./freescale
    104	./broadcom
    398	.

## free
    # free -m
             total       used       free     shared    buffers     cached
    Mem:       484        314        170          0          3         45
    -/+ buffers/cache:    266        218
    Swap:        0          0          0

1. Mem行total=used+free，表示物理内存的统计
2. 第二行 used=used(Mem)-buffers/cache  free=free(Mem)+buffers/cache
    表示linux系统内存的统计，由于buffers/cache可以被回收，所以free增加。