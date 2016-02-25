include $(TOPDIR)/rules.mk

PKG_NAME:=syscall-sensors
PKG_VERSION:=1.3.1
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
	DEPENDS:=+librt +libpthread +libstdcpp +@KERNEL_FTRACE +@KERNEL_FTRACE_SYSCALLS +@KERNEL_ENABLE_DEFAULT_TRACERS +@KERNEL_FUNCTION_TRACER +@KERNEL_FUNCTION_GRAPH_TRACER +@KERNEL_DYNAMIC_FTRACE +@KERNEL_FUNCTION_PROFILER
endef

define Package/syscall-sensors/description
A program for monitoring system calls made by
processes.  They can be used to train a
support-vector machine for malware detection.
endef

define Package/syscall-sensors/config
	source "$(SOURCE)/Config.in"
endef

define Build/Clean
	rm -rf $(PKG_BUILD_DIR)/
endef

define Build/Prepare

ifeq ($(CONFIG_SYSCALL_SENSORS_LOCAL),y)
	rm -rf $(PKG_BUILD_DIR)/
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(CONFIG_SYSCALL_SENSORS_LOCAL_SOURCE_PATH)* $(PKG_BUILD_DIR)
else
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
