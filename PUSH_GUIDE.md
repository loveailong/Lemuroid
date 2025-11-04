# Lemuroid 自定义版本推送指南

## 📦 已准备好的修改

### 1. 按键映射修改
- **文件**: `lemuroid-app/src/main/java/com/swordfish/lemuroid/app/shared/input/lemuroiddevice/LemuroidInputDeviceGamePad.kt`
- **内容**: 改为 1:1 直接映射（A→A, B→B, X→X, Y→Y）

### 2. 简体中文支持
- `lemuroid-app/src/main/res/values-zh-rCN/strings.xml`
- `retrograde-app-shared/src/main/res/values-zh-rCN/strings.xml`
- `retrograde-app-shared/src/main/res/values-zh-rCN/strings-game-system.xml`

### 3. 构建配置优化
- **文件**: `lemuroid-app/build.gradle.kts`
- **内容**: 
  - 使用 debug 签名（简化构建流程）
  - 启用 R8 代码优化（isMinifyEnabled = true）

### 4. GitHub Actions 自动构建
- **文件**: `.github/workflows/build.yml`
- **功能**: 
  - 自动下载模拟器核心
  - 自动编译 Release APK
  - 推送代码后自动构建

---

## 🚀 推送步骤

### 第一步：Fork 原仓库到您的 GitHub 账号
1. 打开浏览器访问：https://github.com/Swordfish90/Lemuroid
2. 点击右上角的 **Fork** 按钮
3. 等待 fork 完成

### 第二步：修改远程仓库地址
```bash
# 将 YOUR_USERNAME 替换为您的 GitHub 用户名
git remote set-url origin https://github.com/YOUR_USERNAME/Lemuroid.git

# 验证修改
git remote -v
```

### 第三步：提交代码
```bash
# 创建提交
git commit -m "自定义修改：1:1按键映射 + 简体中文支持 + 自动构建配置"

# 查看提交记录
git log -1
```

### 第四步：推送到 GitHub
```bash
# 推送到您的仓库
git push origin master
```

---

## 🤖 GitHub Actions 自动构建说明

### 触发条件
- ✅ 每次推送代码到 master/main 分支
- ✅ 手动触发（在 GitHub Actions 页面）

### 构建产物
- 📦 APK 位置：Actions → 选择最新的构建 → Artifacts → `lemuroid-custom-release`
- 📦 保留时间：30 天
- 📦 文件名：`lemuroid-app-free-bundle-release.apk`

### 查看构建进度
1. 推送代码后，访问：`https://github.com/YOUR_USERNAME/Lemuroid/actions`
2. 点击最新的 "Build Custom APK" 工作流
3. 等待构建完成（约 15-25 分钟）
4. 下载 Artifacts 中的 APK 文件

### 手动触发构建
1. 访问：`https://github.com/YOUR_USERNAME/Lemuroid/actions`
2. 点击左侧 "Build Custom APK"
3. 点击右侧 "Run workflow" 按钮
4. 选择分支（master）
5. 点击绿色的 "Run workflow" 按钮

---

## 📊 修改内容汇总

| 文件 | 状态 | 说明 |
|------|------|------|
| `.github/workflows/build.yml` | 新增 | GitHub Actions 自动构建配置 |
| `lemuroid-app/build.gradle.kts` | 修改 | 使用 debug 签名 + 启用 R8 优化 |
| `LemuroidInputDeviceGamePad.kt` | 修改 | 1:1 按键映射 |
| `values-zh-rCN/strings.xml` (x3) | 新增 | 简体中文翻译 |

---

## ⚠️ 注意事项

1. **不要推送到原仓库**: 确保您已经 fork 并修改了 remote URL
2. **首次构建时间较长**: GitHub Actions 需要下载所有模拟器核心（约 20 分钟）
3. **签名配置**: 使用的是 debug 签名，安装时需要卸载原版 Lemuroid
4. **模拟器核心**: 自动从 LibRetro Buildbot 下载最新版本

---

## 🔧 故障排除

### 如果构建失败
1. 检查 Actions 日志中的错误信息
2. 常见问题：
   - 核心下载失败：重新运行工作流
   - 内存不足：GitHub Actions 有内存限制，一般不会出现
   - 网络超时：重新运行即可

### 如果需要本地构建
```bash
# 下载核心文件（使用 PowerShell）
cd lemuroid-cores/bundled-cores/src/main/jniLibs
# 运行之前创建的下载脚本...

# 编译 APK
./gradlew assembleFreeBundleRelease
```

---

## 🎮 使用您的自定义版本

1. 从 GitHub Actions 下载编译好的 APK
2. 传输到 Android 设备
3. 安装前先卸载原版 Lemuroid（如已安装）
4. 安装自定义版本
5. 享受 1:1 按键映射和简体中文界面！

---

**准备好了就开始推送吧！** 🚀

