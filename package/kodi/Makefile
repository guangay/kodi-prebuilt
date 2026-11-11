include $(TOPDIR)/rules.mk

# XGPV3: Kodi 20.5 prebuilt tree extracted from iStoreOS 22.03 (aarch64, musl),
# with its own library closure under /usr/lib/kodi-compat.

PKG_NAME:=kodi
PKG_VERSION:=20.5
PKG_RELEASE:=1
PKG_SOURCE:=kodi-prebuilt-20.5.tar.gz
PKG_SOURCE_URL:=https://github.com/guangay/kodi-prebuilt/releases/download/prebuilt-20.5-r2/
PKG_HASH:=ed2bef3d68f619c85adf963f32ceac9dfe8c0ef51a9917bd0780e6e208a2f5ac
PKG_LICENSE:=GPL-2.0-or-later
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/kodi
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Kodi 20.5 (prebuilt, aarch64, bundled libs)
  DEPENDS:=+libc +libgcc +alsa-lib +libdrm +libinput +python3-light
endef

define Package/kodi/description
  Kodi 20.5 media center (prebuilt). Ships kodi-gbm, /usr/share/kodi,
  /usr/lib/kodi helper scripts, init script and uci config, plus the
  dependency closure in /usr/lib/kodi-compat (openssl 1.1, ffmpeg 59,
  python 3.10, GLES...) so it does not clash with 24.10 system libs.
endef

define Package/kodi/conffiles
/etc/config/kodi
endef

define Build/Compile
endef

define Package/kodi/install
	$(INSTALL_DIR) $(1)/usr $(1)/etc
	$(CP) $(PKG_BUILD_DIR)/usr $(1)/
	$(CP) $(PKG_BUILD_DIR)/etc $(1)/
	$(INSTALL_DIR) $(1)/usr/lib/kodi
	mv $(1)/usr/lib/kodi/kodi-gbm $(1)/usr/lib/kodi/kodi-gbm.real
	printf '#!/bin/sh\nexport LD_LIBRARY_PATH=/usr/lib/kodi-compat:$$LD_LIBRARY_PATH\nexec /usr/lib/kodi/kodi-gbm.real "$$@"\n' > $(1)/usr/lib/kodi/kodi-gbm
	chmod 0755 $(1)/usr/lib/kodi/kodi-gbm
endef

$(eval $(call BuildPackage,kodi))