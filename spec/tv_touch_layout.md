# TV+触屏双端布局规范

## 1. 布局结构
根布局优先ConstraintLayout，杜绝多层LinearLayout嵌套（TV渲染卡顿）

## 2. 焦点配置
焦点控件默认设置focusable=true，触屏环境focusableInTouchMode=true

## 3. 控件尺寸
TV端控件偏大(最小高48dp起)，触屏复用同套layout，使用 AutoSize 框架自动适配各尺寸屏幕
- 基准设计稿：1920x1080dp
- 单位：dp/sp（禁止px）

## 4. 点击状态
selector必须同时配置state_focused(遥控器选中)、state_pressed(触屏按压)

## 5. 布局约束
禁止写死宽高match_parent+固定dp混用，优先wrap_content+layout_constraint约束

## 6. 列表控件
RecyclerView统一封装TvRecyclerView，内置焦点跳转+触屏滑动兼容

## 7. AutoSize 配置
```xml
<meta-data
    android:name="design_width_in_dp"
    android:value="1920" />
<meta-data
    android:name="design_height_in_dp"
    android:value="1080" />
```