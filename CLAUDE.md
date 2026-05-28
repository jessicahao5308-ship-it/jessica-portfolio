# Jessica's Portfolio · Claude 协作说明

## 项目定位

个人作品集网站 ——「**AI 时代的悉尼陪读妈妈**」对外橱窗 + 引流入口。

**关键差异**：
- 这是 Jessica 的**对外展示橱窗**（公开、可索引）
- ≠ Obsidian Vault（私人工作台、含孩子真实信息，永远不公开）
- 两者之间没有自动同步通道，全部手动策展

---

## 部署信息

| 项目 | 值 |
|------|---|
| GitHub | [jessicahao5308-ship-it/jessica-portfolio](https://github.com/jessicahao5308-ship-it/jessica-portfolio) (public) |
| 网址 | https://jessicahao5308-ship-it.github.io/jessica-portfolio/ |
| 部署机制 | 推到 `main` 分支 → GitHub Pages 自动构建（1–2 分钟生效） |
| 当前版本 | v0.2 · Dark（Anthropic 风深暖黑） |

---

## 文件结构

```
jessica-portfolio/
├── index.html        主页（单文件，所有 section 都在里面）
├── works/            作品文件夹
│   └── 03-primes-composites.html
├── README.md
├── CLAUDE.md         ← 本文件
└── .gitignore
```

---

## 🚀 新增作品 SOP

### Jessica 的触发口令

她会说类似：
- "把这个 HTML 加到我的网站上"
- "我有个新作品想加进去"
- "Claude，加一个新作品"

### Claude 要做的 5 步

**1. 索取/确认素材**

- **HTML 作品**：要文件路径（本地）或在线链接
- **图片**：要图片文件路径
- **视频**：要 YouTube / Bilibili 链接（**不要**本地存视频文件，仓库会膨胀）
- **文章**：要标题 + 链接 + 一句话简介

**2. 询问元信息**（如果她没主动给）

- 作品标题（中文 + 英文副标题最佳）
- 一句话简介
- 分类标签（数学课件 / HTML 展示 / 图片 / 视频 / 文章 / Skill）
- 用到的工具栈（如果用了开源模板、AI 工具，要诚实标注）

**3. 复制文件到 `works/`**

```bash
cp /原文件路径 /Users/jessicahao/jessica-portfolio/works/xxx.html
```

⚠️ **重要**：复制而非引用 —— 原文件改动不影响网站，反之亦然。

**4. 改 `index.html` 的「精选作品」section**

- 在第一张作品卡**前**插入新卡（最新的在前）
- 沿用现有 card 样式（参考 03-primes-composites 那张）
- 封面：有截图用截图；没截图用文字 mini-preview（呼应原作品的视觉风格）
- 用工具栈标注（STACK · xxx · yyy）保持诚实化

**5. commit + push**

```bash
cd /Users/jessicahao/jessica-portfolio
git add -A
git commit -m "Add work: [作品标题]"
git push
```

完成后告诉 Jessica："已部署，1-2 分钟后刷新 https://jessicahao5308-ship-it.github.io/jessica-portfolio/ 生效。"

---

## 🎨 修改文案 / 风格 SOP

Jessica 说"改一下 XX" / "把 XX 换成 YY" 时：
1. Edit `index.html`
2. `git add -A && git commit -m "Update: xxx" && git push`
3. 告诉她 1-2 分钟生效

---

## 🔒 隐私原则（最重要，不可妥协）

之前 kids-notes 已经因隐私翻车过一次（2026-05-25 下线）。本项目从架构上避免重蹈覆辙。

**绝对不放**：
- ❌ 孩子真实姓名（Yumo / Yuhan / 予墨 / 予涵）
- ❌ 学校名（Chatswood、IEC 等具体校名）
- ❌ Obsidian 私人笔记原文（.md 内容、学习记录、薄弱点等）
- ❌ 具体学习日期、用时这类个人化数据

**可以放**：
- ✅ Jessica 主动策展、明确说要发的对外作品
- ✅ 脱敏后的数字描述（"500+ 笔记"这种统计，但不放原文）
- ✅ 工作流、方法论、自定义 Skills
- ✅ 公开身份信息（Jessica、悉尼、英语+外贸背景）

**加任何作品前必须确认**：
> "这个要发出去吗？要不要先脱敏？"

Jessica 说 yes 才发。

**不自动同步 Obsidian** —— portfolio 仓库和 Obsidian Vault 是两个独立的文件夹，没有任何脚本会把笔记搬过来。

---

## 📊 首页数字震撼条

当前显示：
- `500+` 澳洲数学课件笔记
- `2` 自研 Claude Skills
- `3` 核心方向
- `2` 真实试用客户（自家娃）

数字过时（如 Skills 多了一个）时，改 `index.html` 里 `stat-num` 那几个 div。

---

## 📞 联系入口（首页 contact 区）

当前都是占位：
- 小红书：`@待填`
- 公众号：`@待填`
- 飞书：扫码加好友（`待填`）

Jessica 给真实账号后，全局替换 `@待填` 即可。

---

## 协作偏好

继承自 Jessica 的全局偏好（详见 `~/Library/.../Jessica's Second Brain/CLAUDE.md`）：
- 默认中文
- 结构化分析 + 具体下一步 + 推荐 + 理由
- 诚实指出问题，不奉承
- 不删文件除非明确说"删掉"
- 不自动 commit 其他仓库
- 但本项目（portfolio）的 commit + push 是默认动作 —— 因为它就是部署链路

---

## 当前已知坑

- GitHub Pages free 账号要求仓库 public（不能改私有，否则部署失败）
- Tailwind CDN 在首次加载时有 ~200ms 闪烁（FOUC），不影响功能
- iCloud 同步路径含中文/空格，操作 Obsidian 文件时路径要加引号
