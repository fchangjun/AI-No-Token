# AI-No-Token

Turn logged-in AI web apps into local API endpoints.

`AI-No-Token` 是一个本地桌面工具。它会在你的电脑上启动本地 API，复用你已经登录的 AI 网页会话，并把网页能力转成可调用的本地接口。

当前公开仓库用于：

- 提供安装包下载入口
- 提供安装和使用说明
- 记录发布版本和已知限制

当前公开仓库不包含源码。

## 当前状态

- 阶段：`alpha`
- 当前主要支持：macOS Apple Silicon
- 发布方式：GitHub Releases

下载入口：

- [Releases](https://github.com/fchangjun/AI-No-Token/releases)

## 它能做什么

- 启动一个本地桌面应用
- 管理网页登录态
- 在本机暴露 HTTP API
- 把 Web 端 AI 能力转成可调用接口

## 它不适合什么

- 公网稳定商用服务
- 多租户共享账号场景
- 依赖长期稳定网页接口的生产环境

## 快速开始

1. 从 [Releases](https://github.com/fchangjun/AI-No-Token/releases) 下载最新 macOS 安装包
2. 安装并启动桌面应用
3. 在应用内登录你自己的 ChatGPT 账号
4. 捕获登录态
5. 通过本地或局域网 HTTP API 调用

首次启动如果 macOS 拦截，请看 [macOS 安装说明](./docs/install-macos.md)。

## API 地址

默认端口：

```text
8787
```

桌面版默认会监听：

```text
0.0.0.0:8787
```

这意味着：

- 本机可以通过 `http://127.0.0.1:8787` 访问
- 同一局域网内也可以通过你的电脑 IP 访问

例如：

```text
http://127.0.0.1:8787
http://192.168.x.x:8787
```

## 调用示例

健康检查：

```bash
curl http://127.0.0.1:8787/health
```

聊天接口：

```bash
curl -X POST http://127.0.0.1:8787/api/chat \
  -H "Content-Type: application/json" \
  -d '{
    "sessionId": "desktop-demo",
    "mode": "auto",
    "prompt": "你好，请介绍一下 Node.js"
  }'
```

OpenAI 风格接口：

```bash
curl -X POST http://127.0.0.1:8787/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "sessionId": "desktop-demo",
    "model": "gpt-4",
    "messages": [
      {"role": "user", "content": "你好，请介绍一下 Electron"}
    ]
  }'
```

## 使用要求

- 使用你自己的账号登录
- 在本机运行桌面应用
- 接受网页接口可能变化

## 安全提醒

- 这是本地工具，不是云服务
- 当前 API 默认监听 `0.0.0.0:8787`
- 如果你不希望局域网其他设备访问，请限制本机网络环境或通过防火墙控制
- 网页接口可能触发验证码、风控或登录失效

## 安装与发布文档

- [macOS 安装说明](./docs/install-macos.md)
- [维护者发布说明](./docs/release-guide.md)

## 已知限制

- 当前公开发布重点是 macOS Apple Silicon
- 由于没有 Apple 开发者签名，首次打开可能需要手动放行
- 部分请求可能因为网页风控回退到 DOM 模式

## 一句话说明

`AI-No-Token` 的重点不是“免费调用 AI”，而是：

**把已登录的 Web AI 会话转成本地可调用的 API 网关。**
