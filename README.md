# DH BOT 发行版

这里是 DH BOT 的唯一生产构建与公开发行仓库，仅存放生产 workflow、经过生产隔离检查并完成 Authenticode 签名的 Windows 安装包、便携版、使用手册、规则模板和校验和。

DH BOT 的 Rust/Tauri 源码、旺商聊协议实现、内部 Fixture、原始契约和构建凭据保存在私有源码仓库 `DH-devmax/d-hbot`，不会进入本仓库。

## 下载与校验

从 [Releases](https://github.com/DH-devmax/d-hbot-releases/releases) 下载最新版本，并使用同一版本中的 `SHA256SUMS.txt` 校验文件完整性。

## 生产构建

私有源码仓库不运行 GitHub Actions。开发者先在本地完成生产、Fixture、界面和 Windows 实机预检，再由管理员在本仓库手动运行 `Build DH BOT production`：

- `source_commit` 必须是私有源码仓库中完整的 40 位 commit SHA。
- `release_tag` 必须与应用版本一致，且不能覆盖既有标签或 Release。
- workflow 使用最小权限只读 Token 检出精确提交，在 Windows Hosted Runner 上构建 `--no-default-features` 生产版。
- 主程序和安装包必须完成 Authenticode 签名、`signtool verify`、NSIS/portable 深度扫描和 SHA-256 清单。
- 缺少只读 Token、签名证书或任一门禁失败时不创建公开 Release。

workflow 只允许管理员手动触发，不响应 push、pull request、fork 或私有源码仓库事件。构建结束后 Runner 工作区自动销毁，私有源码不会提交到本仓库或上传为 Release 资产。

本仓库不保存旺商聊账号、Cookie、原始协议采集、AI 密钥、签名证书明文或开发 Fixture。源码只读 Token 与签名材料只存放在 GitHub Actions Secrets 中，且不会输出到日志。
