# Live2D 猫猫模型网页预览

一个纯前端的 Live2D 模型交互预览页面，支持三个猫猫模型（标准 / 键盘 / 手柄模式）的切换、动作播放、表情切换、点击交互、视角缩放平移等功能。

## 项目结构

```
live2d-preview/
├── index.html              # 主页面（含全部 JS/CSS）
├── README.md               # 本文件
├── vendor/                 # 第三方库（已本地化，无需联网）
│   ├── pixi.min.js             # PixiJS v6.5.10
│   ├── live2dcubismcore.min.js # Live2D Cubism Core
│   └── pixi-live2d-display.min.js  # pixi-live2d-display v0.4.0
└── models/                 # Live2D 模型资源
    ├── standard/cat_model/ # 标准模式 (demomodel.moc3)
    ├── keyboard/cat_model/ # 键盘模式 (demomodel2.moc3)
    └── gamepad/cat_model/  # 手柄模式 (demomodel3.moc3)
```

## 技术栈

- **PixiJS v6.5.10** — 2D 渲染引擎（已本地化到 vendor/）
- **pixi-live2d-display v0.4.0 (cubism4 build)** — Live2D Cubism 4 显示库，使用 cubism4-only 构建以避免 Cubism 2 运行时依赖（已本地化到 vendor/）
- **Live2D Cubism Core** — Live2D 官方 Cubism 4 核心库（已本地化到 vendor/）
- 纯 HTML + JS，无需构建工具，无需后端，无需联网

## 如何本地预览

### 方式一：本地静态服务器（推荐）

由于浏览器对 `file://` 协议下加载本地 JSON/纹理文件有 CORS 限制，**必须通过 HTTP 服务器访问**。

在项目根目录（含 `index.html` 的文件夹）下执行任意一种：

```bash
# Python 3
python3 -m http.server 8080

# Node.js (需先安装 npx)
npx serve -l 8080

# PHP
php -S localhost:8080
```

然后浏览器打开：<http://localhost:8080>

### 方式二：VS Code Live Server

安装 VS Code 插件 "Live Server"，右键 `index.html` → "Open with Live Server"。

### 方式三：直接双击 index.html（不推荐）

部分浏览器可能因 CORS 策略无法加载模型资源。如遇空白画面，请改用方式一。

## 功能说明

| 功能 | 操作 |
|------|------|
| 切换模型 | 顶部「标准模式 / 键盘模式 / 手柄模式」按钮 |
| 播放动作 | 右侧面板「动作」区域点击对应按钮 |
| 切换表情 | 右侧面板「表情」区域点击对应按钮 |
| 点击交互 | 鼠标点击模型身体，随机播放动作 / 切换表情 |
| 平移视角 | 鼠标拖动画布 |
| 缩放视角 | 鼠标滚轮，或右侧「缩放」滑块 |
| 自动眨眼 | 右侧「选项」中勾选/取消 |
| 视线跟随 | 鼠标移动时模型眼球/头部跟随（可在选项中关闭） |
| 自动待机 | 每 8 秒自动随机播放一个动作（有动作的模型） |
| 重置视角 | 右侧「重置视角」按钮 |

## 模型信息

- **标准模式**：1 张贴图，8 个表情，含物理模拟（尾巴/毛发摆动），无预定义动作
- **键盘模式**：3 张贴图，3 个表情，2 个动作组（每组 2 个动作），含配音
- **手柄模式**：3 张贴图，3 个表情，2 个动作组（每组 2 个动作），含配音

## 部署到 GitHub Pages（可选）

1. 将本项目文件夹推送到 GitHub 仓库
2. 仓库 Settings → Pages → Source 选择 `main` 分支根目录
3. 等待部署完成后访问 `https://<用户名>.github.io/<仓库名>/`

## 注意事项

- **需要 WebGL**：Live2D 模型渲染依赖 WebGL，请使用支持 WebGL 的浏览器（Chrome / Edge / Firefox / Safari 12+）。页面会自动检测 WebGL 并在不支持时给出提示
- 所有第三方库已本地化到 `vendor/` 目录，**无需联网**即可运行
- 模型文件较大（约 2.8MB），首次加载请耐心等待
- 由于浏览器安全策略，必须通过 HTTP 服务器访问（不能直接双击 index.html），详见上方「如何本地预览」
- 建议使用 Chrome / Edge / Firefox 最新版浏览器
