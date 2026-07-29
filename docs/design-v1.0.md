# AIAgent 登录页 — 设计文档 V1.0

> 状态：正式版 ｜ 日期：2026-07-30 ｜ 作者：AIAgent 设计团队

---

## 1. 产品概述

### 1.1 产品信息

| 属性 | 值 |
|------|-----|
| 产品名称 | AIAgent |
| 页面类型 | 登录 / 认证 |
| 版本 | V1.0 — 五套设计方案 |
| 技术栈 | 纯静态 HTML5 + CSS3 + 原生 JavaScript |
| 依赖 | 零外部依赖（图标使用内联 SVG） |
| 目标浏览器 | Chrome / Firefox / Safari / Edge 最新两版 |

### 1.2 设计策略

采用**一核多变**架构：共享交互引擎（眼动追踪 + 角色动画 + 状态机），通过替换视觉主题覆盖不同用户场景。

### 1.3 方案矩阵

| 文件 | 代号 | 用户画像 | 设计关键词 |
|------|------|----------|-----------|
| `login.html` | 标准版 | 通用 | 稳重、专业、灰蓝紫 |
| `login-premium.html` | 高端版 | 商务/品牌 | 暗夜、香槟金、晶石几何 |
| `login-kids.html` | 儿童版 | 幼儿园/小学 | 天空彩虹、圆圆大头、云朵星星 |
| `login-student.html` | 学生版 | 中学/大学 | 深色网格、几何拼接、清新现代 |
| `login-pro.html` | 儿童Pro版 | 小学/教育机构 | 粉紫渐变、角色配饰、童趣交互 |

---

## 2. 文件清单

```
LoginPage/
├── login.html              # 标准版 — 通用场景
├── login-premium.html      # 高端美学版 — 暗夜晶石
├── login-kids.html         # 儿童版 — 天空乐园
├── login-student.html      # 学生版 — 几何现代
├── login-pro.html          # 儿童Pro版 — 学堂配饰
├── docs/
│   └── design-v1.0.md      # 本设计文档
└── README.md               # 部署说明
```

---

## 3. 共享架构

所有变体共享以下核心模式：

### 3.1 布局骨架

```
┌────────────────────┬──────────────────────┐
│   左侧面板 40-42%   │   右侧面板 58-60%     │
│                    │                      │
│  Logo              │  标题 + 副标题        │
│                    │                      │
│  角色插画           │  用户名输入           │
│  (SVG + 动画)      │  密码输入 + 眼睛切换   │
│                    │                      │
│  底部文字           │  [登录按钮]           │
│                    │                      │
└────────────────────┴──────────────────────┘
```

### 3.2 响应式断点

| 断点 | 布局 |
|------|------|
| > 768px | 左右分栏 |
| ≤ 768px | 上下堆叠，左侧 240-300px 高，角色 0.7-0.8x 缩放 |

### 3.3 共享交互引擎

```
状态机:  空闲态 ←→ 探头态(stretch-neck) ←→ 转身态(turn-away)
触发:    页面加载    输入框聚焦              密码明文可见
恢复:               失焦                    密码隐藏

瞳孔追踪:
  mousemove / touchstart / touchmove
  → handleCoordMove(clientX, clientY)
  → eyesCache (resize 时刷新)
  → turn-away 时跳过
```

### 3.4 共享 JavaScript 模块

| 模块 | 功能 | 所有变体 |
|------|------|----------|
| `focusHandler` | 聚焦 → stretch-neck | ✓ |
| `blurHandler` | 失焦 → 恢复 | ✓ |
| `togglePassword` | type/图标/class 三步切换 | ✓ |
| `updateEyesCache` | 瞳孔坐标缓存 | ✓ |
| `handleCoordMove` | 距离钳制 + transform | ✓ |
| 事件监听 | mousemove + touchstart + touchmove | ✓ |

---

## 4. 标准版 (`login.html`)

### 4.1 概览

| 属性 | 值 |
|------|-----|
| 标题 | AI教育 — 教育设备管理平台 |
| 氛围 | 稳重、亲和、专业 |
| Logo | 白底紫闪电 + "AI"紫蓝渐变 + "Agent"白色 |
| 底部文字 | 科技改变生活 |

### 4.2 色彩

| 变量 | 值 | 用途 |
|------|-----|------|
| `--bg-left` | `#383b46` | 左侧深灰蓝 |
| `--bg-right` | `#fafbfd` | 右侧近白 |
| `--input-border` | `#e5e5e5` | 输入框边框 |
| `--input-focus-border` | `#4da1ff` | 聚焦高亮 |
| `--btn-primary-bg` | `#4da1ff` | 按钮 |
| `--text-main` | `#222222` | 主文字 |
| `--text-muted` | `#9a9a9a` | 辅助文字 |

### 4.3 角色

| ID | 颜色 | 形状 | 动画 |
|----|------|------|------|
| `char-blue` | `#6d63ff` | 平顶平行四边形 190px | `float-blue` 4s |
| `char-orange` | `#fc8d70` | 拱形 R=70 | `breathe-orange` 3.5s |
| `char-black` | `#1f1f1f` | 矩形 65×140 | `sway-black` 3s |
| `char-yellow` | `#eec53e` | 胶囊 70×120 | `bounce-yellow` 2.8s |

### 4.4 组件规格

| 组件 | 规格 |
|------|------|
| 输入框 | h=46px, r=6px, 图标 20×20 |
| 按钮 | h=46px, r=6px, bg=#4da1ff |
| 图标 | 内联 SVG, stroke="currentColor" |

---

## 5. 高端版 (`login-premium.html`)

### 5.1 概览

| 属性 | 值 |
|------|-----|
| 标题 | Welcome — Sign in to continue |
| 氛围 | 极简、奢华、克制 |
| 特色 | 暗夜背景 + 粒子光环 + 玻璃拟态卡片 |

### 5.2 色彩

| 用途 | 值 |
|------|-----|
| 背景 | `#0f0f1a` |
| 主强调色 | `#c9a96e` (香槟金) |
| 文字 | `#e8e4dc` (暖白) |
| 辅助 | `#8a8578` (灰褐) |
| 卡片 | `rgba(255,255,255,0.04)` + 毛玻璃 |

### 5.3 角色（晶石几何体）

| ID | 形状 | 颜色 | 动画 |
|----|------|------|------|
| `char-crystal1` | 菱形翡翠 | `rgba(180,200,180,0.6)` | `floatCrystal` 6s |
| `char-crystal2` | 玫瑰金三角 | `rgba(201,169,110,0.25)` | `shimmerCrystal` 5s |
| `char-crystal3` | 深色长柱 | `rgba(60,60,80,0.7)` | `floatCrystal` 7s |
| `char-crystal4` | 温暖琥珀 | `rgba(200,160,100,0.35)` | `shimmerCrystal` 4.5s |

### 5.4 独有特效

- 三层粒子光环 `ringPulse` 呼吸脉冲
- 背景光晕 `ambientShift` 缓慢漂移
- 表单卡片 `backdrop-filter: blur(20px)` 玻璃拟态
- 按钮镂空金边 → hover 填充反转

### 5.5 组件规格

| 组件 | 规格 |
|------|------|
| 输入框 | 底线式, h=auto, border-bottom |
| 按钮 | h=auto, p=15px, 金边镂空, letter-spacing=4px |
| 字体 | Cormorant Garamond / Noto Serif SC 衬线细体 |

---

## 6. 儿童版 (`login-kids.html`)

### 6.1 概览

| 属性 | 值 |
|------|-----|
| 标题 | 嗨，小朋友！快来一起探索奇妙世界吧 |
| 氛围 | 欢快、柔软、梦幻 |
| 特色 | 渐变天空 + 浮云 + 闪烁星星 + 超萌大头角色 |

### 6.2 色彩

| 用途 | 值 |
|------|-----|
| 天空顶 | `#87CEEB` |
| 天空底 | `#f8e8ff` |
| 卡片 | `rgba(255,255,255,0.85)` |
| 粉 | `#FF6B9D` |
| 紫 | `#C084FC` |
| 黄 | `#FBBF24` |
| 绿 | `#34D399` |
| 蓝 | `#60A5FA` |

### 6.3 角色（圆润大头）

| ID | 形状 | 颜色 | 动画 |
|----|------|------|------|
| `char-pink` | 椭圆 75×95 | `#FF6B9D` | `bouncePink` 2.2s |
| `char-green` | 椭圆 65×55 | `#34D399` | `wiggleGreen` 2.8s |
| `char-blue-k` | 圆角矩形 85×165 | `#60A5FA` | `bounceBlue` 2.5s |
| `char-yellow-k` | 椭圆 55×70 | `#FBBF24` | `danceYellow` 2s |

### 6.4 独有设计

- 三层浮云 `cloudFloat` 漂移动画
- 五颗星星 `starTwinkle` 闪烁
- 角色微笑 `smileBounce` 弹性摆动
- 眼睛高光（白色瞳孔反光点）
- 按钮粉紫渐变 + 上浮阴影

### 6.5 组件规格

| 组件 | 规格 |
|------|------|
| 输入框 | h=50px, r=16px, border=2px, 浅紫底 |
| 按钮 | h=52px, r=16px, 粉紫渐变, 阴影 |
| 字体 | Comic Sans MS / KaiTi 卡通手写 |

---

## 7. 学生版 (`login-student.html`)

### 7.1 概览

| 属性 | 值 |
|------|-----|
| 标题 | 欢迎回来 — 登录你的学习空间 |
| 氛围 | 清新、现代、活力 |
| 特色 | 深色网格背景 + 白色卡片 + 几何角色 |

### 7.2 色彩

| 用途 | 值 |
|------|-----|
| 左侧背景 | `#0F172A` → `#1E293B` 渐变 |
| 右侧背景 | `#f0f4f8` |
| 卡片 | `#ffffff` + 阴影 |
| 青 | `#0EA5E9` |
| 紫 | `#8B5CF6` |
| 绿 | `#10B981` |
| 橙 | `#F97316` |

### 7.3 角色（几何拼接）

| ID | 形状 | 颜色 | 动画 |
|----|------|------|------|
| `char-a` | 六边形 | `rgba(14,165,233,0.5)` | `levitate` 3.5s |
| `char-b` | 半圆 | `rgba(139,92,246,0.4)` | `pulse` 3s |
| `char-c` | 细长矩形 | `rgba(16,185,129,0.45)` | `tilt` 3.8s |
| `char-d` | 圆角方 | `rgba(249,115,22,0.45)` | `hop` 2.6s |

### 7.4 独有设计

- 网格装饰背景 `background-image` 重复线性渐变
- "记住我"复选框 + "忘记密码"链接
- "还没有账号？立即注册"引导
- 输入框 `focus-within` 外发光 `box-shadow`
- 按钮青蓝渐变 + 偏移阴影

### 7.5 组件规格

| 组件 | 规格 |
|------|------|
| 输入框 | h=50px, r=12px, border=1.5px, 浅灰底 |
| 按钮 | h=50px, r=12px, 青蓝渐变, 阴影 |
| 字体 | Inter / PingFang SC 现代无衬线 |

---

## 8. 儿童Pro版 (`login-pro.html`)

### 8.1 概览

| 属性 | 值 |
|------|-----|
| 标题 | 欢迎来到 AI 学堂 — 和四位小精灵一起学习进步吧 |
| 氛围 | 温馨、鼓励、学堂气息 |
| 特色 | 粉紫渐变 + 角色配饰 + 童趣文案 |

### 8.2 色彩

| 变量 | 值 | 用途 |
|------|-----|------|
| `--bg-left` | `linear-gradient(#a18cd1, #fbc2eb)` | 粉紫渐变 |
| `--bg-right` | `#fff9fc` | 极浅粉白 |
| `--input-border` | `#ffc6d1` | 粉边框 |
| `--input-focus-border` | `#f093fb` | 亮粉聚焦 |
| `--btn-primary-bg` | `linear-gradient(#f6d365, #fda085)` | 暖橙渐变按钮 |

### 8.3 角色（标准角色 + 配饰）

| ID | 颜色 | 配饰 | 效果 |
|----|------|------|------|
| `char-blue` | `#b79ad1` (淡紫) | 🎓 学士帽 + 金色帽穗 | 漂浮时帽穗摇曳 |
| `char-orange` | `#ffb8ba` (珊瑚) | 👓 圆框眼镜 + 鼻梁桥 | 随呼吸缩放 |
| `char-black` | `#83bdf5` (天蓝) | 📖 胸前白书 + 书脊线 | 随摇摆晃动 |
| `char-yellow` | `#fce38a` (鹅黄) | 🚀 火箭背囊 + 调皮笑 | 随弹跳升空 |

### 8.4 独有设计

- 用户名图标使用书本 SVG（贴合学堂场景）
- 按钮 emoji 前缀 "🚀 开始学习"
- 底部文案 "每天进步一点点，知识改变未来 ✨"
- 角色配色柔化为粉彩（降低饱和度，更护眼）

### 8.5 组件规格

| 组件 | 规格 |
|------|------|
| 输入框 | h=52px, r=50px (胶囊), border=2px, 粉紫阴影 |
| 按钮 | h=52px, r=50px (胶囊), 暖橙渐变, 粉橙阴影 |
| 字体 | Comic Sans MS / Chalkboard SE / PingFang SC |

---

## 9. 动画系统

### 9.1 共享动画

| 动画 | 目标 | 标准/Pro | 高端 | 儿童 | 学生 |
|------|------|----------|------|------|------|
| 眨眼 | `.eye-*` | `blink` 4s | `blink` 5s | `blinkBig` 3.5s | `blinkGeom` 4s |
| 探头 | `#characters-group` | stretch-neck | stretch-neck | stretch-neck | stretch-neck |
| 转身 | `#characters-group` | turn-away | turn-away | turn-away | turn-away |

### 9.2 各变体角色动画速查

| 变体 | 角色1 | 角色2 | 角色3 | 角色4 |
|------|-------|-------|-------|-------|
| 标准/Pro | `float-blue` 4s | `breathe-orange` 3.5s | `sway-black` 3s | `bounce-yellow` 2.8s |
| 高端 | `floatCrystal` 6s | `shimmerCrystal` 5s | `floatCrystal` 7s | `shimmerCrystal` 4.5s |
| 儿童 | `bouncePink` 2.2s | `wiggleGreen` 2.8s | `bounceBlue` 2.5s | `danceYellow` 2s |
| 学生 | `levitate` 3.5s | `pulse` 3s | `tilt` 3.8s | `hop` 2.6s |

### 9.3 交互暂停规则（所有变体统一）

```
stretch-neck / turn-away 状态时:
  → 角色独立动画 animation-play-state: paused
  → 眨眼动画 animation-play-state: paused
  → turn-away 状态下瞳孔追踪跳过
```

---

## 10. 眼动追踪系统（V1.0 优化版）

### 10.1 架构

```
初始化:
  querySelectorAll('.pupil') → updateEyesCache()
  → 缓存 { cx, cy, range, el } 数组

运行时:
  mousemove / touchstart / touchmove
  → handleCoordMove(clientX, clientY)
  → turn-away? → return
  → eyesCache.forEach:
      dx = clientX - eye.cx
      dy = clientY - eye.cy
      dist = √(dx² + dy²)
      dist > range → 钳制到 range
      eye.el.style.transform = translate(dx, dy)

刷新:
  window.addEventListener('resize', updateEyesCache)
```

### 10.2 性能指标

| 指标 | 优化前 | 优化后 |
|------|--------|--------|
| 每帧重排次数 | 8 次 (8瞳孔) | 0 次 |
| 缓存刷新触发 | — | resize / orientationchange |
| touch 事件 | passive: true | passive: true |

---

## 11. 技术架构

### 11.1 技术选型

| 决策 | 理由 |
|------|------|
| 纯静态单文件 | 零构建、零部署、浏览器直接打开 |
| CSS 变量 | 统一主题色，换肤只需改变量 |
| 内联 SVG 图标 | 离线可用，`currentColor` 继承 |
| 原生 JS | 无框架开销，< 100 行 |
| CSS Animation | GPU 加速，不阻塞主线程 |
| `passive: true` | 触屏不阻塞滚动 |

### 11.2 浏览器兼容性

| 特性 | Chrome | Firefox | Safari | Edge |
|------|--------|---------|--------|------|
| CSS 变量 | ✓ 49+ | ✓ 31+ | ✓ 9.1+ | ✓ 15+ |
| CSS Animation | ✓ 43+ | ✓ 16+ | ✓ 9+ | ✓ 12+ |
| `preserve-3d` | ✓ 36+ | ✓ 16+ | ✓ 9+ | ✓ 12+ |
| `currentColor` | ✓ | ✓ | ✓ | ✓ |
| `backdrop-filter` | ✓ 76+ | ✓ 103+ | ✓ 9+ | ✓ 17+ |
| `passive` events | ✓ 51+ | ✓ 49+ | ✓ 11.1+ | ✓ 15+ |

---

## 12. 配色速查

### 12.1 各变体左侧面板

| 变体 | 背景 |
|------|------|
| 标准 | `#383b46` 纯色 |
| 高端 | `#0f0f1a` + `radial-gradient` 光晕 |
| 儿童 | `linear-gradient(#87CEEB, #f8e8ff)` 天空 |
| 学生 | `linear-gradient(#0F172A, #1E293B)` + 网格 |
| Pro | `linear-gradient(#a18cd1, #fbc2eb)` 粉紫 |

### 12.2 各变体主按钮

| 变体 | 按钮样式 |
|------|----------|
| 标准 | `bg=#4da1ff, r=6px` 纯色蓝 |
| 高端 | `border=#c9a96e, bg=透明` 金边镂空 |
| 儿童 | `linear-gradient(#FF6B9D, #C084FC), r=16px` 粉紫 |
| 学生 | `linear-gradient(#0EA5E9, #38bdf8), r=12px` 青蓝 |
| Pro | `linear-gradient(#f6d365, #fda085), r=50px` 暖橙 |

---

## 13. 未来规划

### V1.1

- [ ] 表单前端校验（非空、格式、长度）
- [ ] 登录按钮 loading 态 + API 对接
- [ ] Enter 键提交
- [ ] Toast 错误提示

### V1.2

- [ ] 多语言 i18n
- [ ] 暗色模式自动切换
- [ ] 无障碍（ARIA / 键盘导航 / 读屏器）
- [ ] 角色节日主题换肤

### V2.0

- [ ] 第三方登录（Google / GitHub / 微信）
- [ ] 动态背景（WebGL 粒子）
- [ ] React / Vue 组件化版本
