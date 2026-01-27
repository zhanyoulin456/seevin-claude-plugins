# LayerData to Code - 详细参考

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

## 代码生成规则

1. 生成 HTML 结构
   - 基于图层名称创建元素标签
   - 保持层级关系 (父元素包含子元素)
2. 生成 CSS 样式
   - 转换绝对定位为相对定位
   - 应用 margin, padding, flex, grid 等布局属性
   - 保留原始 CSS 样式
3. 默认填充 layerData 的 content 字段,如果没有 content 则填充 name 字段

### 重要提醒

- 严格禁止使用任何绝对定位（position: absolute/fixed）,需要使用 flex，grid，流式布局
- 请使用 tailwind 工具类 + 变量的形式
- 计算 padding 时，需要添加 border-box 样式
- **严格使用**项目设计系统变量和工具类
- 禁止硬编码颜色、字体大小等（如果已有的设计系统不适用，才硬编码）
- 优先使用现有组件和工具类
- 保持与项目整体设计的一致性
- 减少重复样式，提高代码复用性
- 如果是图片使用空 img 对象占位，宽高使用 layer 的宽高,填充一个灰色背景
