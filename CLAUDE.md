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
| 网址 | **https://jessicainsydney.com**（自定义主域，2026-07 上）· 旧址 jessicahao5308-ship-it.github.io/jessica-portfolio 仍会跳转 |
| 域名 | 主域 `jessicainsydney.com`，DNS 在 **Cloudflare**。仓库根 `CNAME` 文件 = `jessicainsydney.com`。Cloudflare 两条 **灰云(DNS only)** CNAME：`@` 和 `www` → `jessicahao5308-ship-it.github.io`。`learn.` 子域是 quickshare，别动。|
| 机制 | push `main` → GitHub Pages 自动构建（1–2 分钟生效）· **HTTPS 已开启并强制**（Let's Encrypt 证书，自动续期）|

> ⚠️ **HTTPS 证书坑（2026-07 踩过）**：若先设自定义域名（push CNAME）、后加 DNS，GitHub 不会自动签证书，`https_certificate.state` 一直 null。解法：**摘掉再装回**——`git rm CNAME` push（等 built）→ 重新 `printf 'jessicainsydney.com' > CNAME` push，证书秒签。之后 `gh api -X PUT repos/…/pages -F https_enforced=true`（注意 `-F` 传布尔，`-f` 会当字符串报 422）。

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
2. **HERO**（`— 2026`）：超大衬线字标 `Jessica.` + 右侧**蓝图肖像板 `.plate`**（竖幅 3/4）+ 水印 `J` + 两个 CTA
   - **当前用**：`works/portrait-real.png` = Jessica 本人真实照片（悉尼海港大桥背景），裁掉海墙杂物 + 轻度暖调调和奶油纸（Pillow：desat 0.9 / 暖白平衡 / 7% cream wash）。四周白色技术标注 FIG.01/SYD·HARBOUR/33.85°S。
   - **备选资产**（riso 插画版，之前那张咖啡馆照做的）：`portrait.png`(v2 网点) / `portrait-v1.png` / `portrait-v3.png`。换真人↔插画只改 hero `<img src>`（插画版记得加回 `mix-blend-mode:multiply`）。
   - **真人照处理**：源 HEIC `~/Downloads/8e44…HEIC` → `sips` 转 jpg + 裁切(取景框掉杂物，保留大桥) → Pillow 暖调。riso 版另走 `rembg` 抠图 + 双色调 LUT + 半调。**本机无 AI 文生图**，都是图像处理。
3. **ABOUT（01）**：`About me` + 节点闭环图 `.nodes`（学 Learn → 做 Build → 享 Share）
4. **SIGNAL（02）· 全平台信号台**：`.signal` 社媒行 `.sig-row`。现两行 LIVE：小红书「悉尼陪读妈妈 Jessica」1K+（profile 65dd909b…）/ 公众号（链到最新文章）。公众号名暂借小红书同名，**待确认**。**GitHub 已全站移除**（仓库里存档 Obsidian 笔记涉隐私，见红线）。
5. **WORK（03）**：作品清单 `.work-list`，**按品类分组**（每组一个 `.group-head` 小标题，用 `.kicker` 样式）：**数学课件** → **双语研学·阅读** → **工具·其他**；组内新的在前，编号 `.rownum` 全列连续 01–06。每行 `.work-row`（编号 + 标题 + 简介 + 形式 chips + 日期/类型）。桌面 hover 浮出 `#hoverPreview`；手机显示 `.row-thumb`。加新作品 = 塞进对应组、组内置顶、全列重编号。
6. **CONTACT（05）· Sac 式横排联系行**：`Let's talk.` + `● 开放合作` + **关键词跑马灯 `.marquee`**（build in public·陪读·AI 实践…）+ **横排 `.contact-bar`**：EMAIL｜小红书（悉尼陪读妈妈 Jessica）｜**微信个人码 `.qr-mini`**（`works/qr-wechat-personal.jpg`，绿码，扫码加我）。
   - **联系区放微信、不放公众号**（Jessica 定，仿 Sac WeChat QR 格）。这是唯一放在站上的二维码（小，融进行里，不突兀）。
   - 其余二维码资产存 Obsidian `04_Resources/品牌资产_二维码/`（微信/公众号/小红书 QR + 各自名片 + 索引卡 `二维码.md`），商品图/私域引流从那取。
7. **双语**：`.len`（英文，默认）/ `.lzh`（中文），`body.lang-zh` 切换；`toggleLang()` 同步 `<title>`

> **待办**：① ~~hero 头像~~ ✅（真人海港照）；② ~~信号台真实账号 + LIVE~~ ✅；③ **确认真实公众号名**（现暂用「悉尼陪读妈妈 Jessica」）；④ ~~公众号/小红书二维码卡~~ ✅（均已上、验证可扫）。

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
- **不在站上链 GitHub**（2026-07 移除）：她的 GitHub 里有存档的 Obsidian 笔记（涉隐私，后面可能才开放）。别把 github.com 链接加回站上（signal/contact/build 都不放）。站点本身仍靠 GitHub Pages 托管（`github.io` 是托管域名，不是引流到 repo，OK）。⚠️ **若那个笔记存档 repo 是 public，需提醒她设为 private**（可能含孩子真实信息）。
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
