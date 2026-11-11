# kodi-prebuilt

XGPV3（RK3568，iStoreOS/OpenWrt 24.10）用的 **Kodi 20.5 预编译包**。

## 为什么是预编译

24.10 的 packages 源里没有 kodi。这里从 iStoreOS 22.03 设备上抽出整棵 Kodi 树（`/usr/lib/kodi`、`/usr/share/kodi`、init/uci），
并把 `kodi-gbm` 的 **62 个依赖库**（openssl 1.1 / ffmpeg 59 / python3.10 / GLES / libass / libcdio 等）一并打进
`/usr/lib/kodi-compat`，用 wrapper 设 `LD_LIBRARY_PATH` 启动，避免与 24.10 的 openssl3/ffmpeg7 冲突。

产物体积约 326 MB（解压后），压缩包 209 MB，放在 Release 资产里而不是仓库文件里。

## 已知风险

- 22.03 的二进制在 24.10 上属于**跨版本搬运**，musl ABI 稳定但 libstdc++/内核接口未必完全兼容，需刷机实测
- 包里自带库和系统库各一份，磁盘占用较大
- 首次启动会走 `firstboot.sh`/`preseed.sh`（依赖 python3，已加依赖）

## 使用

```
src-git kodi_prebuilt https://github.com/guangay/kodi-prebuilt.git;main
```

```
CONFIG_PACKAGE_kodi=y
```