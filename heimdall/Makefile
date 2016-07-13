include $(TOPDIR)/rules.mk

PKG_NAME:=heimdall
PKG_VERSION:=1.0
PKG_RELEASE:=1
PKG_MAINTAINER:=ronin-zero (浪人ー無) <ronin-zero@github.com>

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
  This is a set of utilities for malware and anomaly detection.
  For instance, syscall-sensor is a utility that
  logs system call information.
endef

define Package/syscall-sensor
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call Sensing Utility
	DEPENDS:=heimdall +librt +libpthread +libstdcpp \
		+@KERNEL_FTRACE +@KERNEL_FTRACE_SYSCALLS +@KERNEL_ENABLE_DEFAULT_TRACERS +@KERNEL_FUNCTION_TRACER \
		+@KERNEL_FUNCTION_GRAPH_TRACER +@KERNEL_DYNAMIC_FTRACE +@KERNEL_FUNCTION_PROFILER
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
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/syscall-sensor/ $(1)/usr/sbin
endef

$(eval $(call BuildPackage,heimdall))
$(eval $(call BuildPackage,syscall-sensor))
