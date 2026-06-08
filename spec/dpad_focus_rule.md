# D-pad 焦点导航规范

## 核心原则

所有 TV UI 必须实现**闭环焦点导航**，确保用户按任意方向键时焦点始终在可控范围内。

## 焦点配置

### 1. 基础配置
```xml
<!-- 焦点控件必须设置 -->
android:focusable="true"
android:focusableInTouchMode="true"
```

### 2. 首次焦点
```xml
<!-- 页面默认焦点：根布局设置 -->
android:defaultFocusHighlightEnabled="true"
```

## 方向导航

### 3. nextFocusDown/Up/Left/Right
```xml
<!-- 明确指定各方向的下一个焦点控件 -->
android:nextFocusDown="@+id/btn_confirm"
android:nextFocusUp="@+id/btn_cancel"
android:nextFocusLeft="@+id/btn_prev"
android:nextFocusRight="@+id/btn_next"
```

### 4. 禁止焦点越界
```xml
<!-- 边缘控件必须指定环绕方向 -->
<Button
    android:id="@+id/btn_first"
    android:nextFocusLeft="@+id/btn_last" />  <!-- 左边界环绕到最后一个 -->
```

## 焦点丢失处理

### 5. ViewGroup 焦点容器
```xml
<!-- 动态区域使用 FocusableRelativeLayout 包裹 -->
<FocusableRelativeLayout
    android:focusable="true"
    android:focusableInTouchMode="true">
    <!-- 子控件 -->
</FocusableRelativeLayout>
```

### 6. 焦点状态监听
```java
// 监听焦点变化，处理边界情况
view.setOnFocusChangeListener((v, hasFocus) -> {
    if (hasFocus) {
        // 焦点进入：放大/高亮效果
    }
});
```

## 常见错误

### ❌ 禁止
- 动态添加 View 后未设置 nextFocus 属性
- Recyclerview item 内嵌套可聚焦控件未指定导航
- 使用.requestFocus() 而不处理焦点状态

### ✅ 正确
- 静态布局完整配置 nextFocus 四方向
- 动态区域使用 FocusChangeListener 手动处理
- 边缘控件使用 `nextFocusUp/Down/Left/Right` 形成闭环

## 触摸兼容

### 7. 触摸点击
```java
// 触摸模式下支持点击
if (isInTouchMode()) {
    performClick();
}
```

### 8. 触摸模式焦点
```xml
<!-- 触屏设备需要 -->
android:focusableInTouchMode="true"
```
