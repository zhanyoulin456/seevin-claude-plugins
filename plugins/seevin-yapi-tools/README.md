# Seevin YAPI 工具配置指南

本插件提供 YAPI 接口文档自动获取和代码生成功能。

## 前置要求

- 拥有 Seevin YAPI 账户
- 已安装 Node.js 和 npx

## 配置方法

### 方法 1：环境变量（推荐）

编辑您的 shell 配置文件（`~/.zshrc` 或 `~/.bashrc`）：

```bash
# YAPI 配置
export YAPI_EMAIL="your-email@seevin.com"
export YAPI_PASSWORD="your-password"
export YAPI_URL="http://api.seevin.com/"
```

重启终端或执行：

```bash
source ~/.zshrc
```

### 方法 2：本地配置文件

如果不想使用环境变量，可以创建本地配置文件：

```bash
cd ~/.claude/plugins/marketplaces/seevin-claude-plugins/plugins/seevin-yapi-tools
配置.mcp.json
# 编辑 .mcp.json 填入您的凭证
```

## 使用方法

### 生成 JavaScript API 代码

```bash
/gen-js-api-code [yapi-url] [api-path]
```

### 生成 TypeScript API 代码

```bash
/gen-ts-api-code [yapi-url] [api-path] [type-path]
```

## 故障排除

### YAPI 连接失败

1. 检查环境变量是否正确设置：`echo $YAPI_EMAIL`
2. 确认 YAPI 服务器地址可访问
3. 验证邮箱和密码是否正确

### 命令无法使用

确保已安装插件并配置了 MCP 服务器。
