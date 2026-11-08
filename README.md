# 宇宙无敌号 · 深圳站

一个纯静态的演唱会倒计时页面：深色雨幕背景 + 毛玻璃卡片，实时显示距离开演还有多少天、时、分、秒。

无框架、无构建、无依赖 —— 只有一个 `index.html`，双击就能跑。

## 预览

在线地址：<https://tiipyluo-hash.github.io/SpaceInvincible/>

> 上线后可在仓库根目录放一张 `preview.png` 并在此处引用，README 会更直观。

## 功能

- **实时倒计时**：基于 `setInterval` 每秒刷新，目标时间精确到 `+08:00`，不受访问者本地时区影响
- **毛玻璃视觉**：`backdrop-filter: blur()` + 半透明描边 + 内发光
- **响应式**：宽度 ≤ 768px 时四个时间格自动换行、字号随之下调
- **零依赖**：无 npm、无打包，图片与字体走外链

## 目录结构

```
.
├── index.html                          # 页面全部内容（结构 + 样式 + 脚本）
├── README.md
└── .github/
    └── workflows/
        └── deploy-pages.yml            # 推送到 main 自动发布到 GitHub Pages
```

## 本地运行

不需要任何环境，任选一种：

```bash
# 方式一：直接打开
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows

# 方式二：起一个本地服务器（推荐，避免个别浏览器对本地文件的限制）
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

## 自定义

所有可调项都集中在三处：

**1. 标题**——搜索 `<h1>`：

```html
<h1>宇宙无敌号-深圳站</h1>
```

**2. 目标时间**——搜索 `targetDate`：

```js
const targetDate = new Date('2026-01-31T19:00:00+08:00');
```

> 时区后缀 `+08:00` 建议保留，否则访问者在其他时区打开会看到偏移后的倒计时。

**3. 背景图**——搜索 `background: url(`：

```css
background: url('https://i.postimg.cc/6pS9NP1m/concert.jpg') center/cover no-repeat;
```

## 部署

仓库已配置 GitHub Actions 自动部署，流程：**推送到 `main` → 自动构建 → 发布到 Pages**。

首次启用（只需一次）：

1. 打开仓库 **Settings → Pages**
2. 在 **Build and deployment → Source** 选择 **GitHub Actions**
3. 回到 **Actions** 标签页，运行一次 `Deploy to GitHub Pages`（或直接推到 `main` 触发）

发布地址：<https://tiipyluo-hash.github.io/SpaceInvincible/>

也可以在 **Actions → Deploy to GitHub Pages → Run workflow** 手动触发。

## 已知问题

| 问题 | 说明 |
| --- | --- |
| 倒计时已过期 | 目标时间 `2026-01-31` 已过去，页面当前固定显示 `00 00 00 00`，且没有「已结束」提示 |
| 外链资源不稳 | 背景图依赖 `i.postimg.cc` 图床，字体依赖 Google Fonts，任一失效都会导致观感下降（国内访问 Google Fonts 通常不通） |
| CSS 重复声明 | `.container` 的 `background` 与 `box-shadow` 各写了两次，前一组被覆盖 |

## Roadmap

- [ ] 过期后展示「已结束」状态或自动切换到下一场
- [ ] 把日期 / 标题 / 背景图抽成顶部 `CONFIG` 对象，换场次只改一处
- [ ] 背景图与字体本地化，摆脱图床和 CDN 依赖
- [ ] 补充 OG 分享卡片与 favicon

## 致谢

Fork 自 [CherryCheys/SpaceInvincible](https://github.com/CherryCheys/SpaceInvincible)，原始页面与设计归原作者所有。
