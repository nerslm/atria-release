# Atria server 发布仓库

[Atria](https://github.com/nerslm/atria)（手机远程 AI 编程 IDE）后端的发布包：
自带 node 运行时，含 web 前端、ptyhost 终端宿主、hubd 中控 agent。

## 安装 / 升级（幂等）

```bash
curl -fsSL https://github.com/nerslm/atria-release/releases/latest/download/install.sh | bash
```

- 安装到 `~/.atria`（`ATRIA_HOME` 可改），默认监听 `0.0.0.0:8790`（`ATRIA_PORT` 可改）
- 访问 token 在 `~/.atria/token`，升级不变
- 进程管理：`~/.atria/bin/atriad start|stop|restart|status|token|log <svc>`
- 开机自启：Linux 自动写 cron `@reboot`（`ATRIA_NO_AUTOSTART=1` 跳过）；
  systemd 单元模板在 `~/.atria/dist/current/deploy/`；macOS 需手动（launchd）
- 成功时最后一行输出 `{"port":8790,"token":"…","version":"x.y.z"}`
  （iOS App「SSH 自动部署」按此解析）

## 平台

| 资产 | 平台 |
|---|---|
| `atria-server-linux-x64.tar.gz` | Linux x86_64，glibc ≥ 2.39（Ubuntu 24.04+ / Debian 13+ / 同代 WSL2） |
| `atria-server-darwin-arm64.tar.gz` | macOS Apple Silicon |

源码与打包脚本在主仓库 `release/`；发版流程：`release/publish.sh`。
