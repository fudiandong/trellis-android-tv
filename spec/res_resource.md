# 资源文件规范

## AutoSize 框架适配

项目使用 **Android AutoSize** 框架实现屏幕适配，无需编写多套 dimens 文件。

### 1. 启用 AutoSize
```xml
<!-- AndroidManifest.xml -->
<manifest>
    <application>
        <meta-data
            android:name="design_width_in_dp"
            android:value="1920" />
        <meta-data
            android:name="design_height_in_dp"
            android:value="1080" />
    </application>
</manifest>
```

### 2. 单位使用
```xml
<!-- 优先使用 dp/sp，禁止使用 px -->
<dimen name="text_size_title">48sp</dimen>
<dimen name="margin_standard">24dp</dimen>

<!-- 禁止 -->
<!-- <dimen name="wrong_size">100px</dimen> -->
```

### 3. 布局约束
```xml
<!-- 优先使用约束布局 + wrap_content/match_constraint -->
<TextView
    android:layout_width="0dp"
    app:layout_constraintWidth_default="wrap"
    android:textSize="@dimen/text_size_title" />
```

## 布局文件

### 4. 命名规范
```
activity_xxx_tv.xml     # TV Activity 布局
fragment_xxx_tv.xml     # TV Fragment 布局
item_xxx.xml            # 列表项布局
layout_xxx.xml          # 可复用布局
```

### 5. TV/触屏共用
```xml
<!-- 同一布局文件，AutoSize 自动适配 -->
<!-- 不需要 values-sw720dp 等额外适配 -->
```

## 字体适配

### 6. sp 单位字体
```xml
<!-- 所有字体使用 sp 单位，AutoSize 自动缩放 -->
<TextView
    android:textSize="@dimen/text_size_body"
    android:textColor="@color/text_primary" />
```

## 颜色资源

### 7. 颜色定义
```xml
<!-- res/values/colors.xml -->
<color name="primary">#FF6200EE</color>
<color name="text_primary">#FFFFFFFF</color>
<color name="text_secondary">#B3FFFFFF</color>
```

## 字符串资源

### 8. 字符串规范
```xml
<!-- 禁止硬编码字符串 -->
<!-- 错误：android:text="确定" -->
<!-- 正确 -->
android:text="@string/btn_confirm"
```

## Selector 选择器

### 9. 焦点/按压状态
```xml
<!-- 必须同时定义遥控器焦点和触屏按压状态 -->
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_focused="true" android:drawable="@drawable/bg_focused"/>
    <item android:state_pressed="true" android:drawable="@drawable/bg_pressed"/>
    <item android:drawable="@drawable/bg_normal"/>
</selector>
```

## 常见错误

### ❌ 禁止
- 使用 px 单位
- 硬编码尺寸数值
- 硬编码字符串
- 布局中缺少 focusable 属性

### ✅ 正确
- 使用 dp/sp 单位
- 统一管理颜色/字符串资源
- TV 控件设置 focusable="true"
- 使用 ConstraintLayout 减少嵌套
