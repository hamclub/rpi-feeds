include $(TOPDIR)/rules.mk

PKG_NAME:=ArduiPi_OLED
PKG_REV:=HEAD
PKG_VERSION:=BG5HHP-20180824
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/hallard/ArduiPi_OLED
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git

#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/ArduiPi_OLED
	SECTION:=libs
	CATEGORY:=Atom-GPL
	TITLE:=ArduiPi_OLED
	SUBMENU:=Libraries
	DEPENDS:=+libpthread +wiringPi
endef

define Package/ArduiPi_OLED/description
	C GPIO libraries for the RPI
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/ArduiPi_OLED/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libArduiPi_OLED.so.* $(1)/usr/lib/libArduiPi_OLED.so
	cp $(PKG_BUILD_DIR)/Adafruit_*.h $(1)/usr/include/
	cp $(PKG_BUILD_DIR)/ArduiPi_*.h $(1)/usr/include/
	cp $(PKG_BUILD_DIR)/bcm2835.h $(1)/usr/include/
endef

# define Build/InstallDev
# 	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/
# 	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
# 	cp $(PKG_BUILD_DIR)/devLib/libArduiPi_OLEDDev.so* $(STAGING_DIR)/usr/lib/libArduiPi_OLED.so
# 	cp $(PKG_BUILD_DIR)/Adafruit_*.h $(STAGING_DIR)/usr/include/
# 	cp $(PKG_BUILD_DIR)/ArduiPi_*.h $(STAGING_DIR)/usr/include/
# 	cp $(PKG_BUILD_DIR)/bcm2835.h $(STAGING_DIR)/usr/include/
# endef

$(eval $(call BuildPackage,ArduiPi_OLED,+wiringPi))