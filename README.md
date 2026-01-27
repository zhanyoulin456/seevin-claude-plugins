# Seevin Claude 插件市场

Seevin 团队专属 Claude Code 插件集，提供企业级前端开发工具。

## 快速开始

### 1. 添加插件市场

```bash
/plugin marketplace add https://github.com/zhanyoulin456/seevin-claude-plugins.git
```

### 2. 安装核心插件（推荐）

```bash
/plugin install seevin-core
```

**立即获得**：

- ✨ 前端界面设计技能
- 🎨 LayerData 转换为 Vue 组件
- 📋 JSD 企业代码规范检查
- 🌐 Chrome DevTools 集成
- 📖 TDesign 组件库文档查询
- 📚 Context7 文档查询

**无需任何配置，安装即可使用！**

### 3. 安装 YAPI 工具（可选）

```bash
/plugin install seevin-yapi-tools
```

需要配置个人 YAPI 凭证，详见 [YAPI 配置指南](plugins/seevin-yapi-tools/README.md)。

## 插件列表

### seevin-core

**核心工具集** - 开箱即用

- **Skills**:
  - `frontend-design` - 创建高质量前端界面
  - `layerdata-to-code` - LayerData 转换为 Vue 组件
  - `skill-creator` - 创建新技能的指南

- **Commands**:
  - `jsd-auto-lint` - JSD 企业代码规范检查

- **MCP Servers**:
  - `chrome-devtools` - Chrome DevTools 集成
  - `context7` - 库文档查询（Upstash）
  - `tdesign-mcp-server` - TDesign 组件库工具

### seevin-yapi-tools

**YAPI 自动化工具** - 需配置

- **Commands**:
  - `gen-js-api-code` - 生成 JavaScript API 代码
  - `gen-ts-api-code` - 生成 TypeScript API 代码

- **MCP Servers**:
  - `yapi-get-interface-mcp` - YAPI 接口文档获取

## 配置指南

- [YAPI 工具配置](plugins/seevin-yapi-tools/README.md)
- [完整配置说明](CONFIGURATION.md)

## 常见问题

### Q: 如何配置 YAPI 工具？

A: 查看 [YAPI 配置指南](plugins/seevin-yapi-tools/README.md)

### Q: 插件更新后如何获取新版本？

A: 运行 `/plugin marketplace update` 更新市场，然后重新安装插件

### Q: 遇到问题如何反馈？

A: 联系 zhanyoulin456@163.com 或在 GitLab 提 issue

## License

MIT License - 详见 [LICENSE](LICENSE) 文件

## 团队

Seevin Frontend Team

---

**享受高效的开发体验！** 🚀
