---
name: touch_compat
description: 现有TV代码一键兼容触屏，补充触屏点击逻辑、焦点触摸模式属性
allowed-tools: [file-read,file-write]
---
执行逻辑：
1. 遍历布局，缺少focusableInTouchMode的控件自动补充属性
2. 无按压selector的控件补充selector选择器xml
3. 自定义View缺少onTouch监听的补充触屏适配代码
4. 保证同一套代码：遥控器可用+手指触屏可用