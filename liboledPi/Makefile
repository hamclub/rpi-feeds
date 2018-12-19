#
# Copyright (C) 2018 shawn.chain@gmail.com
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=liboledPi
PKG_REV:=HEAD
PKG_VERSION:=20181213
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hamclub/rpi-oled
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz

#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)
#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)

include $(INCLUDE_DIR)/package.mk

define Package/liboledPi
	SECTION:=libs
	CATEGORY:=GPL
	TITLE:=liboledPi
	SUBMENU:=Libraries
	DEPENDS:=+libstdcpp +libi2c
endef

define Package/liboledPi/description
	RPi OLED userspace driver package for OpenWrt by BG5HHP
endef

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) -DOPENWRT=1" \
	CXXFLAGS="$(TARGET_CPPFLAGS) -DOPENWRT=1"

# define Build/Compile
# 	$(MAKE) -C $(PKG_BUILD_DIR) \
# 	LINUX="$(LINUX_DIR)" \
# 	CC="$(TARGET_CC)" \
# 	CXX="$(TARGET_CXX)" \
# 	STAGING_DIR="$(STAGING_DIR)" \
# 	LDFLAGS="$(TARGET_LDFLAGS)"
# endef

define Package/liboledPi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/liboledPi.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/spi_test $(1)/usr/bin/
	$(CP) $(PKG_BUILD_DIR)/oled_test $(1)/usr/bin/

	# $(INSTALL_DIR) $(STAGING_DIR)/usr/include
	# $(CP) $(PKG_BUILD_DIR)/*.h $(STAGING_DIR)/usr/include/
#	$(CP) $(PKG_BUILD_DIR)/devLib/*.h $(1)/usr/include/
#	$(CP) $(PKG_BUILD_DIR)/liboledPi/*.h $(1)/usr/include/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/liboledPi.so* $(STAGING_DIR)/usr/lib/
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include
	$(CP) $(PKG_BUILD_DIR)/*.h $(STAGING_DIR)/usr/include/
endef

$(eval $(call BuildPackage,liboledPi))
