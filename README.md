# DH BOT 发行说明

DH BOT 当前采用个人发行方式：生产程序只在受控 Windows 开发机本地构建、扫描和实机验收，再通过管理员公布的云盘链接提供下载。

本仓库不运行 GitHub Actions，也不保存私有源码、Fixture、构建凭据、签名证书或原始旺商聊协议。这里仅作为可选下载说明与历史发行索引。

## 当前下载规则

每次分发至少包含：

- `DH-BOT-VERSION-windows-x64-portable.zip`
- `SHA256SUMS.txt`
- `DH-Manual-ZH.pdf`

当前个人发行产物未做 Authenticode 公共信任签名，Windows 首次启动可能显示“未知发布者”或 SmartScreen 提示。下载后请使用 PowerShell 核对 SHA-256：

```powershell
Get-FileHash .\DH-BOT-VERSION-windows-x64-portable.zip -Algorithm SHA256
```

结果应与管理员同时发布的 `SHA256SUMS.txt` 完全一致。

## 边界

- 源码仓库：`DH-devmax/d-hbot`，保持私有，Actions 停用。
- 本仓库：Actions 停用，不承担构建和签名。
- 生产版固定连接真实旺商聊 `127.0.0.1:9222`。
- Fixture、`9233/51300`、测试数据库和开发命令只存在于内部开发环境。
- 云盘包不包含源码、PDB、Source Map、PFX、私钥、Token、Cookie 或真实群数据。

以后若恢复 GitHub Release 或接入公共信任代码签名，将先更新本说明与发布规范，再建立新的发布流程。
