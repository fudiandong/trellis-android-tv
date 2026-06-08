# Android TV+触屏 标准化开发工作流
1. 需求录入：解析页面功能，生成标准目录结构（Activity + Fragment + ViewModel + 布局文件）
2. 布局编写：基于 ConstraintLayout 实现布局，默认开启焦点、触屏双适配属性
3. 业务代码：采用 Java + AndroidX + MVVM 架构，强制继承项目基础基类，启用 ViewBinding
4. 自动化校验：依次执行内置技能
   - tv_focus_check：校验并修复 Dpad 焦点问题
   - touch_compat：补全触屏兼容逻辑与交互效果
   - layout_adapt：抽离硬编码尺寸，完成多分辨率适配
5. 代码评审：code_review_tv 全量检查编码规范、架构、适配规则
6. 最终输出：可直接编译运行的完整代码