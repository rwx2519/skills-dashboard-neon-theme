# Dashboard Neon Theme · 设计规范

## 一、色彩体系

### 深色主题（默认）

| 变量 | 色值 | 用途 |
|---|---|---|
| --bg | #070b14 | 页面底色（近黑深蓝） |
| --bg2 | #0b1220 | 次级面板 / tooltip 底 |
| --card | rgba(15,23,42,.72) | 卡片玻璃底（半透明+blur） |
| --card2 | rgba(15,23,42,.5) | 控件 / 进度槽底 |
| --bd | rgba(56,189,248,.16) | 常规描边（青渗透） |
| --bd2 | rgba(56,189,248,.32) | 控件描边（更亮） |
| --t1 | #eef4ff | 主文字 |
| --t2 | #9db4d8 | 次文字 |
| --t3 | #64748b | 弱化文字 / 持平 |
| --cyan | #22d3ee | 青色 primary（交互态/标题强调） |
| --blue | #3b82f6 | 蓝（图表基线/渐变起点） |
| --magenta | #e879f9 | 洋红（核心指标主视觉，如一阶销额） |
| --gold | #fbbf24 | 金（目标/达成/占比线） |
| --violet | #a78bfa | 紫（辅助系列） |
| --up | #ff6b6b | **涨/正向 = 红**（中文约定） |
| --down | #34d399 | **跌/负向 = 绿**（中文约定） |
| --glow | 0 0 24px rgba(34,211,238,.12) | 全局光晕 |

### 浅色主题（body.light）

| 变量 | 色值 |
|---|---|
| --bg / --bg2 | #eef2f7 / #e2e8f0 |
| --card / --card2 | rgba(255,255,255,.92) / rgba(255,255,255,.7) |
| --bd / --bd2 | rgba(30,64,175,.14) / rgba(30,64,175,.3) |
| --t1 / --t2 / --t3 | #0f172a / #475569 / #94a3b8 |
| --cyan / --blue | #0891b2 / #2563eb |
| --magenta / --gold / --violet | #c026d3 / #d97706 / #7c3aed |
| --up / --down | #dc2626 / #059669 |
| --glow | 0 0 18px rgba(8,145,178,.08) |

### 图表辅助色（pal() 深色/浅色）

- 网格线 grid：#1e293b / #cbd5e1
- 轴文字 axis：#64748b / #94a3b8
- 面积渐变 area：rgba(34,211,238,.28) → 0（浅色 rgba(8,145,178,.25) → 0）
- 数据点内芯 dot：#0b1220 / #fff

## 二、图表分类色板（FORM_COLORS，7-12 系列通用）

```
#22d3ee  青      #3b82f6  蓝      #a78bfa  紫      #e879f9  洋红
#fbbf24  金      #34d399  绿      #fb7185  玫红
```
扩展到 12 色（环形图/堆积柱）时依次补：`#f97316 #14b8a6 #818cf8 #facc15 #4ade80 #f472b6`。
单系列多分类（饼图/环形）按上表顺序取色；堆积柱底座用 blue→cyan 渐变，核心层用 magenta→gold。

## 三、渐变清单

| 名称 | 定义 | 用途 |
|---|---|---|
| 青蓝柱渐变 | linear-gradient(90deg,#3b82f6,#22d3ee) | 横向条/进度条 |
| 洋红柱渐变 | linear-gradient(90deg,#a855f7,#e879f9) | 核心指标条 |
| 面积渐变 | rgba(34,211,238,.28) → rgba(34,211,238,0) | 山峦面积图 |
| 洋红面积 | linear-gradient(180deg,#e879f9/.95 → / .22) | 一阶销额主视觉 |
| 金色柱 | linear-gradient(180deg,#fcd34d,#d97706) | 堆积柱一阶层/环形图 |
| pill 选中态 | linear-gradient(135deg,rgba(34,211,238,.22),rgba(59,130,246,.22)) | 月份/区间切换 |
| 光带 | linear-gradient(90deg,transparent,var(--kc),transparent) | KPI 卡顶 2px |

## 四、组件配方

**玻璃卡片**
```css
background:var(--card); border:1px solid var(--bd); border-radius:14px;
padding:15px 16px; backdrop-filter:blur(8px); box-shadow:var(--glow);
```

**KPI 卡**：玻璃卡片 + `::before` 顶部 2px 光带（`--kc` 控制本卡主色）+ 三层文字（k-t 标题 t2 色 11px / k-v 大数字 22px+tabular-nums / k-s 副标 11px t3 色）+ 可选 sparkline 或 `.prog` 进度条。

**语义胶囊（环比）**：`<span class="up">▲+1.2万</span>` / `<span class="down">▼-3%</span>`，符号用 ▲▼（不用 emoji 箭头），数字保留 1 位小数，pct 场景保留 `+pct` 后缀。

**进度条**：槽 `--card2` 高 8px 圆角 4px；填充青蓝渐变 + `box-shadow:0 0 8px rgba(34,211,238,.4)`；洋红变体见 theme.css。

**呼吸点**：标题左侧 `.dot` 青色发光点，pulse 2.4s。

## 五、使用规则（硬性）

1. 红涨绿跌（中文市场约定）；持平灰 t3。
2. 深色主题为默认；浅色仅通过 `body.light` 整体切换。
3. 卡片禁纯色实底；必须玻璃拟态 + 1px 青渗透描边。
4. 数字一律 `font-variant-numeric:tabular-nums`。
5. 图表网格线虚线 `3 5`，最后一格（基线）实线。
6. 环比标签统一文案「环比 ▲+/▼-数值」，浅色主题色值同步换（红 #dc2626 / 绿 #059669）。
7. 金色只用于「目标/达成/占比」语义；洋红只用于「核心销额指标」；不要互换。
