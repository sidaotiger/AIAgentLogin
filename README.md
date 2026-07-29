# AIAgent 登录页

五套纯静态登录设计方案，零依赖，打开即用。共享眼动追踪交互引擎，覆盖通用/商务/儿童/学生场景。

## 快速选择

| 文件 | 风格 | 适合场景 | 一句话 |
|------|------|----------|--------|
| `login.html` | 标准版 | 通用 | 稳重灰蓝紫，专业亲和 |
| `login-premium.html` | 高端版 | 商务/品牌 | 暗夜香槟金，晶石极简 |
| `login-kids.html` | 儿童版 | 幼儿园/小学 | 天空彩虹云朵，圆圆大头 |
| `login-student.html` | 学生版 | 中学/大学 | 深色网格，几何拼接清新 |
| `login-pro.html` | 儿童Pro | 小学/教育机构 | 粉紫渐变，学士帽配饰 |

## 快速开始

```bash
# 直接浏览器打开任一版本
open login.html
open login-kids.html

# 或本地静态服务器
npx serve .
# 访问 http://localhost:3000/login.html
```

## 目录结构

```
LoginPage/
├── login.html              # 标准版
├── login-premium.html      # 高端美学版
├── login-kids.html         # 儿童版
├── login-student.html      # 学生版
├── login-pro.html          # 儿童Pro版（角色配饰）
├── docs/
│   ├── design-v0.1.md      # 设计文档 V0.1（存档）
│   └── design-v1.0.md      # 设计文档 V1.0（当前）
└── README.md
```

## 共享特性

- 🎭 四角色 SVG + 独立动画（漂浮/呼吸/摇摆/弹跳）
- 👁️ 眼动追踪（鼠标 + 触屏，瞳孔跟随）
- 🔐 密码可见切换（角色转身动画）
- 📱 响应式适配（768px 断点）
- 🚀 零 CDN 依赖（内联 SVG 图标）
- ♿ 支持缩放（无 `user-scalable=no`）
- ⚡ 瞳孔坐标缓存（`resize` 刷新，高频事件零重排）

## 部署

### Nginx

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/loginpage;
    index login.html;

    location / {
        try_files $uri $uri/ /login.html;
    }
}
```

### Docker

```dockerfile
FROM nginx:alpine
COPY *.html /usr/share/nginx/html/
EXPOSE 80
```

```bash
docker build -t loginpage .
docker run -d -p 8080:80 loginpage
```

### 静态托管

上传全部 `.html` 文件到任意服务即可：

- **GitHub Pages**：推送仓库 → Settings → Pages → root 目录
- **Vercel**：`npx vercel . --prod`
- **Netlify**：拖拽文件夹到 Netlify Drop

## 浏览器兼容

| Chrome | Firefox | Safari | Edge |
|--------|---------|--------|------|
| ✓ 90+  | ✓ 90+   | ✓ 14+  | ✓ 90+ |

## 技术栈

- HTML5
- CSS3（变量 + 动画 + 弹性布局 + 毛玻璃）
- 原生 JavaScript（眼动追踪引擎）
- 内联 SVG（图标 + 角色插画）
- 零外部依赖
