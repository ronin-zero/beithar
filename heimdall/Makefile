include $(TOPDIR)/rules.mk

PKG_NAME:=heimdall
PKG_VERSION:=2.01
PKG_RELEASE:=11
PKG_MAINTAINER:=ronin-zero <ronin-zero@github.com>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ronin-zero/heimdall.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/heimdall/default
	SUBMENU:=heimdall
 	SECTION:=utils
 	CATEGORY:=Utilities
 	TITLE:=Heimdall Malware/Anomaly Detection Suite
endef

define Package/heimdall
	$(call Package/heimdall/default)
	MENU:=1
endef

define Package/heimdall/config
	source "$(SOURCE)/Config.in"
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

The detectors are implemented and available.  To include them, select pacakge
"syscall-detector."

Mitigators are theoretical, but hopefully coming.
endef

define Package/syscall-sensor
	$(call Package/heimdall/default)
	MENU:=1
	TITLE:=System Call Sensing Utility
	DEPENDS:=+librt +libpthread +libstdcpp +@KERNEL_FTRACE +@KERNEL_FTRACE_SYSCALLS +@KERNEL_FUNCTION_TRACER +@KERNEL_FUNCTION_GRAPH_TRACER +@KERNEL_DYNAMIC_FTRACE
endef

define Package/syscall-sensor/config 
	source "$(SOURCE)/syscall-sensor/Config.in"
endef

define Package/syscall-sensor/description
This program reads system call information from ftrace and logs it to an output file.
See 'syscall-sensor -h' or 'syscall-sensor --help' for more information.
endef

SYSCALL-SENSOR_SUBDIR:=$(PKG_BUILD_DIR)/syscall-sensor

ifeq ($(CONFIG_SYSCALL-SENSOR_GDB),y)
	SYSCALL-SENSOR_CONF_OPT:=-DCMAKE_BUILD_TYPE=Debug
else
 	SYSCALL-SENSOR_CONF_OPT:=-DCMAKE_BUILD_TYPE=Release
endif

ifeq ($(CONFIG_SYSCALL-SENSOR_DEBUG_COUT),y)
	SYSCALL-SENSOR_MAKE_OPT:=-DDEBUG_COUT
endif

define Package/syscall-detector
	$(call Package/heimdall/default)
	MENU:=1
	TITLE:=System Call-Based Anomaly Detector
	DEPENDS:=+librt +libpthread +libstdcpp +@KERNEL_FTRACE +@KERNEL_FTRACE_SYSCALLS +@KERNEL_FUNCTION_TRACER +@KERNEL_FUNCTION_GRAPH_TRACER +@KERNEL_DYNAMIC_FTRACE
endef

define Package/syscall-detector/config
	source "$(SOURCE)/syscall-detector/Config.in"
endef

define Package/syscall-detector/description
This program monitors sequences of system calls.  Based on frequencies of ngrams of
system calls over the course of a given trace window, it performs anomaly detection.
See 'syscall-detector -h' or syscall-detector --help' for more information.
endef

SYSCALL-DETECTOR_SUBDIR:=$(PKG_BUILD_DIR)/syscall-detector

ifeq ($(CONFIG_SYSCALL-DETECTOR_GDB),y)
	SYSCALL-DETECTOR_CONF_OPT:=-DCMAKE_BUILD_TYPE=Debug
else
	SYSCALL-DETECTOR_CONF_OPT:=-DCMAKE_BUILD_TYPE=Release
endif

define Build/Clean
	rm -rf $(PKG_BUILD_DIR)
endef

define Build/Prepare

ifeq ($(CONFIG_HEIMDALL_LOCAL),y)
	rm -rf $(PKG_BUILD_DIR)/
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(CONFIG_HEIMDALL_LOCAL_SOURCE_PATH)* $(PKG_BUILD_DIR)
else
	$(PKG_UNPACK)
endif

endef

define Package/syscall-sensor/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(SYSCALL-SENSOR_SUBDIR)/bin/syscall-sensor $(1)/usr/sbin
endef

define Package/syscall-detector/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(SYSCALL-DETECTOR_SUBDIR)/bin/syscall-detector $(1)/usr/sbin
endef

$(eval $(call BuildPackage,heimdall))
$(eval $(call BuildPackage,syscall-sensor))
$(eval $(call BuildPackage,syscall-detector))
