## V6.2 / 2.1.2

- 修复 `USE_DEVICE_AEC` 被误判成开发板/4G 选项的问题。
- 顶层开发板识别现在只接受 `BOARD_TYPE_*` / `BOARD_*`。
- 支持 SpotPear MAX35 的两级 menuconfig：先选择 MAX35 父板，再强制选择 ML307/4G 子变体，并关闭同组 Wi-Fi 变体。
- 预检同时验证 MAX35 父板和 ML307/4G 子变体，拒绝静默回退到 Wi-Fi。

# Changelog

## 2.1.1 — Fix GitHub Actions gdown environment

- 修复下载 SpotPear 源码阶段报 `/usr/bin/python: No module named gdown`。
- 下载步骤重新执行 ESP-IDF `export.sh`，确保调用安装了 `gdown` 的同一个 Python 虚拟环境。
- 下载前打印 Python 路径并执行 `python -m gdown --version`，环境不一致会立即失败并给出清晰日志。

## 2.1.0 — Fixed 4G backend

- 固定 OTA / 服务发现地址为 `http://124.221.112.55:8002/xiaozhi/ota/`。
- 不再使用 GitHub Actions Variable 选择 OTA 地址。
- 强制 `CONFIG_OTA_URL` 为上述地址；厂商源码若没有该 Kconfig 项则构建失败。
- 新增运行时 OTA 锁：`GetCheckVersionUrl()` 直接返回 `CONFIG_OTA_URL`，阻止 NVS / Wi-Fi 配网页面的旧 `ota_url` 覆盖固定地址。
- preflight 增加固定后台校验和运行时覆盖校验。
- 保留 SpotPear MAX35 ML307 4G、音频、协议栈和 STELLAR UI-only 架构。
