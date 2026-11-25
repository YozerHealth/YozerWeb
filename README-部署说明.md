# Yozer 官网 · GitHub Pages 部署说明

本目录是一个**纯静态站点**，可直接作为 GitHub 仓库内容发布到 GitHub Pages。
`index.html` 及所有页面均位于根目录，无任何后端函数、无云依赖、无访问统计。

## 目录内容
- 34 个 `.html` 页面：三级结构
  - 一级：`index.html`（首页，仅"手机应用 / 电子书"两大入口）
  - 二级：`apps.html`（4 款 App 列表）、`ebooks.html`（24 本电子书列表）
  - 三级：4 个 App 介绍页 + 24 本电子书介绍页 + 隐私/下载等
- `assets/` — 脚本、样式、图片、24 本电子书封面与试读图
- `apks/` — 3 个安装包（约 58 MB，含断点续传支持由 GitHub Pages CDN 提供）
- `.nojekyll` — 禁用 Jekyll 处理，确保资源原样发布

## 发布步骤
1. 在 GitHub 新建一个仓库（例如 `yozer-site`，公开）。
2. 把**本目录内的所有内容**（含隐藏文件 `.nojekyll`）上传到仓库根目录，不要套一层子文件夹。
   - 网页端：进入仓库 → `Add file` → `Upload files` → 全选本目录文件拖入。
   - 或命令行：在本目录执行
     ```
     git init
     git add -A
     git commit -m "Yozer static site"
     git remote add origin https://github.com/<你的用户名>/yozer-site.git
     git branch -M main
     git push -u origin main
     ```
3. 仓库 → `Settings` → `Pages` → Build and deployment：
   - Source 选 `Deploy from a branch`
   - Branch 选 `main` / `/ (root)` → Save。
4. 等待部署完成，访问地址形如 `https://<你的用户名>.github.io/yozer-site/`。

## 路径说明（重要）
- 站内所有资源与页面链接均为**相对路径**（如 `assets/site.js`、`yozerhealth.html`、`apks/xxx.apk`），
  因此无论部署在 `用户名.github.io/仓库名/` 子路径，还是绑定自定义域名后的根路径，都能正确解析。
- 若使用自定义域名：在仓库根目录新增一个无扩展名文件 `CNAME`，内容为你的域名（如 `www.example.com`），
  并在域名 DNS 配置 CNAME 指向 `<用户名>.github.io`。此时相对路径依然有效。

## 后续更新 APK 时
1. 替换 `apks/` 下的安装包。
2. 编辑 `assets/site.js` 顶部的 `META` 常量（版本、文件名、大小、SHA-256、时间）。
3. 编辑 `yozerhealth.html` 中的下载直链文件名（共 5 处 `apks/...`）。
4. `download.html` 内的两处版本/体积文案也需同步。
