# Release Guide

本文档面向维护者。

目标是：

- 只发布打包产物
- 不公开源码
- 通过 GitHub Releases 分发

## 仓库建议内容

公开仓库建议只保留：

- `README`
- 安装说明
- 发布说明
- 版本说明
- 截图

不要公开：

- 源码
- 本地登录态
- 构建缓存

## 发布产物

当前推荐上传到 GitHub Releases 的内容：

- macOS `.dmg`
- macOS `.zip`

## 发布前检查

1. 确认安装包来自最新构建
2. 确认应用可以启动
3. 确认 `curl http://127.0.0.1:8787/health` 正常
4. 确认局域网访问可用
5. 确认文档已经更新

## macOS 发布说明

当前 macOS 包是：

- 可启动
- 已做 ad-hoc 签名校验修复
- 没有 Apple Developer 官方签名

这意味着：

- 不应再表现为“应用已损坏”
- 但可能仍会被 Gatekeeper 以“无法验证开发者”拦截
- 用户需要右键打开或去系统设置放行

## Release 文案里必须写清楚

- 这是本地工具，不是云服务
- 用户必须登录自己的 ChatGPT 账号
- 当前版本是 `alpha`
- 默认监听 `0.0.0.0:8787`
- 同一局域网内可通过电脑 IP 调用
- 如果不需要局域网访问，应自行做网络限制

## 建议的 Release 标题

```text
v0.1.0-alpha
```

## 建议的 Release 说明结构

```text
What’s new
- First public alpha release
- Local desktop app
- Local and LAN API access

How to use
1. Install the app
2. Launch it
3. Log in with your own account
4. Call http://127.0.0.1:8787

Important notes
- Local tool only
- Your own account only
- macOS may ask you to manually allow first launch
- API listens on 0.0.0.0:8787 in the current alpha
```
