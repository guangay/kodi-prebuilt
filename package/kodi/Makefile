include $(TOPDIR)/rules.mk

# XGPV3：从 iStoreOS 22.03 抽出的 Kodi 20.5 预编译树（aarch64 + 自带库闭包）。
# 二进制为 musl 构建，配合 /usr/lib/kodi-compat 里的 62 个依赖库运行。

PKG_NAME:=kodi
PKG_VERSION:=20.5
PKG_RELEASE:=1
PKG_SOURCE:=kodi-prebuilt-20.5.tar.gz
PKG_SOURCE_URL:=https://github.com/guangay/kodi-prebuilt/releases/download/prebuilt-20.5/
PKG_HASH:=faafd35b1a7cfe7b8bd620fcc7433428b3188ca6b6971072e749e87502e0c797
PKG_LICENSE:=GPL-2.0-or-later
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/kodi
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Kodi 20.5 (prebuilt, aarch64, bundled libs)
  DEPENDS:=+libc +libgcc1 +alsa-lib +libdrm +libinput +libstdcpp6 +python3-light
endef

define Package/kodi/description
  Kodi 20.5 媒体中心（预编译）。包含 kodi-gbm 二进制、/usr/share/kodi 资源树、
  /usr/lib/kodi 脚本、init 脚本与 uci 配置，以及 /usr/lib/kodi-compat 下的依赖库闭包
  （openssl1.1/ffmpeg59/python3.10/GLES 等，避免与 24.10 系统库冲突）。
endef

define Package/kodi/conffiles
/etc/config/kodi
endef

define Build/Compile
endef

define Package/kodi/install
	$(CP) $(PKG_BUILD_DIR)/. $(1)/
	$(INSTALL_DIR) $(1)/usr/lib/kodi
	mv $(1)/usr/lib/kodi/kodi-gbm $(1)/usr/lib/kodi/kodi-gbm.real
	printf '#!/bin/sh\nexport LD_LIBRARY_PATH=/usr/lib/kodi-compat:\$\\nexec /usr/lib/kodi/kodi-gbm.real \"\$\$\@\"\n' > $(1)/usr/lib/kodi/kodi-gbm
	chmod 0755 $(1)/usr/lib/kodi/kodi-gbm
endef

$(eval $(call BuildPackage,kodi))