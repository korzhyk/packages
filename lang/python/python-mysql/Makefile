#
# Copyright (C) 2007-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-mysql
PKG_VERSION:=1.3.12
PKG_RELEASE:=2
PKG_LICENSE:=GPL-2.0

PKG_SOURCE:=mysqlclient-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/source/m/mysqlclient
PKG_HASH:=2d9ec33de39f4d9c64ad7322ede0521d85829ce36a76f9dd3d6ab76a9c8648e5

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-mysql-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../python-package.mk
include ../python3-package.mk

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

# Help python-mysql find libiconv.so when using uClibc.
ifneq ($(CONFIG_USE_UCLIBC),)
TARGET_CPPFLAGS+= \
	-I$(STAGING_DIR)/usr/lib/libiconv-full/include
TARGET_LDFLAGS += \
	-L$(STAGING_DIR)/usr/lib/libiconv-full/lib
endif

define Package/python-mysql/Default
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  URL:=https://pypi.python.org/project/mysqlclient
  MAINTAINER:=Gergely Kiss <mail.gery@gmail.com>
endef

define Package/python-mysql
  $(call Package/python-mysql/Default)
  TITLE:=MySQL database adapter for Python
  DEPENDS:=+PACKAGE_python-mysql:python +libmysqlclient
  VARIANT:=python
endef

define Package/python3-mysql
  $(call Package/python-mysql/Default)
  TITLE:=MySQL database adapter for Python3
  DEPENDS:=+PACKAGE_python3-mysql:python3 +libmysqlclient
  VARIANT:=python3
endef

define Package/python-mysql/description
 MySQLdb is an thread-compatible interface to the popular MySQL database
 server that provides the Python database API.
endef

define Package/python3-mysql/description
$(call Package/python-mysql/description)
.
(Variant for Python3)
endef

$(eval $(call PyPackage,python-mysql))
$(eval $(call BuildPackage,python-mysql))

$(eval $(call Py3Package,python3-mysql))
$(eval $(call BuildPackage,python3-mysql))
