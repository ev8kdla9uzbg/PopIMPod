# PopIMPod

PopIM iOS SDK 的私有 CocoaPods Spec Repo（索引仓库）。

本仓库只存放 `.podspec` 索引文件，不存放二进制产物。

SDK 二进制分别托管在：

| Pod | 二进制仓库 |
|-----|-----------|
| `PopIMLib` | [ev8kdla9uzbg/PopIMLib](https://github.com/ev8kdla9uzbg/PopIMLib) |
| `PopIMApnsLib` | [ev8kdla9uzbg/PopIMApns](https://github.com/ev8kdla9uzbg/PopIMApns) |

> 注意：`PopIMApnsLib` 的组件名与其仓库名（`PopIMApns`）不一致，Podfile 中请使用组件名 `PopIMApnsLib`。


## 接入方式

### 1. 添加私有源（每台机器执行一次）

```bash
pod repo add PopIMPod https://github.com/ev8kdla9uzbg/PopIMPod.git
```

### 2. Podfile 配置

```ruby
source 'https://github.com/ev8kdla9uzbg/PopIMPod.git'      # 私有源
source 'https://cdn.cocoapods.org/'                       # 官方源（系统依赖）

platform :ios, '12.0'
use_frameworks!

target 'YourApp' do
  pod 'PopIMLib', '1.1.9.1'
  pod 'PopIMApnsLib', '1.0.6'   # 推送到达统计，按需引入
end
```

### 3. 安装

```bash
pod repo update PopIMPod
pod install
```

## 可用版本

### PopIMLib

| 版本 | 说明 |
|------|------|
| 1.1.9.1 | 当前最新 |

### PopIMApnsLib

| 版本 | 说明 |
|------|------|
| 1.0.6 | 当前最新 |
| 1.0.5 | |
| 1.0.4 | |

## 目录结构

CocoaPods 要求固定的三级路径，不可随意调整：

```
Specs/<PodName>/<Version>/<PodName>.podspec
```

## 发布新版本

1. 在对应的二进制仓库（[PopIMLib](https://github.com/ev8kdla9uzbg/PopIMLib) 或 [PopIMApns](https://github.com/ev8kdla9uzbg/PopIMApns)）更新 xcframework 与 podspec 版本号，提交后打上与版本号同名的 tag 并推送
2. 回到本仓库执行：

```bash
pod repo push PopIMPod PopIMLib.podspec --allow-warnings --skip-import-validation
# 或
pod repo push PopIMPod PopIMApnsLib.podspec --allow-warnings --skip-import-validation
```

> `--skip-import-validation` 为必需参数：纯二进制 xcframework 无法通过 CocoaPods 的 import 校验。
