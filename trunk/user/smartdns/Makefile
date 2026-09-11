SRC_NAME = smartdns-Release48.1
THISDIR = $(shell pwd)

all: extract_test config_test
	$(MAKE) -C $(SRC_NAME) \
		CFLAGS="$(CFLAGS) -ffunction-sections -fdata-sections" \
		LDFLAGS="$(LDFLAGS) -Wl,--gc-sections" WITH_ZLIB=0 NO_GIT_VER=1

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar -xf $(SRC_NAME).tar.gz ; \
		patch -d $(SRC_NAME) -p1 < $(SRC_NAME).patch ; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		touch config_done; \
	fi )

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) clean ; \
	fi ; \
	rm -f config_done

romfs:
	$(ROMFSINST) -p +x $(THISDIR)/$(SRC_NAME)/src/smartdns /usr/bin/smartdns
	cp -fP $(CONFIG_CROSS_COMPILER_ROOT)/mipsel-linux-uclibc/sysroot/lib/libatomic.so.1* $(ROMFSDIR)/lib
