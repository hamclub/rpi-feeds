#
# Copyright (C) 2018 shawn.chain@gmail.com
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=oledPi
PKG_REV:=HEAD
PKG_VERSION:=20180830
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hallard/ArduiPi_OLED.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz

#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)
#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)

include $(INCLUDE_DIR)/package.mk

define Package/oledPi
	SECTION:=libs
	CATEGORY:=Atom-GPL
	TITLE:=oledPi
	SUBMENU:=Libraries
	DEPENDS:=+libstdcpp +libi2c
endef

define Package/oledPi/description
	ArduiPi_OLED package for OpenWrt by BG5HHP
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CXX="$(TARGET_CXX)" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS)" ArduiPi_OLED

	$(CP) "$(PKG_BUILD_DIR)/libArduiPi_OLED.so.1.0" "$(PKG_BUILD_DIR)/libArduiPi_OLED.so"
	$(MAKE) -C $(PKG_BUILD_DIR)/examples \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC) -I.." \
	CXX="$(TARGET_CXX) -I.." \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L.."
endef

define Package/oledPi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libArduiPi_OLED.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/examples/oled_demo $(1)/usr/bin/

	# $(INSTALL_DIR) $(STAGING_DIR)/usr/include
	# $(CP) $(PKG_BUILD_DIR)/*.h $(STAGING_DIR)/usr/include/
#	$(CP) $(PKG_BUILD_DIR)/devLib/*.h $(1)/usr/include/
#	$(CP) $(PKG_BUILD_DIR)/oledPi/*.h $(1)/usr/include/
endef

define Build/InstallDev 
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libArduiPi_OLED.so* $(STAGING_DIR)/usr/lib/
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include
	$(CP) $(PKG_BUILD_DIR)/*.h $(STAGING_DIR)/usr/include/
endef

$(eval $(call BuildPackage,oledPi))
