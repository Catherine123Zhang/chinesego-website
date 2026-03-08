# ChineseGo 官网部署指南

## 网站文件结构

```
EasyTravelChineseWebsite/
├── index.html          # 主页（落地页）
├── privacy.html        # 隐私政策
├── terms.html          # 服务条款
├── support.html        # 技术支持
├── CNAME               # 自定义域名配置
└── assets/
    └── images/
        ├── logo_1024.png
        ├── logo.png
        ├── logo-dark.png
        └── logo-dark-inner.png
```

---

## 部署方案

### 方案一：Namecheap 静态托管（推荐）

由于域名 `chinesego.app` 在 Namecheap 上，最简单的方式是使用 Namecheap 的静态网站托管。

#### 步骤：

1. **登录 Namecheap 控制面板**
   - 访问 https://www.namecheap.com/myaccount/login/

2. **进入域名管理**
   - Dashboard → Domain List → `chinesego.app` → Manage

3. **上传网站文件**
   - 使用 Namecheap 的 cPanel File Manager
   - 将所有文件上传到 `public_html` 目录：
     - `index.html`
     - `privacy.html`
     - `terms.html`
     - `support.html`
     - `assets/` 文件夹（包含图片）

4. **SSL 证书配置**
   - `.app` 域名**强制要求 HTTPS**
   - 在 Namecheap cPanel 中启用免费 SSL（Let's Encrypt 或 PositiveSSL）
   - 路径: cPanel → SSL/TLS → Install SSL Certificate

5. **验证**
   - 访问 https://chinesego.app 确认网站正常显示

---

### 方案二：GitHub Pages + Namecheap DNS

如果你更习惯用 Git 管理，这也是个好选择。

#### 步骤：

1. **创建 GitHub 仓库**
   ```bash
   cd /Users/changvivian/Documents/AI/EasyTravelChineseWebsite
   git init
   git add .
   git commit -m "Initial commit: ChineseGo landing page"
   ```

2. **推送到 GitHub**
   ```bash
   gh repo create chinesego-website --public
   git push -u origin main
   ```

3. **启用 GitHub Pages**
   - 仓库 Settings → Pages
   - Source: Deploy from a branch
   - Branch: `main` / `root`
   - Save

4. **在 Namecheap 配置 DNS**

   进入 Namecheap 域名管理 → Advanced DNS，添加以下记录：

   | Type  | Host | Value               | TTL  |
   |-------|------|---------------------|------|
   | A     | @    | 185.199.108.153     | Auto |
   | A     | @    | 185.199.109.153     | Auto |
   | A     | @    | 185.199.110.153     | Auto |
   | A     | @    | 185.199.111.153     | Auto |
   | CNAME | www  | yourusername.github.io | Auto |

5. **在 GitHub Pages 设置自定义域名**
   - Settings → Pages → Custom domain: `chinesego.app`
   - 勾选 "Enforce HTTPS"

6. **等待 DNS 生效**（通常 5-30 分钟，最长 48 小时）

---

### 方案三：Cloudflare Pages（推荐用于性能优化）

Cloudflare Pages 提供免费的全球 CDN 加速。

#### 步骤：

1. 将代码推送到 GitHub
2. 登录 Cloudflare Dashboard
3. Pages → Create a project → Connect to Git
4. 选择仓库，构建设置留空（纯静态文件）
5. 在 Namecheap 将 DNS nameservers 改为 Cloudflare 提供的
6. 在 Cloudflare 中添加自定义域名 `chinesego.app`

---

## 重要提醒

### `.app` 域名 HTTPS 要求
- `.app` 是 Google 管理的 HSTS 顶级域名
- **所有 `.app` 域名强制要求 HTTPS**
- 部署前必须确保 SSL 证书已正确配置
- GitHub Pages 和 Cloudflare Pages 都自动提供免费 SSL

### App Store 链接
- 网站中的 App Store 下载链接已配置为：`https://apps.apple.com/us/app/chinesego-travel-chinese/id6758551531`

### SEO 注意事项
- `index.html` 已包含 Open Graph 标签和 meta description
- 建议上线后提交 sitemap 到 Google Search Console
- 可以后续添加 `robots.txt` 和 `sitemap.xml`

---

## 联系方式
- Email: zhangyuanbo123@gmail.com
- 管家电话: +86 182 6866 1068
