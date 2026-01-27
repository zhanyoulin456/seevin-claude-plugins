---
name: layerdata-to-code
description: '将 layerDatas 图层数据转换为 Vue 组件代码 (HTML + CSS)。当用户提示词中包含 layerDatas 时调用'
---

# LayerData to Code

将 UI 设计工具导出的 layerDatas 图层数据转换为 HTML/CSS 页面代码。按照下面的步骤进行

1. 从项目的 `DESIGN.md` 文件中获取设计系统变量（颜色、字体、间距等）和规范
2. 分析 layerDatas 数据结构
3. 生成 HTML 结构和 CSS 样式
4. 确保符合当前项目的设计系统规范
5. 添加到用户指定的位置

## Requirements

- 需要从项目的 `DESIGN.md` 项目规则中获取设计系统变量（颜色、字体、间距等）,是否使用 tailwind css,scss 等
- 如果当前项目的`DESIGN.md` 不存在,或者没有提到设计系统,则暂停,并提示用户添加设计系统信息到 `DESIGN.md` 文件中
- 严格遵循`DESIGN.md`中的代码规范

## Quick Start

### 1. 获取项目的设计系统

- 从项目的 `DESIGN.md` 文件中获取设计系统,（颜色、间距等变量）和规范
- 如果当前项目的`DESIGN.md` 不存在,或者没有提到设计系统,以及不完整的情况下则取消操作,并提示用户添加设计系统信息到 `DESIGN.md` 中
- 严格遵循`DESIGN.md`中的代码规范

需要从 `DESIGN.md` 文件中获取的设计系统变量包括:

- 颜色变量,包括主题色,文本色,背景色,边框色等 css 变量
- 是否使用 tailwind css,scss,less 等 css 框架
- 使用的组件库

### 2. 分析数据结构

解析并理解 layerDatas 的结构化内容。

## 数据结构

### layerData 示例

```json
{
  "type": "shape",
  "name": "矩形 788",
  "x": 1362,
  "y": 102,
  "width": 100,
  "height": 64,
  "css": ["width: 100px;", "height: 64px;", "background: #fff;"],
  "layerIndex": 76
}
```

### 字段说明

| 字段              | 说明                                        |
| ----------------- | ------------------------------------------- |
| `type`            | 图层类型 (group/shape/text/Ellipse/Line)    |
| `content`         | 图层内容                                    |
| `name`            | 图层名称,如果 content 为空,则使用 name 字段 |
| `x`, `y`          | 绝对定位坐标                                |
| `width`, `height` | 元素尺寸                                    |
| `css`             | 原始 CSS 样式数组                           |
| `layerIndex`      | 图层索引                                    |

### 布局转换原理

**原始数据**: 基于绝对定位 (x, y, width, height)

**目标代码**: 使用标准 CSS 布局 (margin, padding, flex, grid 等)

转换时需要:

- 识别图层间的父子/兄弟关系
- 选择合适的布局方案 (flex/grid/block)
- 将原始的 x, y, width, height 绝对定位转换为 css 中的相对定位 (使用 margin, padding, flex, grid 等布局样式),禁止使用 position: absolute/fixed
- 从 layer.css 中提取原始 css 样式,并应用到生成的代码中

### 2. 生成页面代码

根据草图和结构化数据生成 HTML/CSS 代码。

## 代码生成规则

1. 生成 HTML 结构
   - 基于图层名称创建元素标签
   - 保持层级关系 (父元素包含子元素)
2. 生成 CSS 样式
   - 保留原始 CSS 样式
   - 转换绝对定位为相对定位
   - 应用 margin, padding, flex, grid,block,盒子模型等布局特性
   - 默认值不声明,比如`font-weight: 400;`,这是默认值,不需要声明即可生效
3. 默认填充 layerData 的 content 字段,如果没有 content 则填充 name 字段

## 重要提醒

- layerData 中的`x`,`y`,`width`和`height`,在转换时,只能作为布局参考,不可直接作为 CSS 样式的属性值,切记不要直接引用
- 如果是 tailwind 工具类,全部使用 px 单位语法,例如: `w-[100px]`
- 严格禁止使用任何绝对定位（position: absolute/fixed）,需要使用 flex，grid，block 流式布局
- 计算 padding 时，需要添加 border-box 声明使用的盒子模型
- **严格使用**项目设计系统,保持与项目整体设计的一致性,减少重复样式，提高代码复用性
- 如果是图片使用一个空 img 对象占位，宽高使用 layer 的宽高,填充一个灰色背景
  示例:
  ```html
  <div class="w-[100px] h-[64px] ">
    <img src="" alt="" class="bg-[#f5f5f5]" />
  </div>
  ```
- 禁止硬编码颜色、字体大小等（如果已有的设计系统不适用，才硬编码,并且生成完毕后,需要向 user 报告硬编码的内容）
- 如果项目中同时存在多个 css 框架,比如 tailwind,less,scss 等,优先只使用 tailwind
  比如同时存在 tailwind 和 scss,则只使用 tailwind,不使用 scss,也就是有 tailwind 就只使用 tailwind 的语法,不使用其他 css 框架的语法
