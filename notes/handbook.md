# Atlas 前端学习手册（第 1～2 天）

- 覆盖日期：2026-11-04 ～ 2026-11-05
- 用途：复习、查命令、避免重复踩坑
- 当前进度：Phase 0 Week 1，静态 HTML + 表单 + GitHub Pages
- 还没学：CSS、JavaScript、React、Go、MySQL

---

## 0. 一句话总览

> VS Code 写文件 → 浏览器看效果 → Git 存快照 → GitHub 备份 → GitHub Pages 给外网看。

---

## 1. 每天的工作流

### 开始

1. 打开 VS Code 的 `atlas` 文件夹
2. 按 `` Ctrl+` `` 打开集成终端
3. 运行 `git status`，确认 `working tree clean`
4. 看今天的任务

### 学习中

- 改文件 → `Ctrl+S` 保存 → 浏览器刷新
- 卡住 15～20 分钟再看提示
- 卡住 30 分钟，记录“报错 + 已试过什么”，再求助
- 每 45～60 分钟起身休息 5～10 分钟

### 结束

```powershell
git status          # 看有哪些改动
git diff            # 看具体改了什么
git add .           # 放进暂存区
git status          # 确认已暂存
git commit -m "feat: 今天做了什么"
git push            # 推到 GitHub
git log --oneline   # 确认历史
```

然后写日志：

```text
atlas/notes/YYYY-MM-DD.md
```

再提交日志：

```powershell
git add notes/YYYY-MM-DD.md
git commit -m "docs: add day N log"
git push
```

### 每天最低线

- 一个可见进展：页面变化、可验证行为、可复用代码、合并的 PR 或有质量的 review
- 一次有意义的 commit
- 一段 3～5 行日志

---

## 2. 终端与路径

| 命令 | 作用 |
|---|---|
| `cd "路径"` | 进入文件夹 |
| `cd ..` | 回到上一级 |
| `cd ~` | 回到用户目录 |
| `pwd` 或 `Get-Location` | 看当前目录 |
| `ls` 或 `Get-ChildItem` | 列出当前目录文件 |
| `Clear-Host` 或 `cls` | 清屏 |

### 规则

- 路径有中文或空格时，用引号包起来：`cd "C:\Users\91474\Documents\默认项目\atlas"`
- 命令和参数之间必须有空格：`cd "C:\..."`，不是 `cd"C:\..."`
- 输入路径时按 `Tab` 可以自动补全
- PowerShell 的提示符会显示当前目录
- VS Code 集成终端按 `` Ctrl+` `` 打开，默认在项目目录

### 常见错误

| 报错 | 原因 | 解决 |
|---|---|---|
| `fatal: not a git repository` | 不在仓库目录 | 先 `cd` 到 `atlas` |
| `找不到路径 ...\atla` | 路径拼写错误 | 用 Tab 补全 |
| `无法将“cdC:\...”项识别为...` | `cd` 和引号之间少了空格 | 写成 `cd "C:\..."` |

---

## 3. Git 核心概念

### 三个区域

| 区域 | 是什么 | 对应命令 |
|---|---|---|
| 工作区 | 你正在改的文件 | 直接编辑 |
| 暂存区 | 准备提交的内容 | `git add` |
| 仓库 | 已经提交的历史 | `git commit` |

### 核心词

- **仓库（repository）**：项目里的 `.git` 文件夹，保存全部历史
- **提交（commit）**：一次快照 + 信息 + 作者 + 时间
- **分支（branch）**：一条提交历史线；`main` 是默认主线
- **HEAD**：当前所在的最新提交
- **提交 ID**：如 `659db9c`，短哈希
- **远程仓库（remote）**：GitHub 上的副本，默认名字叫 `origin`
- **`origin/main`**：远程仓库里的 `main` 分支

### 命令表

| 命令 | 作用 |
|---|---|
| `git init` | 初始化仓库 |
| `git branch -M main` | 把当前分支改名为 `main` |
| `git status` | 看当前状态 |
| `git diff` | 看未暂存的改动 |
| `git add <file>` | 暂存指定文件 |
| `git add .` | 暂存当前目录所有改动 |
| `git commit -m "说明"` | 提交快照 |
| `git log --oneline` | 看提交历史 |
| `git show --stat HEAD` | 看最近一次提交改了哪些文件 |
| `git remote add origin <url>` | 添加远程仓库 |
| `git remote -v` | 查看远程地址 |
| `git push -u origin main` | 首次推送并设置上游分支 |
| `git push` | 后续推送 |
| `git pull` | 拉取远程更新（以后会用） |

### commit 和 push 的区别

- `commit`：在本地生成快照，不上传
- `push`：把本地新提交同步到 GitHub
- `push` 不是覆盖；如果远程有你没有的提交，push 会被拒绝，先 `pull`
- `git push -f` 是强制覆盖，危险，初学阶段不要用

### 提交信息前缀

| 前缀 | 用途 |
|---|---|
| `feat:` | 新功能 |
| `fix:` | 修 bug |
| `docs:` | 文档、日志 |
| `style:` | 样式、格式 |
| `refactor:` | 重构 |
| `chore:` | 工具、初始化 |

### 读 push 输出

| 输出 | 意思 |
|---|---|
| `[main 659db9c]` | 提交成功，在 `main` 分支，提交 ID 是 `659db9c` |
| `1 file changed, 10 insertions(+)` | 改了 1 个文件，新增 10 行 |
| `A..B main -> main` | 远程 `main` 从旧提交 A 更新到新提交 B |
| `Enumerating / Counting / Compressing / Writing` | Git 内部工作日志，成功时不用逐行看 |
| `remote: ...` | GitHub 那边返回的消息 |

---

## 4. GitHub 与部署

### 关系

- **GitHub**：远程代码托管平台
- **`git push`**：把代码上传到 GitHub
- **GitHub Pages**：GitHub 自带的静态网站托管

### 部署链路

```text
本地文件
  ↓ git add + commit
本地 Git 历史
  ↓ git push
GitHub 仓库
  ↓ 开启 GitHub Pages
公网 URL：https://用户名.github.io/仓库名/
```

### 开启 GitHub Pages

1. 打开仓库的 **Settings → Pages**
2. Source 选 **Deploy from a branch**
3. Branch 选 `main`
4. 目录选 `/ (root)`
5. 点 **Save**
6. 等 1～2 分钟
7. 打开 `https://<用户名>.github.io/<仓库名>/`

### 注意

- 免费版需要 public 仓库
- 第一次部署可能要等几分钟，404 先刷新
- GitHub Pages 只托管静态文件（HTML/CSS/JS），不能跑 Go、MySQL 等后端
- 全栈以后需要：前端 Vercel/Netlify，后端 Fly.io/Railway/Render 或云服务器
- 本地改完要 `commit` + `push`，线上才会更新

### 本地与线上

| 环境 | 地址 | 用途 |
|---|---|---|
| 本地 | `file:///C:/.../atlas/index.html` | 开发时快速看 |
| 线上 | `https://adele39.github.io/atlas/` | 给别人看 |

---

## 5. HTML 基础

### 最小文档结构

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Atlas 交易活动</title>
</head>
<body>
  ...
</body>
</html>
```

| 部分 | 作用 |
|---|---|
| `<!DOCTYPE html>` | 声明这是 HTML5 文档 |
| `<html lang="zh-CN">` | 根元素，`lang` 表示语言 |
| `<head>` | 给浏览器看的信息，不显示在页面上 |
| `<meta charset="UTF-8">` | 字符编码，避免中文乱码 |
| `<meta name="viewport" ...>` | 手机适配 |
| `<title>` | 浏览器标签页标题 |
| `<body>` | 用户能看到的内容 |

### 标签、元素、属性

- **标签**：`<h1>` 是开始标签，`</h1>` 是结束标签
- **元素**：开始标签 + 内容 + 结束标签，例如 `<h1>标题</h1>`
- **属性**：写在开始标签里的键值对，例如 `id="hero"`、`href="#faq"`、`type="email"`
- **空元素**：`<input>`、`<img>`，没有结束标签

### 属性写法

```html
<input id="name" name="name" type="text" required>
```

- 标签名和第一个属性之间：必须有空格
- 属性之间：必须有空格
- 属性名、`=`、值之间：习惯上不加空格
- 引号内的空格是值的一部分：`class="btn primary"`
- 布尔属性出现即真，不需要值：`required`、`disabled`、`checked`、`selected`

### 语义标签

| 标签 | 作用 |
|---|---|
| `header` | 页头 |
| `nav` | 导航区域，里面放链接 |
| `main` | 主内容 |
| `section` | 有主题的内容块，通常有标题 |
| `footer` | 页脚 |
| `div` | 无语义容器，只用于分组/排版 |

判断：**有标题、是页面独立的一部分 → `section`；只为分组/排版 → `div`。**

### 常用内容标签

| 标签 | 作用 |
|---|---|
| `h1` | 主标题，整页只用一个 |
| `h2` | 区块标题 |
| `h3` | 子标题、FAQ 问题 |
| `p` | 段落 |
| `a` | 链接 |
| `ul` / `li` | 无序列表 / 列表项 |
| `form` | 表单 |
| `label` | 输入框说明 |
| `input` | 输入框 |
| `button` | 按钮 |

### 标题层级

- 一个 `h1`
- 每个 section 一个 `h2`
- 子问题用 `h3`
- 不跳级，例如不要 `h1` 直接到 `h3`

### id 与 href

```html
<nav>
  <a href="#campaign">活动规则</a>
</nav>

<section id="campaign">...</section>
```

- `id` 是页面内唯一标识
- `href="#campaign"` 跳到 `id="campaign"` 的元素
- `href="campaign"` 会去找一个叫 `campaign` 的文件，不是页面内跳转
- 页面内跳转必须带 `#`

### 注释

```html
<!-- 这是注释，不会显示在页面上 -->
```

---

## 6. 表单与可访问性

### 基本结构

```html
<form id="register-form">
  <div>
    <label for="name">姓名</label>
    <input id="name" name="name" type="text" required minlength="2" autocomplete="name">
  </div>

  <button type="submit">提交报名</button>
</form>
```

### label 的两种关联

1. `for="name"` 对应 `input id="name"`（推荐）
2. 把 `input` 放进 `label` 里面

作用：点 label 文字能聚焦输入框；读屏软件能读出输入框名称。

### 常用 input 属性

| 属性 | 作用 |
|---|---|
| `type="text"` | 单行文本 |
| `type="email"` | 邮箱，浏览器会校验格式 |
| `type="checkbox"` | 复选框 |
| `required` | 必填，布尔属性 |
| `minlength="10"` | 最少字符数 |
| `maxlength="100"` | 最多字符数 |
| `autocomplete="name"` | 提示浏览器这是姓名字段 |
| `autocomplete="email"` | 提示浏览器这是邮箱字段 |
| `autocomplete="off"` | 不自动填充 |
| `spellcheck="false"` | 关闭拼写检查 |
| `aria-describedby="hint-id"` | 关联提示文字 |
| `name` | 提交表单时的字段名 |
| `id` | 页面内唯一标识，给 label/CSS/JS 用 |

### id 和 name 的区别

- `id`：页面内唯一，给 `label for`、CSS、JavaScript 用
- `name`：提交表单时的字段名

### aria-describedby 是什么

```html
<input id="wallet" name="wallet" type="text" required minlength="10"
       aria-describedby="wallet-hint">
<p id="wallet-hint">仅用于活动登记演示，不会发起交易。</p>
```

- 输入框写 `aria-describedby="wallet-hint"`
- 提示文字写 `id="wallet-hint"`
- 两者名字必须一致
- 读屏软件聚焦输入框时，会读“名称 + 角色 + 状态 + 描述”
- 它不影响页面外观，只影响辅助技术
- 不加也能视觉显示，但读屏用户可能听不到提示

### 表单测试清单

- 点每个 label，光标能跳到对应输入框
- Tab 顺序：姓名 → 邮箱 → 钱包 → 同意 → 提交
- 空表单提交被拦
- 邮箱填 `abc` 被拦
- 未勾选同意被拦
- 点“我同意活动规则”能切换复选框
- 375px 下不溢出（等 CSS 做完再测）
- DevTools Accessibility 面板能看到 Name 和 Description

---

## 7. 浏览器与调试

### 打开本地页面

```powershell
Start-Process index.html
```

### DevTools

- `F12` 或 `Ctrl+Shift+I` 打开
- **Console**：看报错、运行 JavaScript
- **Elements**：看 HTML 结构和样式
- **Accessibility**：看可访问名称和描述
- **Network**：看请求（后面学 fetch 时用）

### 首次粘贴代码被拦

Chrome 会提示“请勿将您不理解或未自行检查的代码粘贴到控制台”。在 Console 输入：

```text
allow pasting
```

或中文：

```text
允许粘贴
```

按 Enter 后即可粘贴。这是安全保护，不是报错。

### 常用检查代码

标题大纲：

```js
[...document.querySelectorAll('h1,h2,h3')].map(h => h.tagName + ' ' + h.textContent.trim())
```

表单 label 检查：

```js
[...document.querySelectorAll('input, select, textarea')].map(el => ({
  name: el.name || el.id,
  labels: el.labels.length
}))
```

横向溢出检查：

```js
({ viewport: innerWidth, content: document.documentElement.scrollWidth })
```

Expected：`content <= viewport`。

---

## 8. 常见错误速查

| 现象 | 原因 | 解决 |
|---|---|---|
| `fatal: not a git repository` | 不在仓库目录 | `cd` 到 `atlas` |
| `nothing to commit, working tree clean` | 没有改动，或已经提交 | 先改文件，`git status` 确认 |
| `找不到路径 ...\atla` | 路径拼写错 | 用 Tab 补全 |
| `cd"C:\..."` 无法识别 | `cd` 和引号之间少空格 | `cd "C:\..."` |
| 页面没变化 | 没保存或没刷新 | `Ctrl+S` + `Ctrl+R` |
| 页面上看不到 `hero` | `id` 不是可见文字 | 正常，`id` 不显示 |
| 复选框变成文本框 | `type="check box"` 有空格 | 改成 `type="checkbox"` |
| 邮箱不校验 | 缺少 `type="email"` | 补上 |
| `minlength` 不生效 | 拼成 `minilength` | 改成 `minlength` |
| 导航点了不跳 | `href="faq"` 少 `#` | `href="#faq"` |
| 控制台粘贴被拦 | Chrome 安全保护 | 输入 `allow pasting` |
| `git push` 被拒绝 | 远程有本地没有的提交 | 先 `git pull`，不要用 `-f` |
| GitHub Pages 404 | 第一次部署还没完成 | 等 1～2 分钟再刷新 |

---

## 9. 术语表

| 英文 | 中文 | 一句话 |
|---|---|---|
| repository | 仓库 | 存项目历史的地方 |
| commit | 提交 | 一次快照 |
| branch | 分支 | 一条历史线 |
| main | 主分支 | 默认稳定线 |
| remote | 远程仓库 | GitHub 上的副本 |
| origin | 远程名 | 默认叫 `origin` |
| push | 推送 | 本地 → 远程 |
| pull | 拉取 | 远程 → 本地 |
| staging area | 暂存区 | `add` 之后、`commit` 之前 |
| working tree | 工作区 | 正在改的文件 |
| HEAD | 当前提交指针 | 你站在哪 |
| tag | 标签 | `<h1>` 这种 |
| element | 元素 | 开始标签 + 内容 + 结束标签 |
| attribute | 属性 | 标签里的键值对 |
| id | 唯一标识 | 页面内唯一 |
| class | 类名 | 可以有多个，给 CSS 用 |
| semantic | 语义化 | 标签表达内容含义 |
| accessibility | 可访问性 | 让所有人能用 |
| screen reader | 读屏软件 | 把页面读出来 |
| anchor | 锚点 | 页面内跳转 |
| validation | 校验 | 检查输入是否有效 |
| deployment | 部署 | 把网站放到公网 |

---

## 10. 自测题

先自己回答，再看下面的答案。

1. `Ctrl+S` 和 `git commit` 的区别？
2. `git add` 做了什么？暂存区在哪？
3. `commit` 和 `push` 的区别？
4. `main` 是什么？`HEAD -> main` 什么意思？
5. `git status` 显示 `working tree clean` 说明什么？
6. `section` 和 `div` 的区别？
7. `id` 和 `name` 的区别？
8. `label` 的 `for` 和 `input` 的 `id` 为什么要一致？
9. `href="#faq"` 和 `href="faq"` 的区别？
10. `required` 为什么没有等号？
11. `aria-describedby` 解决什么问题？
12. `type="email"` 和 `type="text"` 的区别？
13. GitHub Pages 是什么？它能不能跑 Go 后端？
14. 本地能打开、线上打不开，先检查什么？

### 参考答案

1. `Ctrl+S` 把当前文件写到磁盘；`commit` 把项目状态存成 Git 历史快照。
2. `add` 把改动放进暂存区；暂存区是“准备提交”的区域。
3. `commit` 在本地生成快照；`push` 把本地新提交同步到 GitHub。
4. `main` 是默认主线分支；`HEAD -> main` 表示当前在 `main` 的最新提交上。
5. 没有未提交的改动，工作区和最新提交一致。
6. `section` 是有主题的内容块，通常有标题；`div` 是无语义容器，用于分组/排版。
7. `id` 是页面内唯一标识，给 label/CSS/JS 用；`name` 是提交表单时的字段名。
8. 这样点 label 能聚焦输入框，读屏软件也能正确读出名称。
9. `#faq` 跳到当前页面 `id="faq"` 的位置；`faq` 会去找一个叫 faq 的文件。
10. `required` 是布尔属性，出现即真，不需要值。
11. 把输入框和提示文字关联起来，让读屏软件在聚焦时读出提示。
12. `type="email"` 会校验邮箱格式；`type="text"` 不校验格式。
13. GitHub Pages 是静态网站托管；不能跑 Go 后端，也不能连 MySQL。
14. 先确认代码已 `push`、Pages 已开启、分支和目录正确，再等 1～2 分钟刷新。

---

## 11. 下次开始前检查

- [ ] 打开 VS Code 的 `atlas` 文件夹
- [ ] 按 `` Ctrl+` `` 打开终端
- [ ] `git status` 显示 `working tree clean`
- [ ] 看今天的任务
- [ ] 知道今天结束要 commit 什么

---

## 12. 下一阶段

下一步是 **CSS**：

- 创建 `styles.css`
- 用 `<link rel="stylesheet" href="styles.css">` 引入
- 盒模型、CSS 变量、排版
- Flexbox 导航和卡片
- 响应式 375px

CSS 之后才是 JavaScript、React、Go 和 MySQL。不急着跳。
