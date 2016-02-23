include $(TOPDIR)/rules.mk

PKG_NAME:=anomaly-detectors
PKG_VERSION:=1.2.1
PKG_RELEASE:=1
PKG_MAINTAINER:=Alexander Duff <amd435@drexel.edu>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/alexanderduff/linux_anomaly_detection.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/anomaly-detectors
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call-Based Anomaly Detectors
	DEPENDS:=+librt +libpthread +libstdcpp +syscall-sensors
endef

define Package/anomaly-detectors/description
This is a program that works with the sycall-sensors
program to monitor kernel-level system calls and
detect when an anomalous state is occurring on the system.
endef

define Package/anomaly-detectors/config
	source "$(SOURCE)/Config.in"
endef

define Build/Prepare
ifeq ($(CONFIG_ANOMALY_DETECTORS_LOCAL),y)
	rm -rf $(PKG_BUILD_DIR)/
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(CONFIG_ANOMALY_DETECTORS_LOCAL_SOURCE_PATH)* $(PKG_BUILD_DIR)
else
	$(PKG_UNPACK)
endif
endef

define Package/anomaly-detectors/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/anomaly-detectors $(1)/usr/sbin
endef

ifeq ($(CONFIG_ANOMALY_DETECTORS_GDB),y)
  CFLAGS += -g
  CXXFLAGS += -g
endif

$(eval $(call BuildPackage,anomaly-detectors))
