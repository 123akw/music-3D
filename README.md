# music-3D

![Mineradio 暗场启动页](./docs/assets/readme/cinema-beat-smoke.png)

music-3D 是 123akw 维护的 Windows / macOS 桌面沉浸式音乐播放器，把天气电台、搜索播放、歌词舞台、粒子视觉和 3D 歌单架组合成一个更接近现场感的私人音乐空间。

## 立即下载与 macOS 版本说明

| 下载入口 | 推荐人群 | 链接 |
| --- | --- | --- |
| GitHub Release | Windows / macOS 用户 | [music-3D Releases](https://github.com/123akw/music-3D/releases) |

安装时只需要下载并运行 `Mineradio-1.1.1-Setup.exe`。不要下载 `Source code`、`.blockmap`、`latest.yml`，也不要把 `win-unpacked` 当成正式安装包。

macOS 版本已经接入原生标题栏、Mac 图标资源和 `dmg` / `zip` 打包配置。当前 Mac 首版优先用于本地验证和独立构建产物，尚未承诺代码签名、公证和自动更新全链路。需要在 Mac 上体验时，建议从源码运行或本地打包：

```bash
npm install
npm start
npm run build:mac:dir
npm run build:mac
```

`npm run build:mac:dir` 会生成可直接检查的 `dist/mac-arm64/Mineradio.app` 或对应架构目录；`npm run build:mac` 会生成 `Mineradio-1.1.1-mac-arm64.dmg` / `.zip` 和 `x64` 产物。未签名构建首次打开时可能触发 macOS 安全提示，可在 Finder 中右键选择“打开”进行本地测试。

## 下载或安装被拦截怎么办

小众 Electron 桌面软件、未签名安装包有时会被浏览器、Windows Defender 或 SmartScreen 提示风险。请先确认安装包来自上面的 GitHub Release 官方入口，文件名是 `Mineradio-1.1.1-Setup.exe`。

1. 浏览器下载栏提示风险时，打开下载列表，点这条下载右侧的 `...` 三个点，选择 `保留` / `仍要保留` / `显示更多` 后继续保留。
2. Windows SmartScreen 弹出蓝色拦截窗口时，点 `更多信息`，再点 `仍要运行`。
3. 如果杀毒软件明确显示木马、高危或已经隔离，不要强行运行；删除该文件后重新从 GitHub Release 下载，仍然异常请带截图反馈。

1.1.1 的核心目标是把 Mineradio 重新整理成一份可公开下载的纯净安装版：默认视觉参数来自内置「默认测试」用户存档，首次启动就进入统一的视觉手感；3D 歌单架、歌词层级、用户存档和后台性能策略都在同一轮里收口。

## 当前版本

当前版本：`1.1.1`

状态：1.1.1 纯净安装发布版。

> 安全提示：`v1.0.10` 及更早旧安装包不再建议继续安装或传播，请先隔离旧安装包。请使用本页提供的 `Mineradio-1.1.1-Setup.exe` 进行纯净安装。

## 核心特性

- Open-Meteo 天气电台，根据当前位置、城市和天气 mood 生成更合适的播放队列
- 首页包含天气电台、每日推荐、私人电台、继续听、听歌画像和我的歌单入口
- Wallpaper 银河首页背景，未播放状态保持干净的星河氛围
- 播放后切换到 Emily / 默认播放态视觉，歌词舞台与粒子舞台同步工作
- 基于节奏的电影镜头视觉系统
- 面向长播客和 DJ 曲目的专属视觉模式
- 歌词舞台、自定义歌词、歌词位置与视觉控制
- 自定义专辑封面上传与裁剪
- 右键唤起 3D 歌单架，支持歌单队列浏览
- 网易云音乐账号、搜索、歌单、播客等体验接入
- QQ 音乐搜索、登录态与音源补充接入
- macOS 原生标题栏、红黄绿窗口控制、自适应登录页/弹窗和 Mac 打包配置
- GitHub Releases 更新检测与下载入口
- 首次启动内置「默认测试」视觉用户存档，软件内默认视觉参数与该存档一致

## 使用说明

Windows 用户可以在 GitHub Releases 中下载安装包。macOS 用户当前建议从源码运行或使用本地构建产物。

正式分发以 `Mineradio-1.1.1-Setup.exe` 为准，不建议直接下载 `win-unpacked` 目录作为正式分发包。安装包会创建桌面快捷方式；直接运行打包版 `Mineradio.exe` 时，应用也会在首次启动时补创建桌面快捷方式。

已经安装过旧版本的用户，建议卸载旧版本、隔离旧安装包后，再使用 `v1.1.1` 安装包纯净安装。

macOS 下使用原生窗口控制，不再显示 Windows 风格的右侧自绘最小化/关闭按钮。桌面歌词可继续使用；依赖 Windows WorkerW 的壁纸模式会在 macOS 上降级为不可用，避免调用 Windows API 崩溃。

## 开发运行

```bash
npm install
npm start
npm run build:win
npm run build:mac:dir
npm run build:mac
```

桌面版入口由 Electron 主进程加载本地服务。`npm run build:win` 会生成 Windows NSIS 安装包，产物位于 `dist/`。`npm run build:mac:dir` 用于快速生成 macOS `.app` 目录验证；`npm run build:mac` 会生成 macOS `dmg` 和 `zip`，同时覆盖 `arm64` 与 `x64`。

## 更新机制

Mineradio 会请求 GitHub Releases latest 检测新版本。远端版本高于本地版本时，应用内更新入口会展示 Release 内容、下载安装包到本机用户数据目录，并通过系统打开安装包。

macOS 当前不会沿用 Windows NSIS 安装器逻辑。若应用内检测到更新，Mac 版本会降级打开 GitHub Release 页面，由用户自行下载对应产物，避免误下载或打开 `.exe`。

本地验证更新链路时，可以通过 `MINERADIO_UPDATE_MANIFEST` 指向一个本地 manifest JSON 或 HTTP 地址来模拟线上 Release。

## 第三方音乐平台说明

Mineradio 不是网易云音乐、QQ 音乐或腾讯音乐娱乐集团的官方客户端，也不隶属于任何音乐平台。

项目中的第三方平台接入仅用于个人学习、本地客户端体验和用户自有账号的播放辅助。请遵守对应平台的用户协议、版权规则和会员权益规则。项目不会提供绕过付费、绕过会员、破解音质或重新分发音乐内容的能力。

QQ 音乐接入会区分“账号已登录”和“播放授权已就绪”：扫码或网页登录后，应用会持久化 QQ/QQMusic 域 cookie，并通过 `qm_keyst` / `qqmusic_key` 等字段判断播放授权。已授权账号的 QQ 搜索、歌单和播放地址会标记为可播；若官方接口只返回试听片段或无地址，界面会提示需要购买、会员权限或官方客户端权限，并继续走降音质/换源策略。

## 用户数据与隐私

登录 Cookie、搜索历史、自定义封面、自定义歌词、节奏分析缓存等数据只应保存在本机用户数据目录或浏览器本地存储中，不应提交到仓库。

更多说明见 [PRIVACY.md](./PRIVACY.md)。

## 致谢

music-3D 基于 GPL-3.0 授权的 Mineradio 开源项目继续维护和适配。emily 作为早期视觉底层想法与 `emily` 视觉预设改进方向的共创者和灵感来源之一，特此感谢。

同时感谢小天才e宝、应春日、锋将军、軌跡、林中、骊、风痕、花椰菜🥦在早期体验、测试反馈和发布准备中的帮助。

## 版权与授权

Copyright (C) 2026 123akw and music-3D contributors.

本项目采用 GPL-3.0 授权。详见 [LICENSE](./LICENSE)。

MR Logo、Mineradio 名称、界面视觉设计与原创视觉表达归作者所有；第三方依赖和第三方服务分别遵循其各自授权与服务条款。
