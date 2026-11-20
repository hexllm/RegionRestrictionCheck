# RegionRestrictionCheck

[中文](README.md) | English

A Bash script for checking regional restrictions of streaming media and common online services. This repository evolved from upstream [lmc999/RegionRestrictionCheck](https://github.com/lmc999/RegionRestrictionCheck) and is maintained independently.

## Supported OS

The script includes compatibility branches for the following environments (detected by package manager in `checkOS()`):

- Debian-based Linux (`apt`)
- RedHat-based Linux (`dnf` / `yum`)
- macOS (`brew`)
- Termux (`pkg`)

In practice, only Debian Stable has been verified; other environments have not been fully tested. If you encounter issues, please check and resolve dependencies manually.

## Usage

**Make sure `curl` is installed before running the script.**

General use:

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -E
```

Test IPv4 only:

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -E -M 4
```

Test IPv6 only:

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -E -M 6
```

Specify a network interface or source IP:

```bash
bash <(curl -L -s https://raw.githubusercontent.com/hexllm/RegionRestrictionCheck/main/check.sh) -E -I eth0
```

## Options

| Flag | Description |
| ---- | ----------- |
| `-I <Interface/IP>` | Specify the network interface or source IP address (passed to curl `--interface`) |
| `-M <4/6>` | Test IPv4 (`4`) or IPv6 (`6`) only |
| `-E` | Output in English |
| `-X <IP>` | Inject an `X-Forwarded-For` request header |
| `-P <Proxy>` | Specify a proxy for testing; see curl `-x` for supported protocols |
| `-F <Function>` | Run only the specified check function |
| `-S <Value>` | Special option; currently only recognizes `force6` (forces printing entries marked as `IPv6 Not Support`) |
| `-R <IP>` | Resolve all HTTPS domains (port 443) to the specified IP (passed to curl `--resolve *:443:<IP>`) |
| `-C <Path>` | Specify the path to the `curl` binary |
| `-D <DNS>` | Specify custom DNS server(s) (requires a `curl` build with c-ares support; use with `-C` if needed) |
