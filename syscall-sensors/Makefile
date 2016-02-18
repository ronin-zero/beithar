include $(TOPDIR)/rules.mk

PKG_NAME:=syscall-sensors
PKG_VERSION:=1.2.10
PKG_RELEASE:=1
PKG_MAINTAINER:=Alexander Duff <amd435@drexel.edu>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/alexanderduff/linux_sensors.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk


define Package/syscall-sensors
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call Sensors 
endef

define Package/syscall-sensors/description
A program for monitoring system calls made by
processes.  They can be used to train a
support-vector machine for malware detection.
endef

define Package/syscall-sensors/config
	source "$(SOURCE)/Config.in"
endef


define Build/Prepare
	echo "ayyyy"
ifeq ($(CONFIG_SYSCALL_SENSORS_LOCAL),y)
	rm -rf $(PKG_BUILD_DIR)/
	mkdir -p $(PKG_BUILD_DIR)
	echo ""
	echo "$(CONFIG_SYSCALLS_LOCAL_SOURCE_PATH)"
	echo ""
	$(CP) $(CONFIG_SYSCALLS_LOCAL_SOURCE_PATH)* $(PKG_BUILD_DIR)
else
	echo ""
	echo "Not using local source..."
	echo ""
	$(PKG_UNPACK)
endif
endef


define Package/syscall-sensors/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/syscall-sensors $(1)/usr/sbin
endef

ifeq ($(CONFIG_SYSCALL_SENSORS_GDB),y)
  CFLAGS += -g
  CXXFLAGS += -g
endif

$(eval $(call BuildPackage,syscall-sensors))
