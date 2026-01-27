---
description: 根据企业规范发现项目问题
argument-hint: [branch name]
---

# 执行步骤

1. 如果用户没有提供上下文,则默认获取当前分支修改的文件,否则按照用户提供的：$ARGUMENTS参数进行处理，只处理当前分支的所有改动代码
2. 检查第一步获取的所有文件是否符合jsd - 企业通用规范,具体规则查看下方，但是不要吹毛求疵
3. 生成一份报告到项目根目录.code-lint-report.md,查看下方的末班
4. 这份报告是给开发者查看的,同时需要作为下一步让agent修复的参考

---

# code-lint-report 模板

## 问题1

文件名:[filename]

路径:[path]([line-start]-[line-end])

违反规则:[rule-name]

问题简述:[problem-short-desc]

问题代码摘录:
[problem-code]

解决方案:[solution]

## 问题2

.......

## 总结

[summary]

---

# jsd - 企业通用规范

## 1. 基本命名规范

### 目录命名

● 规范：全小写，多单词以中划线连接。集合类文件夹采用复数命名。

● 示例： components, views, utils, user-manage

### 文件命名

● 通用文件： 小写字母 + 中划线（detail.vue,index.js, user-auth.ts, company.png）

● Vue单文件： 业务页面用小写中划线（user-list.vue）

● 公共组件：项目级或模块级均需管理在 src/components文件夹中，对于复杂度高的组件目录下采用大驼峰文件夹形式，内建 index.vue，复杂度低的组件可直接components/PageTitle.vue

示例：

- 1. 在src/components文件夹
  - 1.1 复杂组件：采用大驼峰文件夹形式，内建 index.vue(src/components/ComplexComponent/index.vue)
  - 1.2 简单组件：直接在components文件夹下，文件名采用小写中划线形式（components/PageTitle.vue）

- 2. 在src/views文件夹
  - 2.1 业务页面：采用小写中划线形式（src/views/page/user-list.vue）

## 2. 路由与页面映射

在vue项目中为了实现“路径即代码”的可维护性，建立以下强约束：

● 映射规则： 路由 path 必须与 src/views 目录下的文件层级完全一致

● 地址 /user/order-list --> 对应文件 src/views/user/order-list/index.vue

● 懒加载： 所有路由定义必须使用 () => import() 动态导入

## 2.编码规范

### 2.1 HTML & Vue Template

● 缩进： 统一使用 2个空格。

● 语义化： 优先使用 nav, main, section 等标签，避免“满屏 div”

● 组件引用： 自定义组件使用大驼峰 <PageTitle />，强制 自闭合

● 属性值： 必须使用双引号包裹

● 注释： <!-- start -->表示模块开始<!-- end -->表示模块结束

● CSS选择器：使用单词字母小写，多个单词组成时，采用中划线-分隔，符合BEM/Vue官方风格，

● Vue SFC 推荐 scoped 或 CSS Modules，减少命名冲突

### 2.2 CSS 规范

● 预处理器： 使用 scss/less

● 层级嵌套： 原则上 不得超过三层

● 变量管理： 颜色、字号尽量使用全局定义的css变量,避免直接定义颜色值

● 原子化： 鼓励使用 tailwind.css 处理布局与间距，减少无意义的类名

● 禁止随意在项目中增加全局样式

● 避免编写行类样式（内联样式）

● 避免使用标签名、直接子选择器

● 省略 0 后面的单位

● 合理使用scss的特性进行代码优化

2.3 Javascript 规范

● 统一使用单引号（''）

● 变量使用camelCase 方式命名，尽可能使用完整的单词拼写命名，不要嫌单词长

● 方法名、参数名、局部变量都统一使用小驼峰 lowerCamelCase 风格，方法应当使用常用的add、update、delete、get、handle等作为前缀连接处理的对象进行命名

● 提炼函数：当一个函数内代码量过大时，需抽离函数

● 遵循卫语句优先原则

● 把复杂的条件分支语句提炼成函数

● 三目运算符不能嵌套过深（两层是可以接受的程度）

● 合理使用循环语句，提升代码质量，避免出现死循环

● 使用传递对象参数代替过长的参数列表，尽量减少参数数量

● 对于数字类型需采用统一的小数位处理方法进行输入控制

● 参与数值计算的变量必须强制进行类型判断以及转换，为了防止精度丢，应该再使用big.js的方法来处理数值计算

2.4 Typescript 规范

● 禁止大面积地使用any类型；

● 类本身使用大驼峰 PascalCase 方式命名，类成员使用 camelCase 方式命名；

● 接口本身使用大驼峰 PascalCase 方式命名，不要在接口名前加I。接口成员使用小驼峰 camelCase 方式命名；

● 枚举对象本身使用大驼峰 PascalCase 方式命名，枚举成员使用小驼峰 camelCase 方式命名

● 类型声明应尽量依靠 TS 的自动类型推断功能，如果能够推断出正确类型尽量不要再手动声明

● 基础类型变量不需要手动声明类型

● 引用类型变量应该保证类型正确，不正确的需要手动声明

● 共享的类型应该在项目 types 或者 typing 里定义

● 在一个文件里，类型定义应尽可能在顶部，类型较多时，单独抽离

● 接口，枚举类型等需添加注释
