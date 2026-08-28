# Kisama Panel · Cloudflare Pages 部署指南

本项目是一个**纯静态站点**：仓库根目录直接包含 `index.html`、图标资源（`favicon.svg`、`icons.svg`）以及编译后的 `assets/` 目录。无需任何构建步骤，可直接免费部署到 [Cloudflare Pages](https://pages.cloudflare.com/)。

下文以本仓库 `deploy-kisama-panel` 为例，演示从 Fork 到上线的完整流程。

---

## 一、前置准备

### 1. Fork 本仓库到自己的 GitHub 账号

1. 打开源仓库：<https://github.com/liveqte/deploy-kisama-panel>
2. 点击右上角 **Fork**，选择你自己的 GitHub 账号，创建一个属于你的副本。
3. Fork 完成后，你会在自己的账号下得到 `你的用户名/deploy-kisama-panel`。

> 后续所有部署都基于你 Fork 后的副本，便于你自己修改与更新。

### 2. 授权 Cloudflare Pages 访问 GitHub

1. 打开 [Cloudflare Dashboard](https://dash.cloudflare.com/) → 左侧 **Workers 和 Pages** → **创建** → **Pages** → **连接到 Git**。
2. 在「连接到 Git 提供商」中选择 **GitHub**，按提示点击 **Authorize Cloudflare Pages / Install**（授权 / 安装）。
3. 在 GitHub 的授权页面中，允许 Cloudflare Pages 访问你的账号（至少需要能读取你刚 Fork 的 `deploy-kisama-panel` 仓库；建议直接授予 `All repositories` 或单独勾选该仓库）。

> 如果你在后续「选择存储库」步骤中看不到仓库，说明授权范围不够，回到 GitHub → **Settings → Applications → Cloudflare Pages** 调整仓库访问权限即可。

---

## 二、部署步骤（3 步）

进入 Cloudflare Pages 的「创建应用程序」向导，顶部进度条为：**1 选择存储库 → 2 设置构建和部署 → 3 部署站点**。

### 步骤 1 / 3：选择存储库

- 来源选择 **GitHub**（如需也可选 GitLab）。
- 确认 GitHub 账号为你的账号（例如 `你的用户名`）。
- 在「选择一个存储库」中搜索并选中 **`deploy-kisama-panel`**。
- 点击 **开始设置**。

### 步骤 2 / 3：设置构建和部署

按下表填写构建配置（本项目是静态文件，无需构建命令）：

| 配置项 | 填写值 | 说明 |
| --- | --- | --- |
| 项目名称 | `deploy-kisama-panel` | 可自定义，会决定 `*.pages.dev` 子域名 |
| 生产分支 | `master` | 仓库的默认分支 |
| 框架预设 | **无** | 纯静态，不使用框架 |
| 构建命令 | **（留空）** | 不需要打包 |
| 构建输出目录 | **`/`** （根目录） | `index.html` 位于仓库根目录 |

其余「根目录（高级）」「环境变量（高级）」保持默认即可。

确认后点击 **保存并部署**。

### 步骤 3 / 3：部署站点

- Cloudflare 会自动拉取 `master` 分支并发布，页面提示：**成功！您的项目已部署到以下区域：全球**。
- 预览地址为：`https://deploy-kisama-panel.pages.dev`（其中 `deploy-kisama-panel` 为你设置的项目名）。
- 点击 **查看构建日志** 可查看部署详情；**添加自定义域** 可绑定你自己的域名。

---

## 三、访问与后续维护

- **默认访问地址**：`https://<项目名>.pages.dev`
- **自动部署**：之后只要向 Fork 后仓库的 `master` 分支 `push` 新提交，Cloudflare Pages 会自动重新构建并上线，无需手动操作。
- **自定义域名**：在 Pages 项目 → **自定义域** 中按提示添加并配置 DNS（CNAME 指向 `*.pages.dev` 或由 Cloudflare 自动托管）。
- **本地调试**：可安装 [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install/)（`npm install -g wrangler && wrangler pages dev .`）在本地预览根目录站点。
