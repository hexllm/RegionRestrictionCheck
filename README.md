# RegionRestrictionCheck

中文 | [English](README_EN.md)

流媒体及常见网络服务地区限制检测脚本。本仓库基于上游 [lmc999/RegionRestrictionCheck](https://github.com/lmc999/RegionRestrictionCheck) 演化并独立维护。

## 支持 OS

脚本内含以下环境的适配分支（按 `checkOS()` 检测包管理器）：

- Debian 系（`apt`）
- RedHat 系（`dnf` / `yum`）
- macOS（`brew`）
- Termux（`pkg`）

实际仅在 Debian 稳定版验证通过，其余环境未经完整测试；如运行出现问题，请自行检查并解决依赖。

## 使用方法

**使用脚本前请确认已安装 `curl`。**

默认运行：

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh)
```

仅检测 IPv4：

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -M 4
```

仅检测 IPv6：

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -M 6
```

指定出口网卡或 IP：

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -I eth0
```

## 参数

| 参数 | 说明 |
| ---- | ---- |
| `-I <Interface/IP>` | 指定测试使用的网卡或出口 IP（传给 curl `--interface`） |
| `-M <4/6>` | 指定仅测试 IPv4（`4`）或仅测试 IPv6（`6`） |
| `-E` | 使用英文输出 |
| `-X <IP>` | 在请求头中注入 `X-Forwarded-For` |
| `-P <Proxy>` | 指定测试使用的代理，支持协议请参考 curl `-x` |
| `-F <Function>` | 仅运行指定的检测函数 |
| `-S <Value>` | 特殊选项，目前仅识别 `force6`（强制输出被标记为 `IPv6 Not Support` 的条目） |
| `-R <IP>` | 将所有 HTTPS 域名（443 端口）解析到指定 IP（传给 curl `--resolve *:443:<IP>`） |
| `-C <Path>` | 指定使用的 `curl` 程序路径 |
| `-D <DNS>` | 指定使用的 DNS 服务器（需使用启用了 c-ares 的 `curl`，可配合 `-C` 参数指定） |
