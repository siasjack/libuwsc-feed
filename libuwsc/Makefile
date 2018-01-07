#
# Copyright (C) 2014-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libuwsc
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/zhaojh329/libuwsc.git
PKG_SOURCE_VERSION:=7bdecbd0d847cbf27111b3cc83d7fdc9eaa597d8
PKG_MIRROR_HASH:=72e13bacb63e5b6ebb49fdf08d2d9919515b1bcf71b47bc76dcbc515765130b4
CMAKE_INSTALL:=1

PKG_BUILD_DIR=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_SOURCE_SUBDIR)

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE

PKG_MAINTAINER:=Jianhui Zhao <jianhuizhao329@gmail.com>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DUWSC_DEBUG=on

define Package/libuwsc/default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Networking
  TITLE:=libuwsc
  DEPENDS:=+libubox
endef

define Package/libuwsc-nossl
  $(Package/libuwsc/default)
  TITLE += (NO SSL)
  VARIANT:=nossl
endef

define Package/libuwsc-openssl
  $(Package/libuwsc/default)
  TITLE += (openssl)
  DEPENDS += +libustream-openssl
  VARIANT:=openssl
endef

define Package/libuwsc-wolfssl
  $(Package/libuwsc/default)
  TITLE += (wolfssl)
  DEPENDS += +libustream-wolfssl
  VARIANT:=wolfssl
endef

define Package/libuwsc-mbedtls
  $(Package/libuwsc/default)
  TITLE += (mbedtls)
  DEPENDS += +libustream-mbedtls
  VARIANT:=mbedtls
endef

ifeq ($(BUILD_VARIANT),nossl)
  CMAKE_OPTIONS += -DUWSC_SSL_SUPPORT=off
endif

define Package/libuwsc/default/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/libuwsc.so* $(1)/usr/lib/
endef

Package/libuwsc-nossl/install = $(Package/libuwsc/default/install)
Package/libuwsc-openssl/install = $(Package/libuwsc/default/install)
Package/libuwsc-wolfssl/install = $(Package/libuwsc/default/install)
Package/libuwsc-mbedtls/install = $(Package/libuwsc/default/install)

$(eval $(call BuildPackage,libuwsc-nossl))
$(eval $(call BuildPackage,libuwsc-mbedtls))
$(eval $(call BuildPackage,libuwsc-wolfssl))
$(eval $(call BuildPackage,libuwsc-openssl))