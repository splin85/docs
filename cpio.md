# initrd启动

    find . | cpio -o -H newc > ../rootfs.cpio
    mkimage -n "rootfs" -A arm -O linux -T ramdisk -C gzip -d  rootfs.name rootfs.name.uboot