### 搭建3x-ui服务，自带warp功能无需另外安装

```markdown
# 3X-UI 安装与配置指南

3X-UI 是基于 Xray 的多协议、多用户管理面板，支持 Vmess、Vless、Trojan、ShadowSocks 和 WireGuard 等多种协议，并且内置 WARP 功能。

## 准备工作

1. **域名**：3X-UI 支持 SSL 证书申请和域名绑定。
2. **VPS 服务器**：确保有可用的 VPS，并在防火墙中开放对应的端口。

## 安装 3X-UI

### 一键安装脚本
在 VPS 上运行以下命令安装 3X-UI 面板：

```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

安装过程中会提示输入端口号，并生成一个随机的根路径，例如：`111.123.23.33:9000/156dfhfgh`。安装完成后会生成一个随机的账号和密码。

### 登录面板
使用 `服务器地址 + 端口号 + 根路径` 组合访问面板，并使用生成的账号密码登录。

### 修改面板设置
登录后可以在 `面板设置 -> 安全设定` 中更改账号密码和根路径。

## 安装 SSL 证书

在安装过程中，可以选择申请 SSL 证书：

1. 运行 `x-ui` 命令。
2. 选择 `18 SSL Certificate Management`。
3. 选择 `1 Get SSL` 并输入解析好的域名。
4. 按提示选择端口（默认 80），等待证书申请完成。
5. 完成后，选择 `y` 将证书应用于面板。

## 启用 BBR 加速

在 VPS 上运行以下命令以启用 BBR 加速：

```bash
x-ui
```

选择 `23 Enable BBR`，然后退出。

## 添加入站规则

1. 在面板的入站列表中，点击 `添加入站`。
2. 选择协议（通常选择 VLESS 或 VMESS），传输选择 WebSocket。
3. 设置路径（路径不可重复），如 `/stepn`。
4. 在安全设置中选择 TLS，清空 ALPN 字段内容。
5. 设置证书并保存。

## 配置 WARP 路由

1. 在 `Xray 设置 -> 基本路由` 中，启用 WARP。
2. 在 WARP 输入框中添加需要通过 WARP 路由的域名，例如 `openai` 和 `netflix`。
3. 使用正则表达式匹配特定关键词，如 `regexp:.*disney.*`，表示包含 `disney` 的流量将通过 WARP 路由。

## 参考

- GitHub 项目地址: [https://github.com/MHSanaei/3x-ui](https://github.com/MHSanaei/3x-ui)
```

该版本对流程进行了优化，并按照 GitHub README 的格式排版，便于理解和操作。希望这份更详细的说明能帮助到您。
