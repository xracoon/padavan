VERSION = 2.1.18
ARCHIVE = dnscrypt-proxy-linux_mipsle-$(VERSION).tar.gz
URL = https://github.com/DNSCrypt/dnscrypt-proxy/releases/download/$(VERSION)/$(ARCHIVE)
SHA256 = b325339a7f0fc720ea19aec7dd3c3101da9621bdae39cb1f2c823b508ce931a0
DIR = linux-mipsle
THISDIR = $(shell pwd)

all: $(ARCHIVE) extract

$(ARCHIVE):
	@if [ ! -f "$@" ]; then curl -fL --retry 3 -o "$@" "$(URL)"; fi
	@echo "$(SHA256)  $@" | sha256sum -c -

extract: $(ARCHIVE)
	@if [ ! -d "$(DIR)" ]; then tar -xf "$(ARCHIVE)"; fi

clean:
	@true

romfs: all
	$(ROMFSINST) -p +x $(THISDIR)/$(DIR)/dnscrypt-proxy /usr/bin/dnscrypt-proxy
