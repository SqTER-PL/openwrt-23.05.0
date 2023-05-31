# 
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# makefile by SqTER

include $(TOPDIR)/rules.mk

PKG_NAME:=mc
PKG_VERSION:=4.8.28
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.midnight-commander.org/
PKG_HASH:=e994d9be9a7172e9ac4a4ad62107921f6aa312e668b056dfe5b8bcebbaf53803
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf gettext-version
PKG_BUILD_DEPENDS:=libtirpc

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/mc_full
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+glib2 +libncurses +libslang2 +libtirpc +libmount +libssh2 $(ICONV_DEPENDS) $(INTL_DEPENDS)
  TITLE:=midnight commander - Full Version by SqTER
  URL:=http://www.midnight-commander.org/
  SUBMENU:=filemanager
endef

define Package/mc_full/description
	GNU Midnight Commander is a text-mode full-screen file manager. 
	It uses a two panel interface and a subshell for command execution. 
	It includes an internal editor with syntax highlighting and an 
	internal viewer with support for binary files. Also included is 
	Virtual Filesystem (VFS), that allows files on remote systems 
	(e.g. FTP, SSH, SMB servers) and files inside archives to be 
	manipulated like real files.
endef

CONFIGURE_ARGS += \
	--with-homedir=/etc/mc \
	--enable-utf8 \
	--without-gpm-mouse \
	--without-x \
	--disable-glibtest \
	--disable-doxygen-doc \
	--disable-nls \
	--disable-tests \
	--with-libintl-prefix="$(INTL_PREFIX)" \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-slang-includes="$(STAGING_DIR)/usr/include" \
	--with-slang-libs="$(STAGING_DIR)/usr/lib" \
	fu_cv_sys_stat_statfs2_bsize=yes

CONFIGURE_VARS += \
	ac_cv_search_addwstr=no \

TARGET_CPPFLAGS += -I$(STAGING_DIR)/usr/include/tirpc

define Package/mc_full/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mc $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/mc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/mc.charsets $(1)/etc/mc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/mc.ext $(1)/etc/mc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/mc.default.keymap $(1)/etc/mc/mc.keymap
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/filehighlight.ini $(1)/etc/mc
	$(INSTALL_DIR) $(1)/usr/share/mc/help
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/doc/hlp/mc.hlp $(1)/usr/share/mc/help
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/mc.menu $(1)/etc/mc
	$(INSTALL_DIR) $(1)/etc/mc/skins
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/misc/skins/default.ini $(1)/etc/mc/skins
	$(INSTALL_DIR) $(1)/usr/share/mc/syntax
	touch $(1)/usr/share/mc/syntax/Syntax
	ln -sf mc $(1)/usr/bin/mcdiff
	ln -sf mc $(1)/usr/bin/mcedit
	ln -sf mc $(1)/usr/bin/mcview
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/vfs/sfs/sfs.ini $(1)/etc/mc
	$(INSTALL_DIR) $(1)/usr/lib/mc/extfs.d
endef


define Package/mc/conffiles
/etc/mc/mc.menu
/etc/mc/skins/default.ini
endef

$(eval $(call BuildPackage,mc_full))
