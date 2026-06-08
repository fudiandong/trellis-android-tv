# Android TV+触屏项目基础编码规范（Java）
## 1 开发基线
- 编译SDK：33，minSdk：21（主流TV盒子最低版本），TargetSdk 33
- 语言：纯Java，禁止Kotlin、Compose，原生AndroidX
- 依赖统一：AndroidX Appcompat、ConstraintLayout、ViewModel、LiveData、ViewBinding
- 打包：开启ViewBinding，禁用过时findViewById
## 2 代码分层强制
Activity只做页面挂载+生命周期，逻辑全部下沉ViewModel，View只负责UI渲染
## 3 兼容性硬性约束
1. 控件必须同时兼容【遥控器DPAD上下左右焦点跳转】+【手指触屏点击】
2. 不能硬编码px尺寸，全部使用dp/sp，多布局适配TV大屏(1080P/4K)+平板触屏(7/10寸)
3. 弹窗、Dialog、Popup必须处理遥控器回车确认、返回键、触屏点击
## 4 命名规范
- Activity: XXXTvActivity.java
- Fragment: XXXTvFragment.java
- ViewModel: XXXViewModel.java
- layout: activity_xxx_tv.xml / fragment_xxx_tv.xml