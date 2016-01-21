include $(TOPDIR)/rules.mk

PKG_NAME:=syscall-sensors
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/syscall-sensors
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call Sensors
	DEPENDS:=+libpthread +libc +libstdcpp +librt
endef

define Package/syscall-sensors/description
A program for monitoring system calls made by
processes.  They can be used to train a
support-vector machine for malware detection.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) -r ./src/* $(PKG_BUILD_DIR)/
endef

define Package/syscall-sensors/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/syscall-sensors $(1)/usr/sbin
endef

$(eval $(call BuildPackage,syscall-sensors))
