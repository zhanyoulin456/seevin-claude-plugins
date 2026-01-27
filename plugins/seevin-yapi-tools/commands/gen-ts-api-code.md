---
description: 根据接口文档使用mcp生成代码
argument-hint: [yapi-url] [api-path] [type-path]
---

# 参数说明

$ARGUMENTS 中的url参数为yapi的接口文档地址
还需要代码生成后存放的位置，如果用户没有提供，需要提示用户传入
也就是必须要传入接口文件的位置 和 yapi的url

## 注意事项

1. 用户需要传入2个位置，一个是接口文件的位置，一个是接口的ts类型
2. 如果yapi-get-interface-mcp mcp工具调用失败，终止流程，提示用户检查工具可用性

## 执行步骤

1. 调用 yapi-get-interface-mcp mcp，根据接口文档获取接口信息
2. 根据接口信息和规范生成代码
3. 将代码存储到用户指定位置
