#
# Copyright (C) 2008-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

### Remarks
### 'python pascal ruby lua' need to be deleted in src/clients/Makefile.am

include $(TOPDIR)/rules.mk

PKG_NAME:=knxd
PKG_VERSION:=0.14.18
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/knxd/knxd.git
PKG_SOURCE_VERSION:=5e707fdb7430009a299d3ad849aecf9ccbc8fdf6
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MIRROR_HASH:=96d5dd7b1513ccf871aed2bdd2601ca2a2f2d1005462fb1c631e5683e2e86e4e

PKG_MAINTAINER:=Othmar Truniger <github@truniger.ch>

PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_BUILD_DEPENDS:=argp-standalone

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/knxd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=EIB KNX daemon
  DEPENDS:=+libusb-1.0 +libstdcpp +libev
endef

define Package/knxd/description
EIB KNX Daemon
endef

define Package/knxd/conffiles
/etc/config/knxd.ini
endef

TARGET_CXXFLAGS+= -std=c++0x
TARGET_CXX=$(TARGET_CC)

CONFIGURE_ARGS+= \
	--disable-systemd

EXTRA_LDFLAGS+= \
	-largp -lstdc++

define Package/knxd/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libeibclient.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/knxd_args $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/knxd/eibwrite-cgi $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/knxd/eibread-cgi $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/knxd.init $(1)/etc/init.d/knxd

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/knxd.ini $(1)/etc/config/knxd.ini
endef

$(eval $(call BuildPackage,knxd))
