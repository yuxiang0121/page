# GitHub Pages 静态网页部署指南

本文说明如何把当前目录下的 `index.html` 通过 GitHub Pages 发布成一个公网可访问的网页。

## 最终效果

部署完成后访问 `https://<用户名>.github.io/<仓库名>/` 即可看到 "Hello World" 页面。

## 文件说明

| 文件 | 作用 |
| --- | --- |
| `index.html` | 网页本体。GitHub Pages 默认把 `index.html` 当作首页入口，文件名必须为 `index.html` |
| `GitHub-Pages部署指南.md` | 本文档 |

## 操作步骤

### 1. 创建 GitHub 仓库

1. 打开 https://github.com/new
2. Repository name 填一个名字，例如 `hello-pages`
3. 选择 Public（GitHub Pages 免费版要求仓库公开）
4. **不要**勾选 "Add a README file"，保持仓库为空，方便本地推送
5. 点击 Create repository

### 2. 本地初始化并推送

在本目录执行（`main` 为默认分支名，如本地默认是 `master` 请自行替换）：

```bash
git init
git add index.html GitHub-Pages部署指南.md
git commit -m "Add hello world page"

git branch -M main
git remote add origin https://github.com/<用户名>/<仓库名>.git
git push -u origin main
```

如果本地 git 还没配置身份，先执行一次：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

### 3. 开启 GitHub Pages

1. 打开仓库页面 → **Settings** → 左侧 **Pages**
2. **Build and deployment** → **Source** 选择 **Deploy from a branch**
3. **Branch** 选择 `main`，目录选择 `/ (root)`
4. 点击 **Save**

### 4. 等待并访问

保存后页面顶部会出现提示 "Your site is live at https://<用户名>.github.io/<仓库名>/"。

首次发布通常需要等 1–3 分钟，之后再推送代码一般几十秒内生效。看到提示后刷新浏览器即可。

## 后续更新网页

修改 `index.html` 后重新提交推送，GitHub Pages 会自动重新部署：

```bash
git add index.html
git commit -m "Update page"
git push
```

## 常见问题

**访问 404**

- 确认 Settings → Pages 里分支选的是 `main`、目录选的是 `/ (root)`
- 确认首页文件名是 `index.html`，不是 `home.html` 之类
- 首次发布后等待几分钟再试；强制刷新浏览器（Ctrl + F5）绕开缓存
- 检查 Actions 标签页里的 `pages build and deployment` 工作流是否为绿色

**仓库是 Private**

免费账号的 GitHub Pages 只对 Public 仓库生效（GitHub Pro 及以上支持私有仓库）。把仓库设为 Public 即可：Settings → General → Danger Zone → Change repository visibility。

**想让地址不带仓库名**

把仓库命名为 `<用户名>.github.io`（用户名必须完全一致，小写），然后用同样的方式发布，地址就是 `https://<用户名>.github.io/`。

## 本地预览

推送前可以先在本地看效果：

```bash
# 方式一：直接双击打开 index.html
# 方式二：起一个本地服务（推荐，避免缓存问题）
python3 -m http.server 8000
# 然后浏览器访问 http://localhost:8000
```
