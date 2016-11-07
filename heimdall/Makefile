include $(TOPDIR)/rules.mk

PKG_NAME:=heimdall
PKG_VERSION:=1.7
PKG_RELEASE:=8
PKG_MAINTAINER:=ronin-zero <ronin-zero@github.com>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ronin-zero/heimdall.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/heimdall
 	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Heimdall Malware/Anomaly Detection Suite
endef

define Package/heimdall/description
  Heimdall is a robust, configurable security system that coordinates sensors,
  detectors, and mitigators.  Utilizing cutting-edge machine learning techniques,
  Heimdall can monitor a system for anomalous behavior (caused by malware, for
  instance), identify, and mitigate the source.
  
  Currently, this package is in development. Selecting this package will not
  add any code or functionality to your kernel.  It is a stub for development
  purposes.

  The sensors are implemented and available.  To include them, select package
  "syscall-sensor."

  The detectors are coming soon.

  Mitigators are theoretical, but hopefully coming.
endef

define Package/syscall-sensor
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call Sensing Utility
	DEPENDS:=+librt +libpthread +libstdcpp	+@KERNEL_FTRACE +@KERNEL_FTRACE_SYSCALLS
endef

define Package/syscall-sensor/description
  This program reads system call information from ftrace and logs it to an output file.
  See 'syscall-sensor -h' or 'syscall-sensor --help' for more information.
endef

define Build/Clean
	rm -rf $(PKG_BUILD_DIR)
endef

define Build/Prepare
	$(PKG_UNPACK)
endef

define Package/syscall-sensor/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/syscall-sensor $(1)/usr/sbin
endef

$(eval $(call BuildPackage,heimdall))
$(eval $(call BuildPackage,syscall-sensor))
