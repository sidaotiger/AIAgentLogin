# AIAgent Login Page — Design Document V1.0

> Status: Release ｜ Date: 2026-07-30 ｜ Author: AIAgent Design Team

---

## 1. Product Overview

### 1.1 Product Info

| Attribute | Value |
|-----------|-------|
| Product Name | AIAgent |
| Page Type | Login / Authentication |
| Version | V1.0 — Five Design Variants |
| Tech Stack | Pure static HTML5 + CSS3 + Vanilla JavaScript |
| Dependencies | Zero (icons use inline SVG) |
| Target Browsers | Chrome / Firefox / Safari / Edge (latest 2 versions) |

### 1.2 Design Strategy

A **one-core, multi-variant** architecture: a shared interaction engine (eye-tracking + character animation + state machine) paired with swappable visual themes to cover diverse user scenarios.

### 1.3 Variant Matrix

| File | Codename | Audience | Keywords |
|------|----------|----------|----------|
| `login.html` | Standard | General | Solid, professional, slate-blue |
| `login-premium.html` | Premium | Business/Brand | Dark, champagne gold, crystal geometry |
| `login-kids.html` | Kids | Preschool/Primary | Sky rainbow, round-headed, clouds & stars |
| `login-student.html` | Student | Secondary/College | Dark grid, geometric patchwork, fresh modern |
| `login-pro.html` | Kids Pro | Primary/Education | Pink-purple gradient, character accessories, playful |

---

## 2. File Inventory

```
LoginPage/
├── login.html              # Standard — General purpose
├── login-premium.html      # Premium — Dark crystal
├── login-kids.html         # Kids — Sky wonderland
├── login-student.html      # Student — Geometric modern
├── login-pro.html          # Kids Pro — School accessories
├── docs/
│   └── design-v1.0.md      # This document (Chinese)
│   └── design-v1.0-en.md   # This document (English)
└── README.md               # Deployment guide
```

---

## 3. Shared Architecture

All variants share the following core patterns:

### 3.1 Layout Skeleton

```
┌────────────────────┬──────────────────────┐
│  Left Panel 40-42% │  Right Panel 58-60%   │
│                    │                       │
│  Logo              │  Title + Subtitle     │
│                    │                       │
│  Character Art      │  Username Input       │
│  (SVG + Animation) │  Password + Eye Toggle│
│                    │                       │
│  Footer Text       │  [Login Button]       │
│                    │                       │
└────────────────────┴──────────────────────┘
```

### 3.2 Responsive Breakpoint

| Breakpoint | Layout |
|------------|--------|
| > 768px | Side-by-side columns |
| ≤ 768px | Stacked, left panel 240-300px tall, characters 0.7-0.8x scale |

### 3.3 Shared Interaction Engine

```
State Machine:  Idle ←→ Stretch-neck ←→ Turn-away
Trigger:        Page load    Input focus     Password visible
Restore:                     Input blur      Password hidden

Pupil Tracking:
  mousemove / touchstart / touchmove
  → handleCoordMove(clientX, clientY)
  → eyesCache (refreshed on resize)
  → skipped when turn-away is active
```

### 3.4 Shared JavaScript Modules

| Module | Function | All Variants |
|--------|----------|:------------:|
| `focusHandler` | Focus → stretch-neck | ✓ |
| `blurHandler` | Blur → restore | ✓ |
| `togglePassword` | type/icon/class triple toggle | ✓ |
| `updateEyesCache` | Cache pupil coordinates | ✓ |
| `handleCoordMove` | Clamp distance + transform | ✓ |
| Event listeners | mousemove + touchstart + touchmove | ✓ |

---

## 4. Standard (`login.html`)

### 4.1 Overview

| Attribute | Value |
|-----------|-------|
| Title | AI Education — Device Management Platform |
| Vibe | Solid, warm, professional |
| Logo | White-bg purple lightning + "AI" gradient + white "Agent" |
| Footer | Technology changes life |

### 4.2 Colors

| Variable | Value | Usage |
|----------|-------|-------|
| `--bg-left` | `#383b46` | Left panel |
| `--bg-right` | `#fafbfd` | Right panel |
| `--input-border` | `#e5e5e5` | Input border |
| `--input-focus-border` | `#4da1ff` | Focus highlight |
| `--btn-primary-bg` | `#4da1ff` | Button |
| `--text-main` | `#222222` | Primary text |
| `--text-muted` | `#9a9a9a` | Secondary text |

### 4.3 Characters

| ID | Color | Shape | Animation |
|----|-------|-------|-----------|
| `char-blue` | `#6d63ff` | Flat-top parallelogram 190px | `float-blue` 4s |
| `char-orange` | `#fc8d70` | Arch R=70 | `breathe-orange` 3.5s |
| `char-black` | `#1f1f1f` | Rect 65×140 | `sway-black` 3s |
| `char-yellow` | `#eec53e` | Pill 70×120 | `bounce-yellow` 2.8s |

### 4.4 Component Specs

| Component | Spec |
|-----------|------|
| Input | h=46px, r=6px, icon 20×20 |
| Button | h=46px, r=6px, bg=#4da1ff |
| Icons | Inline SVG, stroke="currentColor" |

---

## 5. Premium (`login-premium.html`)

### 5.1 Overview

| Attribute | Value |
|-----------|-------|
| Title | Welcome — Sign in to continue |
| Vibe | Minimalist, luxurious, restrained |
| Signature | Dark background + particle rings + glassmorphism card |

### 5.2 Colors

| Usage | Value |
|-------|-------|
| Background | `#0f0f1a` |
| Primary accent | `#c9a96e` (Champagne gold) |
| Text | `#e8e4dc` (Warm white) |
| Secondary | `#8a8578` (Taupe) |
| Card | `rgba(255,255,255,0.04)` + frosted glass |

### 5.3 Characters (Crystal Geometry)

| ID | Shape | Color | Animation |
|----|-------|-------|-----------|
| `char-crystal1` | Diamond emerald | `rgba(180,200,180,0.6)` | `floatCrystal` 6s |
| `char-crystal2` | Rose gold triangle | `rgba(201,169,110,0.25)` | `shimmerCrystal` 5s |
| `char-crystal3` | Dark pillar | `rgba(60,60,80,0.7)` | `floatCrystal` 7s |
| `char-crystal4` | Warm amber | `rgba(200,160,100,0.35)` | `shimmerCrystal` 4.5s |

### 5.4 Signature Effects

- Three-layer particle rings with `ringPulse` breathing
- Background glow `ambientShift` slow drift
- Form card `backdrop-filter: blur(20px)` glassmorphism
- Hollow gold-border button → solid fill on hover

### 5.5 Component Specs

| Component | Spec |
|-----------|------|
| Input | Underline style, h=auto, border-bottom |
| Button | h=auto, p=15px, gold hollow border, letter-spacing=4px |
| Font | Cormorant Garamond / Noto Serif SC — serif, light weight |

---

## 6. Kids (`login-kids.html`)

### 6.1 Overview

| Attribute | Value |
|-----------|-------|
| Title | Hi there, little friend! Come explore a wonderful world |
| Vibe | Cheerful, soft, dreamy |
| Signature | Gradient sky + floating clouds + twinkling stars + chibi characters |

### 6.2 Colors

| Usage | Value |
|-------|-------|
| Sky top | `#87CEEB` |
| Sky bottom | `#f8e8ff` |
| Card | `rgba(255,255,255,0.85)` |
| Pink | `#FF6B9D` |
| Purple | `#C084FC` |
| Yellow | `#FBBF24` |
| Green | `#34D399` |
| Blue | `#60A5FA` |

### 6.3 Characters (Chibi Round)

| ID | Shape | Color | Animation |
|----|-------|-------|-----------|
| `char-pink` | Ellipse 75×95 | `#FF6B9D` | `bouncePink` 2.2s |
| `char-green` | Ellipse 65×55 | `#34D399` | `wiggleGreen` 2.8s |
| `char-blue-k` | Rounded rect 85×165 | `#60A5FA` | `bounceBlue` 2.5s |
| `char-yellow-k` | Ellipse 55×70 | `#FBBF24` | `danceYellow` 2s |

### 6.4 Signature Details

- Three floating clouds with `cloudFloat` drift
- Five stars with `starTwinkle` sparkle
- Character smiles with `smileBounce` elastic wiggle
- Eye highlight dots (white pupil reflections)
- Pink-purple gradient button with lift shadow

### 6.5 Component Specs

| Component | Spec |
|-----------|------|
| Input | h=50px, r=16px, border=2px, light purple bg |
| Button | h=52px, r=16px, pink-purple gradient, shadow |
| Font | Comic Sans MS / KaiTi — playful handwritten |

---

## 7. Student (`login-student.html`)

### 7.1 Overview

| Attribute | Value |
|-----------|-------|
| Title | Welcome back — Sign into your learning space |
| Vibe | Fresh, modern, energetic |
| Signature | Dark grid background + white card + geometric characters |

### 7.2 Colors

| Usage | Value |
|-------|-------|
| Left background | `#0F172A` → `#1E293B` gradient |
| Right background | `#f0f4f8` |
| Card | `#ffffff` + shadow |
| Cyan | `#0EA5E9` |
| Purple | `#8B5CF6` |
| Green | `#10B981` |
| Orange | `#F97316` |

### 7.3 Characters (Geometric Patchwork)

| ID | Shape | Color | Animation |
|----|-------|-------|-----------|
| `char-a` | Hexagon | `rgba(14,165,233,0.5)` | `levitate` 3.5s |
| `char-b` | Semi-circle | `rgba(139,92,246,0.4)` | `pulse` 3s |
| `char-c` | Slim rect | `rgba(16,185,129,0.45)` | `tilt` 3.8s |
| `char-d` | Rounded square | `rgba(249,115,22,0.45)` | `hop` 2.6s |

### 7.4 Signature Details

- Grid decoration background via `background-image` repeating linear gradients
- "Remember me" checkbox + "Forgot password?" link
- "Don't have an account? Sign up" call-to-action
- Input `focus-within` glow `box-shadow`
- Cyan-blue gradient button with offset shadow

### 7.5 Component Specs

| Component | Spec |
|-----------|------|
| Input | h=50px, r=12px, border=1.5px, light gray bg |
| Button | h=50px, r=12px, cyan-blue gradient, shadow |
| Font | Inter / PingFang SC — modern sans-serif |

---

## 8. Kids Pro (`login-pro.html`)

### 8.1 Overview

| Attribute | Value |
|-----------|-------|
| Title | Welcome to AI Academy — Learn and grow with four little sprites! |
| Vibe | Warm, encouraging, scholastic |
| Signature | Pink-purple gradient + character accessories + playful copy |

### 8.2 Colors

| Variable | Value | Usage |
|----------|-------|-------|
| `--bg-left` | `linear-gradient(#a18cd1, #fbc2eb)` | Pink-purple gradient |
| `--bg-right` | `#fff9fc` | Pale pink-white |
| `--input-border` | `#ffc6d1` | Pink border |
| `--input-focus-border` | `#f093fb` | Bright pink focus |
| `--btn-primary-bg` | `linear-gradient(#f6d365, #fda085)` | Warm orange gradient button |

### 8.3 Characters (Standard + Accessories)

| ID | Color | Accessory | Effect |
|----|-------|-----------|--------|
| `char-blue` | `#b79ad1` (lavender) | 🎓 Graduation cap + gold tassel | Tassel sways with float |
| `char-orange` | `#ffb8ba` (coral) | 👓 Round glasses + bridge | Scales with breathing |
| `char-black` | `#83bdf5` (sky blue) | 📖 White book + spine line | Rocks with sway |
| `char-yellow` | `#fce38a` (cream) | 🚀 Rocket backpack + smirk | Launches with bounce |

### 8.4 Signature Details

- Book SVG icon for username field (scholastic theme)
- Emoji-prefixed button "🚀 Start Learning"
- Footer: "A little progress each day, knowledge changes the future ✨"
- Pastel-softened character palette (reduced saturation, eye-friendly)

### 8.5 Component Specs

| Component | Spec |
|-----------|------|
| Input | h=52px, r=50px (pill), border=2px, pink-purple shadow |
| Button | h=52px, r=50px (pill), warm orange gradient, pink-orange shadow |
| Font | Comic Sans MS / Chalkboard SE / PingFang SC |

---

## 9. Animation System

### 9.1 Shared Animations

| Animation | Target | Standard/Pro | Premium | Kids | Student |
|-----------|--------|:-----------:|:-------:|:----:|:-------:|
| Blink | `.eye-*` | `blink` 4s | `blink` 5s | `blinkBig` 3.5s | `blinkGeom` 4s |
| Lean-in | `#characters-group` | stretch-neck | stretch-neck | stretch-neck | stretch-neck |
| Turn-away | `#characters-group` | turn-away | turn-away | turn-away | turn-away |

### 9.2 Per-Variant Character Animation Quick Reference

| Variant | Char 1 | Char 2 | Char 3 | Char 4 |
|---------|--------|--------|--------|--------|
| Standard/Pro | `float-blue` 4s | `breathe-orange` 3.5s | `sway-black` 3s | `bounce-yellow` 2.8s |
| Premium | `floatCrystal` 6s | `shimmerCrystal` 5s | `floatCrystal` 7s | `shimmerCrystal` 4.5s |
| Kids | `bouncePink` 2.2s | `wiggleGreen` 2.8s | `bounceBlue` 2.5s | `danceYellow` 2s |
| Student | `levitate` 3.5s | `pulse` 3s | `tilt` 3.8s | `hop` 2.6s |

### 9.3 Interaction Pause Rules (All Variants)

```
When stretch-neck / turn-away is active:
  → Character animations: animation-play-state: paused
  → Blink animations: animation-play-state: paused
  → Pupil tracking skipped during turn-away
```

---

## 10. Eye-Tracking System (V1.0 Optimized)

### 10.1 Architecture

```
Initialization:
  querySelectorAll('.pupil') → updateEyesCache()
  → Cached array of { cx, cy, range, el }

Runtime:
  mousemove / touchstart / touchmove
  → handleCoordMove(clientX, clientY)
  → turn-away? → return
  → eyesCache.forEach:
      dx = clientX - eye.cx
      dy = clientY - eye.cy
      dist = √(dx² + dy²)
      dist > range → clamp to range
      eye.el.style.transform = translate(dx, dy)

Refresh:
  window.addEventListener('resize', updateEyesCache)
```

### 10.2 Performance Metrics

| Metric | Before | After |
|--------|--------|-------|
| Reflows per frame | 8 (8 pupils) | 0 |
| Cache refresh trigger | — | resize / orientationchange |
| Touch events | passive: true | passive: true |

---

## 11. Technical Architecture

### 11.1 Technology Choices

| Decision | Rationale |
|----------|-----------|
| Pure static single file | Zero build, zero deploy, open directly in browser |
| CSS custom properties | Centralized theming, swap by changing variables |
| Inline SVG icons | Offline-capable, `currentColor` inheritance |
| Vanilla JS | No framework overhead, under 100 lines |
| CSS Animation | GPU-accelerated, non-blocking |
| `passive: true` | Touch events don't block scrolling |

### 11.2 Browser Compatibility

| Feature | Chrome | Firefox | Safari | Edge |
|---------|:------:|:-------:|:------:|:----:|
| CSS Variables | ✓ 49+ | ✓ 31+ | ✓ 9.1+ | ✓ 15+ |
| CSS Animation | ✓ 43+ | ✓ 16+ | ✓ 9+ | ✓ 12+ |
| `preserve-3d` | ✓ 36+ | ✓ 16+ | ✓ 9+ | ✓ 12+ |
| `currentColor` | ✓ | ✓ | ✓ | ✓ |
| `backdrop-filter` | ✓ 76+ | ✓ 103+ | ✓ 9+ | ✓ 17+ |
| `passive` events | ✓ 51+ | ✓ 49+ | ✓ 11.1+ | ✓ 15+ |

---

## 12. Color Quick Reference

### 12.1 Left Panel by Variant

| Variant | Background |
|---------|------------|
| Standard | `#383b46` solid |
| Premium | `#0f0f1a` + `radial-gradient` glow |
| Kids | `linear-gradient(#87CEEB, #f8e8ff)` sky |
| Student | `linear-gradient(#0F172A, #1E293B)` + grid |
| Pro | `linear-gradient(#a18cd1, #fbc2eb)` pink-purple |

### 12.2 Primary Button by Variant

| Variant | Button Style |
|---------|-------------|
| Standard | `bg=#4da1ff, r=6px` solid blue |
| Premium | `border=#c9a96e, bg=transparent` gold hollow |
| Kids | `linear-gradient(#FF6B9D, #C084FC), r=16px` pink-purple |
| Student | `linear-gradient(#0EA5E9, #38bdf8), r=12px` cyan-blue |
| Pro | `linear-gradient(#f6d365, #fda085), r=50px` warm orange |

---

## 13. Roadmap

### V1.1

- [ ] Client-side form validation (required, format, min-length)
- [ ] Login button loading state + API integration
- [ ] Enter key submission
- [ ] Toast error notifications

### V1.2

- [ ] i18n multi-language support
- [ ] Auto dark mode detection
- [ ] Accessibility (ARIA labels, keyboard nav, screen readers)
- [ ] Seasonal/holiday character themes

### V2.0

- [ ] Third-party login (Google / GitHub / WeChat)
- [ ] Dynamic backgrounds (WebGL particles)
- [ ] React / Vue component library versions
