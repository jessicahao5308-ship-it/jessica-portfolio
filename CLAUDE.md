# Jessica's Portfolio · Claude 协作说明

## 项目定位

个人作品集网站 ——「**悉尼陪读妈妈 Jessica · Learn in public, build in public**」对外橱窗 + 引流入口。

- **奶油纸 × 蓝图技术图 × 编辑风**（复刻 Sac 风格，2026-07 改版）：暖奶油纸 `--paper #f2ede3` + 橙锈红 accent `#e0602f` + 黑墨字 `#1b1813`，**单文件 `index.html`**，内联 CSS/JS。
  - 签名装饰语言：十字准星角标 `.cross`、点阵/网格 `.bp-dots/.bp-grid`、mono 小标号 `.kicker`（`ABOUT — 01`）、超大衬线 `.serif-en`（Playfair 800）、水印数字 `.watermark`。
  - 前身是暗色 off-black + 琥珀（v3，git 历史里）；如需回退可查 commit `99e52c9` 前。
- ≠ Obsidian Vault（私人工作台、含孩子真实信息，永不公开）。两者**无自动同步**，全手动策展。

## 部署

| 项 | 值 |
|---|---|
| GitHub | [jessicahao5308-ship-it/jessica-portfolio](https://github.com/jessicahao5308-ship-it/jessica-portfolio) · **必须 public**（否则 Pages 部署失败）|
| 网址 | https://jessicahao5308-ship-it.github.io/jessica-portfolio/ |
| 机制 | push `main` → GitHub Pages 自动构建（1–2 分钟生效）|

**本项目 `commit + push` 是默认动作**（它就是部署链路），不用每次问。

## 文件结构

```
jessica-portfolio/
├── index.html        单文件主页（暗色 + Burton 式作品 list + hover 浮图 + 中英双语切换）
├── works/            作品文件（HTML / PDF / 截图 / 桌面 App 安装包）
│   ├── shots/        作品缩略图（无头 Chrome 截，见 SOP）
│   └── use-ai-ppt/
├── README.md
└── CLAUDE.md         ← 本文件
```

## 网页结构（index.html，单页多 section，每段带 `— 0N` 小标号）

1. **NAV**：`Jessica.` + slogan + About/Signal/Work/Contact + `SYD · 2026` chip + `EN/中` 切换按钮
2. **HERO**（`— 2026`）：超大衬线字标 `Jessica.` + 右侧**蓝图占位板 `.plate`**（`FIG.01 PORTRAIT / 头像待补`，**等 Jessica 给照片/插画替换**）+ 水印 `J` + 两个 CTA
3. **ABOUT（01）**：`About me` + 节点闭环图 `.nodes`（学 Learn → 做 Build → 享 Share）
4. **SIGNAL（02）· 全平台信号台**：`.signal` 社媒行 `.sig-row`（图标 + 账号 + 粉丝数 + sparkline `.spark` + LIVE/SOON 状态）。**GitHub 是真 LIVE**，小红书/公众号/飞书现 `@TBA` = SOON（有真账号后改 handle + 状态）
5. **WORK（03）**：作品清单 `.work-list`，每行 `.work-row`（编号 + 标题 + 简介 + 形式 chips + 日期/类型）。桌面 hover 浮出 `#hoverPreview`；手机显示 `.row-thumb`
6. **CONTACT（04）**：`Let's talk.` + 三张 `.card`（小红书 / 公众号 / GitHub）
7. **双语**：`.len`（英文，默认）/ `.lzh`（中文），`body.lang-zh` 切换；`toggleLang()` 同步 `<title>`

> **待办**：① hero 蓝图占位板换成真实照片或墨绘插画（Jessica 定）；② 信号台三个 `@TBA` 换真实账号 + 状态改 LIVE；③ 联系卡二维码。

## 作品呈现：两种行

- **单作品**：一行，标题链接直接打开作品（如 用好 AI、桌面袋鼠）
- **案例节点**（同一节课的多种形式）：一行 + 一排「形式 chips」(`.forms > a.form`)
  - 质数与合数 = 📖 笔记 · 🖨️ PDF · 🎞️ 课件 · 🎯 游戏
  - 角的类型 = 📖 笔记 · 🖨️ PDF · 🎯 游戏
- 行是 `<div>`（**非 `<a>`**，因含多个链接）；标题用 `a.rowtitle-link`，`data-img` 驱动 hover 预览图

## 🚀 加新课件案例 SOP（触发：「加 Year X 的 XX 单元」）

课件源在 Obsidian「可分发课件」（**已去隐私 + 品牌化的分发版**）：
```
~/Library/Mobile Documents/iCloud~md~obsidian/Documents/Jessica's Second Brain/03_Areas-Startup/02 可分发课件/Year N/<Unit>/
```
1. 从该单元**复制**（非引用）要展示的形式到 `works/`：笔记 `.html` / `.pdf` / 游戏 `.html`
2. 截缩略图到 `works/shots/`：起 `python3 -m http.server 8765`，无头 Chrome 截首屏
   ```
   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --window-size=1280,800 --screenshot=works/shots/xxx.png "http://localhost:8765/works/xxx.html"
   ```
   游戏类用手机尺寸 `--window-size=430,860`
3. 在 `.work-list` 复制一个案例 `.work-row` 结构，填标题 + 简介 + 形式 chips + `data-img`
4. `git add -A && git commit && git push`

## 🔒 红线（不可妥协）

- **隐私**：绝不放孩子真名（Yumo/Yuhan/予墨/予涵）、学校名（Chatswood/IEC）、Obsidian 私人笔记原文、具体学习日期/用时。**不自动同步 Obsidian**。
- **版权**：网站现**公开可下载** MathsOnline 衍生的双语 PDF（质数、角的类型）。这些是她去隐私+品牌化的"可分发版"，是否公开由她判断；**新增可下载课件/PDF 时主动提示一句版权**。
- 加任何对外作品前确认：「这个要发出去吗？要不要先脱敏？」她说 yes 才发。

## KangaPet 桌面袋鼠下载

`works/KangaPet-0.1.0-AppleSilicon.dmg`（3.3MB，Tauri）—— **仅 Apple 芯片 Mac，未签名（adhoc）**，下载者需右键→打开过 Gatekeeper（卡片已注明）。源码/打包在 Obsidian `.../素材库/图片素材库/KangaPet/`。
**Backlog**：网页版袋鼠（浏览器即玩、零下载门槛，更适合小红书引流）—— 她说先不做。

## 协作偏好

继承全局 `~/.claude/CLAUDE.md`（中文、结构化分析 + 具体下一步 + 推荐 + 理由、诚实不奉承、不删文件除非明说）。

## 已知坑

- Pages free 账号要求仓库 public。
- Tailwind CDN 首次加载有轻微 FOUC。
- iCloud / Obsidian 路径含中文 + 空格，命令里要加引号。
- **无头截图**：hero 已不用 `88dvh`（改为自然高度），可直接 `--window-size=1440,4200` 截整页再 `sips -c` 裁段。
