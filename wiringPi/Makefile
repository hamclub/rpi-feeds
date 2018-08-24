include $(TOPDIR)/rules.mk

PKG_NAME:=wiringPi
PKG_REV:=HEAD
PKG_VERSION:=BG5HHP-20180824
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/WiringPi/WiringPi.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git

#PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

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

	cp $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so
	cp $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so

	$(MAKE) -C $(PKG_BUILD_DIR)/gpio \
	LINUX="$(LINUX_DIR)" \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/wiringPi -I$(PKG_BUILD_DIR)/devLib" \
	STAGING_DIR="$(STAGING_DIR)" \
	LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR)/wiringPi -L$(PKG_BUILD_DIR)/devLib -lwiringPiDev"
endef

define Package/wiringPi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/gpio/gpio $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so.* $(1)/usr/lib/libwiringPiDev.so
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/devLib/*.h $(1)/usr/include/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so.* $(1)/usr/lib/libwiringPi.so
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wiringPi/*.h $(1)/usr/include/
endef

#define Build/InstallDev
#	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/
#	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
#	cp $(PKG_BUILD_DIR)/devLib/libwiringPiDev.so* $(STAGING_DIR)/usr/lib/libwiringPiDev.so
#	cp $(PKG_BUILD_DIR)/devLib/*.h $(STAGING_DIR)/usr/include/
#	cp $(PKG_BUILD_DIR)/wiringPi/libwiringPi.so* $(STAGING_DIR)/usr/lib/libwiringPi.so
#	cp $(PKG_BUILD_DIR)/wiringPi/*.h $(STAGING_DIR)/usr/include/
#endef

$(eval $(call BuildPackage,wiringPi))