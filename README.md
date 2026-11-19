# ChatGPT 安卓 WebView 客户端壳（白色简洁版）

这是一个轻量 Android APP，在应用内部使用 Android WebView 显示 OpenAI 官方网站 `https://chatgpt.com/`，不再自动跳转到外部浏览器。

## 登录与会话
- 首次打开后，在 ChatGPT 官方网页中完成登录。
- WebView 启用 JavaScript、DOM Storage 和 Cookie；网站登录会话由 Android WebView 的 Cookie 存储机制保存在本机，重新打开 APP 时会尝试恢复。
- APP 不读取、不单独保存、不上传账号密码，也没有注入 JavaScript 桥接接口。
- 清除 APP 数据、卸载 APP、网站主动退出登录、会话过期或安全验证，都可能导致需要重新登录。
- 某些第三方 OAuth 登录（例如 Google）可能拒绝在内嵌 WebView 中运行。如果遇到登录提供方的限制，可能需要通过系统浏览器完成授权；这不是本 APP 可以绕过的限制。

## 安全与隐私说明
- 只加载 HTTPS 页面，禁止明文 HTTP 混合内容。
- 禁止网页访问本地文件和 Content URI。
- 使用 Android WebView 自带的 Cookie 持久化，不将 Cookie 导出到应用自建文件。
- 本项目不是 OpenAI 官方发布的原生客户端，而是打开官方 ChatGPT 网站的第三方 WebView 外壳。

## 用 Android Studio 构建
1. 安装 Android Studio（建议最新版）及 Android SDK 35。
2. 打开本项目文件夹 `ChatGPTLauncher`。
3. 等待 Gradle Sync 完成。
4. 选择 Build > Build Bundle(s) / APK(s) > Build APK(s)。
5. APK 通常生成在 `app/build/outputs/apk/debug/app-debug.apk`。

## 在线编译 APK（GitHub Actions）
1. 在 GitHub 新建一个空仓库。
2. 将本项目 ZIP 解压后，把里面所有文件上传到仓库根目录（包括 `.github` 隐藏目录）。
3. 打开仓库的 Actions 页面，选择 `Build Android APK`，点击 `Run workflow`。
4. 构建成功后打开该次运行页面，在 Artifacts 下载 `ChatGPT-Android-APK`，解压得到 `app-debug.apk`。
5. 将 APK 传到华为 Mate40 Pro 安装。

## 华为 Mate40 Pro / HarmonyOS 4.2 安装提示
从可信来源将 APK 下载到手机，点击安装并按系统提示允许该来源安装应用。首次启动需要联网并在 APP 内登录 ChatGPT。
