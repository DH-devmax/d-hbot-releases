# DH BOT 发行版

这里是 DH BOT 的公开发行仓库，仅存放经过生产隔离检查并完成 Authenticode 签名的 Windows 安装包、便携版、使用手册、规则模板和校验和。

DH BOT 的 Rust/Tauri 源码、旺商聊协议实现、内部 Fixture、原始契约和构建凭据保存在私有源码仓库 `DH-devmax/d-hbot`，不会进入本仓库。

## 下载与校验

从 [Releases](https://github.com/DH-devmax/d-hbot-releases/releases) 下载最新版本，并使用同一版本中的 `SHA256SUMS.txt` 校验文件完整性。

## 发布边界

私有源码仓库完成测试、Windows 构建、生产隔离扫描和签名后，通过只对本仓库有写权限的 Deploy Key 将产物投递到 `incoming/<版本>/`。本仓库的 GitHub Actions 会再次校验：

- 发布清单来源必须是 `DH-devmax/d-hbot`。
- 文件名不含子目录或路径穿越字符。
- 发行清单不含 Rust、TypeScript、Go、PDB、Source Map 或 Fixture。
- `SHA256SUMS.txt` 中的校验值全部匹配。

校验通过后 Actions 创建公开 Release，并删除仓库工作树中的临时投递目录。

本仓库不保存旺商聊账号、Cookie、Token、原始协议采集、AI 密钥、签名证书或开发 Fixture。
