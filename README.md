<p align="center">
  <img src="https://img.shields.io/badge/version-1.0-6d63ff?style=flat-square" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-c9a96e?style=flat-square" alt="License">
  <img src="https://img.shields.io/badge/dependencies-zero-10B981?style=flat-square" alt="Dependencies">
  <img src="https://img.shields.io/badge/files-pure%20HTML-E34F26?style=flat-square" alt="HTML5">
</p>

<h1 align="center">🎨 AIAgent 登录页</h1>

<p align="center">
  <strong>五套纯静态登录设计方案</strong> · 零依赖 · 打开即用<br>
  共享眼动追踪交互引擎，覆盖通用 · 商务 · 儿童 · 学生场景
</p>

<br>

---

## 🧭 方案速览

<table>
<tr>
  <th width="18%">文件</th>
  <th width="14%">代号</th>
  <th width="22%">适合</th>
  <th width="30%">一眼识别</th>
  <th width="16%">Live</th>
</tr>
<tr>
  <td><code>login.html</code></td>
  <td>🔷 标准版</td>
  <td>通用场景</td>
  <td>灰蓝左面板 · 四色几何角色</td>
  <td align="center"><a href="https://sidaotiger.github.io/AIAgentLogin/login.html">预览</a></td>
</tr>
<tr>
  <td><code>login-premium.html</code></td>
  <td>🥂 高端版</td>
  <td>商务 · 品牌</td>
  <td>暗夜黑底 · 晶石 · 香槟金描边</td>
  <td align="center"><a href="https://sidaotiger.github.io/AIAgentLogin/login-premium.html">预览</a></td>
</tr>
<tr>
  <td><code>login-kids.html</code></td>
  <td>🌈 儿童版</td>
  <td>幼儿园 · 小学</td>
  <td>渐变天空 · 云朵星星 · 超萌大头</td>
  <td align="center"><a href="https://sidaotiger.github.io/AIAgentLogin/login-kids.html">预览</a></td>
</tr>
<tr>
  <td><code>login-student.html</code></td>
  <td>📐 学生版</td>
  <td>中学 · 大学</td>
  <td>深色网格 · 几何拼接 · 白色卡片</td>
  <td align="center"><a href="https://sidaotiger.github.io/AIAgentLogin/login-student.html">预览</a></td>
</tr>
<tr>
  <td><code>login-pro.html</code></td>
  <td>🎓 儿童 Pro</td>
  <td>小学 · 教育机构</td>
  <td>粉紫渐变 · 学士帽 · 配饰角色</td>
  <td align="center"><a href="https://sidaotiger.github.io/AIAgentLogin/login-pro.html">预览</a></td>
</tr>
</table>

---

## ✨ 核心亮点

<table>
<tr>
  <td width="50%">

### 🎭 四角色动画引擎
每个角色拥有独立个性和动画——漂浮、呼吸、摇摆、弹跳。标准版/Pro版角色佩戴学士帽、眼镜、书本、火箭等配饰，随动画联动。

### 👁️ 眼动追踪
8 个瞳孔实时跟随鼠标/手指移动，坐标缓存 + `resize` 刷新，高频事件零布局重排。

  </td>
  <td width="50%">

### 🔐 交互叙事
- 聚焦输入框 → 角色探头偷看
- 密码明文可见 → 角色集体转身
- 眨眼节奏错开，自然生动

### 📱 全平台适配
768px 断点自动切换上下布局，`touchstart` + `touchmove` 支持移动端瞳孔追踪，`passive: true` 不阻塞滚动。

  </td>
</tr>
</table>

---

## 🚀 快速开始

```bash
git clone https://github.com/sidaotiger/AIAgentLogin.git
cd AIAgentLogin

# 浏览器直接打开
open login.html

# 或本地服务器
npx serve .
```

---

## 📦 目录

```
AIAgentLogin/
├── login.html                 # 🔷 标准版
├── login-premium.html         # 🥂 高端美学版
├── login-kids.html            # 🌈 儿童版
├── login-student.html         # 📐 学生版
├── login-pro.html             # 🎓 儿童 Pro 版
├── docs/
│   ├── design-v1.0.md         # 设计文档（当前）
│   └── design-v0.1.md         # 设计文档（存档）
├── LICENSE                    # MIT 中英双语
└── README.md
```

---

## 🖥️ 部署

<details>
<summary><b>Nginx</b></summary>

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/loginpage;
    index login.html;
    location / { try_files $uri $uri/ /login.html; }
}
```
</details>

<details>
<summary><b>Docker</b></summary>

```dockerfile
FROM nginx:alpine
COPY *.html /usr/share/nginx/html/
EXPOSE 80
```

```bash
docker build -t loginpage .
docker run -d -p 8080:80 loginpage
```
</details>

<details>
<summary><b>静态托管</b></summary>

上传全部 `.html` 文件到任意服务即可运行：

| 平台 | 方式 |
|------|------|
| GitHub Pages | Settings → Pages → root 目录 |
| Vercel | `npx vercel . --prod` |
| Netlify | 拖拽文件夹到 Netlify Drop |
| OSS / COS | 上传至云存储桶，开启静态网站托管 |
</details>

---

## 🛠️ 技术栈

| 层 | 技术 | 说明 |
|----|------|------|
| 结构 | HTML5 | 语义化标签 |
| 样式 | CSS3 | 变量 · 动画 · Flexbox · 毛玻璃 · `preserve-3d` |
| 逻辑 | Vanilla JS | 眼动追踪引擎 · 状态机 · 事件缓存 |
| 图形 | 内联 SVG | 角色插画 · 图标 · `currentColor` 继承 |
| 依赖 | **零** | 无 CDN · 无框架 · 无构建 |

## 🌐 兼容性

| Chrome | Firefox | Safari | Edge |
|:------:|:-------:|:------:|:----:|
| 90+ ✅ | 90+ ✅ | 14+ ✅ | 90+ ✅ |

---

<p align="center">
  <sub>Made with ❤️ · MIT License · <a href="https://github.com/sidaotiger/AIAgentLogin">GitHub</a></sub>
</p>
