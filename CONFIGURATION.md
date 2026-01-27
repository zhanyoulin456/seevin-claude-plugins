# Seevin 插件配置指南

## seevin-yapi-tools 配置

本插件需要配置 YAPI 个人凭证才能使用。

### 环境变量配置（推荐）

**步骤 1**: 编辑 shell 配置文件

```bash
nano ~/.zshrc  # 或 ~/.bashrc
```

**步骤 2**: 添加以下内容

```bash
# YAPI 配置 - Seevin 团队
export YAPI_EMAIL="your-email@seevin.com"
export YAPI_PASSWORD="your-password"
export YAPI_URL="http://api.seevin.com/"
```

**步骤 3**: 保存并重启终端

```bash
source ~/.zshrc
```

**步骤 4**: 验证配置

```bash
echo $YAPI_EMAIL
# 应该显示您的邮箱地址
```

### 使用本地配置文件（备选方案）

如果不使用环境变量：

```bash
cd ~/.claude/plugins/marketplaces/seevin-claude-plugins/plugins/seevin-yapi-tools
cp .mcp.json.template .mcp.json
nano .mcp.json  # 填入您的凭证
```

## 安全提醒

⚠️ **重要**：

1. 切勿将个人凭证提交到 Git 仓库
2. `.mcp.json` 已加入 .gitignore
3. 定期更新密码以确保安全

## 验证安装

测试 YAPI 工具是否正常工作：

```bash
/gen-js-api-code http://api.seevin.com/ /api/path
```

如果成功生成代码，说明配置正确。

## 获取帮助

- 配置问题：zhanyoulin456@163.com
- YAPI 账户问题：联系团队管理员
