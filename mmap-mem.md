# /dev/mem mmap程序

## 热启动为例，保留部分内存用作热启动

    #include <stdio.h>
    #include <unistd.h>
    #include <sys/types.h>
    #include <sys/stat.h>
    #include <fcntl.h>
    #include <sys/mman.h>


    #define  MAGIC_RD   0x0
    #define  MAGIC_WR   0x1

    #define  MAGIC1     0x012ee51c
    #define  MAGIC2     0x012f3468
    #define  MAGIC3     0x0133c90b

    #if defined(GSWA_CONFIG)
    #define  PHY_ADDR   0xfff00000
    #else
    #define  PHY_ADDR   0x9ff00000
    #endif

    int boot_magic_ioctl(char opt,
                         int *magic1,
                         int *magic2,
                         int *magic3)
    {   
        int     fd;
        off_t   offset;
        long    page;
        int    *vaddr;
        void   *base;

    
        if (opt != MAGIC_RD && opt != MAGIC_WR)
        {   
            return -1;
        }
        
        page = sysconf(_SC_PAGESIZE);
        
        fd = open("/dev/mem", O_RDWR | O_SYNC);
        if (fd < 0)
        {   
            return -1;
        }
        
        offset = PHY_ADDR & ~(page-1);
        base = mmap(NULL, page, PROT_READ | PROT_WRITE, MAP_SHARED, fd, offset);
        if (base == MAP_FAILED)
        {
            close(fd);
            return -1;
        }

        vaddr = (int *)(base + (PHY_ADDR & (page -1)));

        if (opt == MAGIC_RD)
        {
            *magic1 = *vaddr;
            *magic2 = *(vaddr+1);
            *magic3 = *(vaddr+2);
        }
        else
        {
            *vaddr     = *magic1;
            *(vaddr+1) = *magic2;
            *(vaddr+2) = *magic3;
        }

        munmap(base, page);
        close(fd);

    }