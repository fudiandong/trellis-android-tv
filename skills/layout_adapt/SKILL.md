---
name: layout_adapt
description: 布局多尺寸适配，拆分dimens，区分TV大屏和触屏小屏
allowed-tools: [file-read,file-write]
---
执行逻辑：
1. 提取布局内固定dp数值，抽入dimens资源
2. 自动生成values/values-sw720dp两套dimens配置
3. 修改xml硬编码尺寸为@dimen引用，完成一套布局双端适配