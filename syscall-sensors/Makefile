include $(TOPDIR)/rules.mk

PKG_NAME:=syscall-sensors
PKG_VERSION:=1.2.8
PKG_RELEASE:=1
PKG_MAINTAINER:=Alexander Duff <amd435@drexel.edu>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/alexanderduff/linux_sensors.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

CMAKE_INSTALL:=1

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
	$(PKG_UNPACK)
endef

define Package/syscall-sensors/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/syscall-sensors $(1)/usr/sbin
endef

$(eval $(call BuildPackage,syscall-sensors))
