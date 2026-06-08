# MVVM 架构规范

## 项目架构

基于 Google Android Architecture Components，采用 **MVVM + ViewBinding** 模式。

## 目录结构

```
com.stb.duer.apps.xtvott
├── ui/                    # Activity/Fragment/Adapter
│   ├── main/
│   ├── player/
│   └── common/
├── vm/                    # ViewModel
├── model/                 # 数据模型
│   ├── entity/           # 数据库实体
│   └── data/             # 数据类
├── repository/           # 数据仓库
├── data/                 # 数据层
│   ├── local/            # 本地存储
│   └── remote/           # 远程接口
└── util/                 # 工具类
```

## ViewModel 规范

### 1. ViewModel 创建
```java
// 使用 ViewModelProvider
ViewModelProvider provider = new ViewModelProvider(this);
MyViewModel vm = provider.get(MyViewModel.class);
```

### 2. LiveData 使用
```java
// 暴露 LiveData
private final MutableLiveData<String> statusLiveData = new MutableLiveData<>();
public LiveData<String> getStatus() {
    return statusLiveData;
}
```

### 3. 生命周期感知
```java
// 使用 observe 绑定到 lifecycleOwner
viewModel.getData().observe(this, data -> {
    // 自动在 onDestroy 时解绑
});
```

## 数据绑定

### 4. ViewBinding 使用
```java
// Activity 中
private ActivityMainBinding binding;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    binding = ActivityMainBinding.inflate(getLayoutInflater());
    setContentView(binding.getRoot());
}
```

### 5. 双向绑定（少量使用）
```xml
<!-- 仅用于简单表单 -->
android:text="@={viewModel.inputText}"
```

## Repository 模式

### 6. 数据仓库封装
```java
public class UserRepository {
    private final UserApi api;
    private final UserDao dao;

    public LiveData<User> getUser(int id) {
        // 优先使用本地缓存，支持离线
        return dao.getUser(id);
    }
}
```

## 常见错误

### ❌ 禁止
- 在 ViewModel 中直接操作 View
- 使用 LiveData 而不 observe
- ViewModel 中使用 Context（使用 Application Context）
- 在主线程进行网络/数据库操作

### ✅ 正确
- ViewModel 通过 LiveData 通知 View
- 使用 Executor/AsyncTask 处理异步
- 使用 Application Context 或 LiveDataScope
- 数据操作在 Repository 层统一处理
