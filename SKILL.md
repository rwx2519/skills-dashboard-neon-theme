---
name: dashboard-neon-theme
description: 深色霓虹数据大屏配色方案（源自百事饮品山东行销公司直营一阶数据大屏）。当用户构建/美化数据看板、大屏、可视化 HTML 页面并要求「霓虹蓝青配色」「深色玻璃拟态」「红涨绿跌中文约定」等风格时使用本 skill。提供双主题（深色/浅色）CSS 变量体系、组件配方、图表色板，可直接引入 assets/theme.css。
agent_created: true
---

# 数据大屏霓虹配色方案（Dashboard Neon Theme）

深色底 + 霓虹蓝/青主色 + 玻璃拟态卡片 + 红涨绿跌语义色。该方案已在生产大屏（直营一阶数据大屏、WIE 冰柜考核看板等）长期使用，覆盖 1920×1080 与移动端宽屏。

## 使用方法

1. 新建看板/大屏页面：将 `assets/theme.css` 复制或 `<link>` 引入页面，HTML 结构使用语义化 class（`.card` `.kpi` `.pill` `.prog` 等，见 `references/theme.md`）。
2. 美化已有页面：将 `assets/theme.css` 的 `:root`（深色）与 `body.light`（浅色）变量块注入目标页面 CSS 顶部，再把卡片的 `background/border/backdrop-filter/box-shadow` 替换为变量写法（配方见 `references/theme.md`）。不改目标页面的布局结构，只替换颜色与质感。
3. 图表配色（ECharts/Chart.js/SVG 内联）：直接取 `references/theme.md` 中的「图表色板」十六进制值；深色主题下网格线 `#1e293b`、轴文字 `#64748b`。

## 硬性规则

- **红涨绿跌**（中文市场约定，与欧美相反）：涨/达标/正向 = `--up: #ff6b6b`（红），跌/未达标/负向 = `--down: #34d399`（绿），持平 = `--t3`。
- 卡片一律玻璃拟态：`background: var(--card); border: 1px solid var(--bd); backdrop-filter: blur(8px); border-radius: 14px;`，禁止纯色实底。
- KPI 卡顶部有 2px 霓虹光带（`::before` 渐变，随卡片主色 `--kc` 变化）。
- 大屏默认深色主题（`--bg:#070b14`），浅色主题通过 `body.light` 整体切换，不做单元素混搭。
- 数字使用 `font-variant-numeric: tabular-nums` 保证对齐。

## 资源索引

- `assets/theme.css` — 完整双主题变量 + 基础组件样式，直接引入即可用
- `assets/demo.html` — 独立演示页（KPI 卡/进度条/pill 徽章/迷你图表），打开即见效果
- `references/theme.md` — 完整设计规范：全部色值、渐变清单、组件配方、图表 12 色板、语义色使用场景

配色微调时只改变量值，不改选择器结构；新增语义色先在 `:root` 定义再引用。
