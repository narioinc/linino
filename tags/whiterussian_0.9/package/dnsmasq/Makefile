# $Id$

include $(TOPDIR)/rules.mk

PKG_NAME:=dnsmasq
PKG_VERSION:=2.35
PKG_RELEASE:=1
PKG_MD5SUM:=57b8643dc394cf2fbd1bced64536c6df

PKG_SOURCE_URL:=http://thekelleys.org.uk/dnsmasq
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_CAT:=zcat

include $(TOPDIR)/package/rules.mk

$(eval $(call PKG_template,DNSMASQ,$(PKG_NAME),$(PKG_VERSION)-$(PKG_RELEASE),$(ARCH)))

$(PKG_BUILD_DIR)/.configured:
	touch $@

$(PKG_BUILD_DIR)/.built:
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC=$(TARGET_CC) CFLAGS="$(TARGET_CFLAGS) -DHAVE_ISC_READER=1" \
		BINDIR=/usr/sbin MANDIR=/usr/man
	touch $@

$(IPKG_DNSMASQ):
	install -d -m0755 $(IDIR_DNSMASQ)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/src/$(PKG_NAME) $(IDIR_DNSMASQ)/usr/sbin/
	install -d -m0755 $(IDIR_DNSMASQ)/etc/init.d/
	install -m0644 ./files/dnsmasq.conf $(IDIR_DNSMASQ)/etc/dnsmasq.conf
	install -m0755 ./files/S60dnsmasq $(IDIR_DNSMASQ)/etc/init.d/S60dnsmasq
	$(RSTRIP) $(IDIR_DNSMASQ)
	$(IPKG_BUILD) $(IDIR_DNSMASQ) $(PACKAGE_DIR)

