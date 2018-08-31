#
# Copyright (C) 2018 shawn.chain@gmail.com
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=wiringPi
PKG_REV:=HEAD
PKG_VERSION:=2.46
PKG_RELEASE:=20180830

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/WiringPi/WiringPi.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz

#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)
#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)

include $(INCLUDE_DIR)/package.mk

define Package/wiringPi
	SECTION:=libs
	CATEGORY:=Atom-GPL
	TITLE:=wiringPi
	SUBMENU:=Libraries
	DEPENDS:=+libpthread
endef

define Package/wiringPi/description
	C GPIO libraries for the RPI
endef


define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/wiringPi \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS)"

	$(MAKE) -C $(PKG_BUILD_DIR)/devLib \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/wiringPi" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR)/wiringPi -L$(PKG_BUILD_DIR)/devLib -L$(STAGING_DIR)/lib -L$(STAGING_DIR)/usr/lib"

	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(INSTALL_DIR) $(STAGING_DIR)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(STAGING_DIR)/usr/lib/libwiringPiDev.so
	$(CP) $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(STAGING_DIR)/usr/lib/libwiringPi.so

	$(MAKE) -C $(PKG_BUILD_DIR)/gpio \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/wiringPi -I$(PKG_BUILD_DIR)/devLib" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR)/wiringPi -L$(PKG_BUILD_DIR)/devLib -L$(STAGING_DIR)/lib -L$(STAGING_DIR)/usr/lib -lwiringPiDev"
endef

define Package/wiringPi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(1)/usr/lib/libwiringPi.so
	$(CP) $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(1)/usr/lib/libwiringPiDev.so

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/gpio/gpio $(1)/usr/bin/
#
#	$(INSTALL_DIR) $(1)/usr/include
#	$(CP) $(PKG_BUILD_DIR)/devLib/*.h $(1)/usr/include/
#	$(CP) $(PKG_BUILD_DIR)/wiringPi/*.h $(1)/usr/include/
endef

define Build/InstallDev 
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so* $(STAGING_DIR)/usr/lib/libwiringPiDev.so
	$(CP) $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so* $(STAGING_DIR)/usr/lib/libwiringPi.so

	$(INSTALL_DIR) $(STAGING_DIR)/usr/include
	$(CP) $(PKG_BUILD_DIR)/devLib/*.h $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/wiringPi/*.h $(STAGING_DIR)/usr/include/
endef

$(eval $(call BuildPackage,wiringPi,+libpthread))
