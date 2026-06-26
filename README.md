# Jessica's Portfolio · 悉尼陪读妈妈

个人作品集网站 —— AI 时代的悉尼陪读妈妈。

> Sale myself · 用 Claude Code + Obsidian，把澳洲教育和新移民资源，系统化、产品化，分享给中文世界。

## Stack

- 单文件静态 `index.html` + Tailwind CSS (CDN)，内联 CSS/JS（hover 浮图预览 + 滚动渐入 + 中英双语切换）
- 部署：GitHub Pages（push `main` 自动构建）
- 无构建依赖、无 JS 框架

## 本地预览

直接双击 `index.html`；或 `python3 -m http.server` 后访问（作品链接走相对路径）。

## 作品 / Works

`works/` 下放作品文件（HTML / PDF / 截图 / 桌面 App 安装包）。主页以 **list（清单）** 呈现，分两类：

- **单作品** — 一行，标题直接链接到作品
- **案例节点** — 同一节课的多种形式（笔记 / PDF / 课件 / 游戏）收成一行 + 一排「形式 chips」

新增课件案例的完整 SOP（从 Obsidian「可分发课件」复制 + 截图 + 拼行）见 `CLAUDE.md`。

## 隐私 / 版权

- 网站只放主动策展的对外作品；**不自动同步** Obsidian 私人笔记
- 孩子真实姓名 / 学校 / 学习记录等敏感内容永不上线
- 可下载的课件 PDF 均为去隐私 + 品牌化的「可分发版」；新增可下载课件前确认版权与脱敏
