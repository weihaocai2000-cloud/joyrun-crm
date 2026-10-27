# JOYRUN CRM (前端)

JOYRUN CRM 的网页应用前端。**本仓库是源码唯一真源（source of truth）**，不再依赖任何单台开发机。

## 技术形态
- 单文件 `index.html`：内联 CSS + 内联 JS，引入 WorkBuddy cloud SDK（`@tencent-ai/workbuddy-cloud-sdk`）做云端数据同步。
- 通过 Lark 开发者后台「网页应用」挂载，主页地址指向本仓库部署出的 URL。

## 本地预览
```bash
cd joyrun-crm
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

## 部署（推送即上线）
1. 在 GitHub 新建仓库，开启 **Settings → Pages → Source: GitHub Actions**。
2. 首次把本仓库推到 `main` 分支，GitHub Actions 会自动部署到 GitHub Pages。
3. 复制 Pages 地址（`https://<用户名>.github.io/<仓库名>/`），填回
   Lark 开发者后台 → JOYRUN CRM → 应用能力 → 网页应用 → **主页地址**，发一版新版本即可。

## 日常更新流程（不再需要 Mac）
```bash
git add index.html
git commit -m "fix: settings 页面自适应 v26"
git push origin main
# → GitHub Actions 自动重新部署，Lark 客户端刷新即更新
```

## 版本号
`index.html` 顶部 `var BUILD = 'NN'` 控制前端缓存穿透（cache-bust）。每次发布改一次数字即可强制客户端刷新。

## ⚠️ 切主机时的数据注意事项
本应用数据走 WorkBuddy cloud SDK，登录后数据绑定在用户会话上、与前端托管域名无关——但首次切换到新地址后，请先抽验 Customers / Members 等数据是否完整，确认无误再弃用旧地址（`https://joyrun-crm.app.workbuddy.host`）。如数据异常，旧地址仍可用作回滚。
