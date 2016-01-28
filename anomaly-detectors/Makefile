include $(TOPDIR)/rules.mk

PKG_NAME:=anomaly-detectors
PKG_VERSION:=1.2.0
PKG_RELEASE:=1
PKG_MAINTAINER:=Alexander Duff <amd435@drexel.edu>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/alexanderduff/linux_anomaly_detection.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=HEAD

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/anomaly-detectors
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=System Call-Based Anomaly Detectors
	DEPENDS:=+libpthread +libc +libcstdcpp +librt
endef

define Package/anomaly-detectors/description
This is a program that works with the sycall-sensors
program to monitor kernel-level system calls and
detect when an anomalous state is occurring on the system.
endef

define Build/Prepare
	$(PKG_UNPACK)
endef

define Package/anomaly-detectors/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/anomaly-detectors $(1)/usr/sbin
endef

$(eval $(call BuildPackage,anomaly-detectors))
