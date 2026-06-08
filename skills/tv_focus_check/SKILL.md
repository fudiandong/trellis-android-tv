---
name: tv_focus_check
description: 自动校验页面焦点逻辑，检查Dpad焦点越界、控件无法聚焦、焦点丢失问题，输出修改代码
allowed-tools: [file-read,file-write,code-lint]
---
执行逻辑：
1. 读取目标layout xml + 对应Activity/Fragment Java代码
2. 核查：focusable、focusableInTouchMode、key事件拦截、RecyclerView焦点配置
3. 找出焦点跳转BUG，自动修正xml属性和java按键回调代码
4. 输出修改后的完整文件，标注改动点