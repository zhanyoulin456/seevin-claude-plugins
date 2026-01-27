# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是 Seevin 团队的 Claude Code 插件市场，提供企业级前端开发工具集。项目采用模块化插件架构，包含两个核心插件：

- **seevin-core**: 核心工具集，开箱即用
- **seevin-yapi-tools**: YAPI 自动化工具，需配置个人凭证

## 插件架构

### 插件市场配置

`.claude-plugin/marketplace.json` 定义了整个插件市场的元数据：

- 插件市场信息（name, description, owner, homepage）
- 插件列表及其源码路径：`source: ./plugins/插件目录`

每个插件的详细元数据由其 `plugin.json` 定义，strict 模式下会自动合并。

### 插件目录结构

每个插件遵循统一的结构：

```
plugins/插件名/
├── .claude-plugin/
│   └── plugin.json          # 插件元数据（包含路径配置）
├── commands/                # 命令文件（.md）
│   └── command-name.md
├── skills/                  # 技能目录
│   └── skill-name/
│       ├── SKILL.md         # 必需：技能定义
│       ├── LICENSE.txt      # 可选：许可证
│       └── references/      # 可选：参考资料
└── .mcp.json               # MCP 服务器配置
```

**plugin.json** 包含：

- **基本信息**：name, description, version, author, license
- **分类信息**：category, tags
- **路径配置**：mcpServers, commands, skills, homepage
- 这些配置使插件自包含，成为单一事实来源

### 技能（Skills）文件格式

**SKILL.md** - 技能定义文件，使用 frontmatter 格式：

```markdown
---
name: skill-name
description: 触发条件描述，用于匹配用户请求
license: Complete terms in LICENSE.txt
---

# 技能标题

技能详细说明和执行指南...
```

技能采用三级加载系统管理上下文，避免一次性加载过多内容。

### 命令（Commands）文件格式

命令文件使用 frontmatter 定义元数据：

```markdown
---
description: 命令描述
argument-hint: [参数提示]
---

# 命令标题

执行步骤说明...
```

命令通过斜杠命令调用，例如：`/jsd-auto-lint`

### MCP 服务器配置

**`.mcp.json`** 定义 MCP 服务器集成：

```json
{
  "mcpServers": {
    "服务器名称": {
      "type": "stdio",
      "command": "npx",
      "args": ["包名", "--参数", "值"]
    }
  }
}
```

已集成的 MCP 服务器：

- `chrome-devtools`: Chrome DevTools 集成
- `context7`: 库文档查询（Upstash）
- `tdesign-mcp-server`: TDesign 组件库工具
- `yapi-get-interface-mcp`: YAPI 接口文档获取

## 核心技能说明

### frontend-design

创建高质量前端界面，避免通用 AI 美学。关键原则：

- 选择独特的设计方向并坚持执行
- 使用独特的字体（避免 Inter、Roboto 等常见字体）
- 采用大胆的配色方案和主题
- 通过动画和微交互增强体验
- 创造意外的布局和空间构成

### layerdata-to-code

将设计工具的 layerDatas 转换为 Vue 组件代码。参考文件：

- `ASCII.md`: ASCII 艺术字符参考
- `examples.md`: 代码示例
- `reference.md`: 技术参考

### jsd-auto-lint

JSD 企业通用代码规范检查命令：

- 分析当前分支或指定分支的代码修改
- 检查命名规范、路由映射、编码风格
- 生成 `.code-lint-report.md` 报告
- 包含具体问题描述和解决方案

## 配置管理

### YAPI 工具配置

seevin-yapi-tools 插件需要配置个人 YAPI 凭证：

**推荐方式：环境变量**

```bash
export YAPI_EMAIL="your-email@seevin.com"
export YAPI_PASSWORD="your-password"
export YAPI_URL="http://api.seevin.com/"
```

添加到 `~/.zshrc` 或 `~/.bashrc` 中持久化。

**备选方式：本地配置文件**

```bash
cd ~/.claude/plugins/marketplaces/seevin-claude-plugins/plugins/seevin-yapi-tools
配置 .mcp.json
# 编辑 .mcp.json 填入凭证
```

⚠️ **安全提醒**：

- `.mcp.json` 已加入 `.gitignore`
- 切勿将个人凭证提交到 Git 仓库
- 定期更新密码

## 插件安装与使用

### 添加插件市场

```bash
/plugin marketplace add https://github.com/zhanyoulin456/seevin-claude-plugins.git
```

### 安装插件

```bash
# 核心工具集（推荐）
/plugin install seevin-core

# YAPI 工具（需配置）
/plugin install seevin-yapi-tools
```

### 更新插件

```bash
/plugin marketplace update
```

## 开发指南

### 创建新技能

使用 `skill-creator` 技能作为指南，包含：

- 脚本工具：`scripts/init_skill.py`, `scripts/package_skill.py`
- 参考文档：`references/workflows.md`, `references/output-patterns.md`

### 创建新命令

在插件的 `commands/` 目录创建 `.md` 文件，使用 frontmatter 定义元数据。

### 添加 MCP 服务器

在插件的 `.mcp.json` 中添加服务器配置。参考现有 MCP 服务器的配置格式。

## 企业代码规范

JSD 企业通用规范要点：

**命名规范**

- 目录：全小写，中划线连接，集合类使用复数
- 文件：小写中划线（`user-list.vue`）
- 公共组件：复杂组件用大驼峰文件夹 + index.vue，简单组件用小写中划线

**路由映射**

- 路由 path 必须与 `src/views` 目录结构一致
- 必须使用动态导入：`() => import()`

**编码风格**

- HTML/Vue：2 空格缩进，语义化标签，大驼峰组件名，双引号属性值
- CSS：使用 scss/less，不超过三层嵌套，优先使用 CSS 变量
- JavaScript：单引号，小驼峰命名，卫语句优先
- TypeScript：避免 any，接口不用 I 前缀，类型定义在顶部

完整规范参见 `jsd-auto-lint` 命令文档。

## 团队联系

- 技术支持：zhanyoulin456@163.com
- GitHub：https://github.com/zhanyoulin456/seevin-claude-plugins
