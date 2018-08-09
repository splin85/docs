# Makefile tips
1. $@ 目标文件, $^所有的文件，$< 第一个文件  

## example
    
    # Copyright (C) 2018 Bei Jing Fu Hua Yu Qi Info Tech, Inc
    #
    # @author splin
    # @date 08/08/18

    ifeq ($(PRJ_DIR), )
      PRJ_DIR = $(CURDIR)/../../
      export PRJ_DIR

      include $(PRJ_DIR)/make/make.topdirs
    endif

    RM = rm -rf 
    CC = $(CROSS_COMPILE)gcc
     
    ifeq ($(PLATFORM), freescale)
        SYSROOT = --sysroot=/opt/fsl-qoriq/2.0/sysroots/cortexa7hf-vfp-neon-fsl-linux-gnueabi
        FHOS_CFLAGS = -march=armv7-a -mfloat-abi=hard -mfpu=neon -mtune=cortex-a7 $(SYSROOT)
        HOST_CFLAGS = --host=arm-fsl-linux-gnueabi
    else ifeq ($(PLATFORM), broadcom)
        SYSROOT = --sysroot=/opt/bcm/iproc/usr/arm-broadcom-linux-gnueabi/sysroot
        FHOS_CFLAGS = $(SYSROOT)
        HOST_CFLAGS = --host=arm-broadcom-linux-gnueabi
    else
        $(error unsupport platform: $(PLATFORM))
    endif


    export LIBMNL_CFLAGS = "-I$(BUILD_DIR)/include"
    export LIBMNL_LIBS = "-L$(BUILD_DIR)/lib -lmnl"
    export LIBNFTNL_CFLAGS = "-I$(BUILD_DIR)/include"
    export LIBNFTNL_LIBS = "-L$(BUILD_DIR)/lib -lnftnl"

    NFT_CFLAGS = --prefix=$(BUILD_DIR) \
                 --with-mini-gmp       \   
                 --disable-man-doc


    .PHONY: all clean

    all: configure
        ./configure $(HOST_CFLAGS) CFLAGS="$(FHOS_CFLAGS)" $(NFT_CFLAGS)
        make && make install

    clean:
    ifneq ($(wildcard Makefile),)
        make clean
    endif
        $(RM) $(BUILD_DIR)/include/nftables
        $(RM) $(BUILD_DIR)/lib/libnftables*
        $(RM) $(BUILD_DIR)/lib/pkgconfig/libnftables.pc