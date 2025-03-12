---
title: Cursor + Qwen2.5-Coder 开发一个网页应用，So easy！附代码.md
author: 老章 mlpy
date: 2024-12-13 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

大家好，我是不懂前端的章北海

看到 `Qwen2.5-Coder` 非常强悍，就想测试一下，能否 0 基础开发一个网页应用。

我是 `Mac💻`用户，浏览器全屏模式下看时间需要鼠标上划唤出菜单栏，容易打断我的专注模式🧘。

所以就想开发一个网页，能在 `Tab` 标题中显示北京时间，另外，页面内部也想加一个番茄🍅时钟。

试了一下，果然很强，效果如下⬇️，完美满足我的需求，然后上线部署到 `vercel` 就行了：
![](https://r2blog.zhanglearning.com/2024/12/f1562196b2a58e1889241170c6183a8f.png)

上线后，开网页不影响我看时间！

![](https://r2blog.zhanglearning.com/2024/12/f7707e32b1d673eee9f1cc2f44b2877c.png)

## Cursor + Qwen2.5-Coder

本文我测试用到的是 `Qwen2.5-Coder-32B-Instruct`，它基于 `Qwen2.5` 开发的代码特定大语言模型。该模型通过 5.5 万亿 `tokens` 的训练，在代码生成、代码推理和代码修复方面都取得了显著提升。它是当前最先进的开源代码语言模型，编码能力可与 `GPT-4` 相媲美。

* 阿里云百炼： https://help.aliyun.com/zh/model-studio/developer-reference/what-is-qwen-llm 
* 魔搭社区 ModelScope 体验： https://www.modelscope.cn/studios/Qwen/Qwen2.5-Turbo-1M-Demo 
* Hugging Face 体验： https://huggingface.co/spaces/Qwen/Qwen2.5-Turbo-1M-Demo


阿里自己也有一个编程辅助工具叫**通义灵码**，在 `VSCode` 中安装插件即可，也很棒，下次再测试吧。

>[通义灵码](https://tongyi.aliyun.com/lingma/)，是基于通义大模型的智能编程辅助工具，提供行级/函数级实时续写、自然语言生成代码、单元测试生成、代码优化、注释生成、代码解释、研发智能问答、异常报错排查等能力，并针对阿里云的云服务使用场景调优，助力开发者高效、流畅地编码。

最近经常用 `Cursor`，所以就直接在 `Cursor` 中调用 `Qwen2.5-Coder-32B-Instruct` 来帮我开发这个网页应用。

![](https://r2blog.zhanglearning.com/2024/12/73fca1426e27b081ca87d3053c029470.png)

## “开发”过程

整个过程，代码全部由`Qwen2.5-Coder`生成！

prompt 如下：你是前端开发工程师，我想实现一个网页应用，tab 页可以显示具体的时间，页面正文部分显示具体的北京时间、年月日，还可以设定番茄时钟。

它给我了三段代码

### 1. HTML
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>番茄时钟</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="tabs">
        <button class="tab-button" onclick="showTab('time')">时间</button>
        <button class="tab-button" onclick="showTab('pomodoro')">番茄时钟</button>
    </div>
    <div id="time" class="tab-content">
        <h1 id="current-time"></h1>
        <h2 id="current-date"></h2>
    </div>
    <div id="pomodoro" class="tab-content" style="display:none;">
        <h1>番茄时钟</h1>
        <div id="pomodoro-timer">25:00</div>
        <button id="start-pomodoro">开始</button>
        <button id="stop-pomodoro">停止</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

### 2. CSS 样式
```css
/* styles.css */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
}

#tabs {
    margin-top: 20px;
}

.tab-button {
    padding: 10px 20px;
    margin: 0 5px;
    cursor: pointer;
}

.tab-content {
    margin-top: 20px;
    display: none;
}

.tab-content.active {
    display: block;
}
```

### 3. JavaScript 逻辑

```javascript
// script.js 处理时间显示和番茄时钟的功能

// 显示当前时间
function updateTime() {
    const now = new Date();
    const timeString = now.toLocaleTimeString('zh-CN', { hour12: false });
    const dateString = now.toLocaleDateString('zh-CN', { year: 'numeric', month: 'long', day: 'numeric' });
    document.getElementById('current-time').textContent = timeString;
    document.getElementById('current-date').textContent = dateString;
}

// 切换标签页
function showTab(tabName) {
    const tabs = document.getElementsByClassName('tab-content');
    for (let i = 0; i < tabs.length; i++) {
        tabs[i].style.display = 'none';
    }
    document.getElementById(tabName).style.display = 'block';
}

// 番茄时钟逻辑
let pomodoroInterval;
let pomodoroTime = 25 * 60; // 25分钟

function startPomodoro() {
    pomodoroInterval = setInterval(() => {
        pomodoroTime--;
        updatePomodoroTimer();
        if (pomodoroTime <= 0) {
            clearInterval(pomodoroInterval);
            alert('番茄时钟结束！');
        }
    }, 1000);
}

function stopPomodoro() {
    clearInterval(pomodoroInterval);
}

function updatePomodoroTimer() {
    const minutes = Math.floor(pomodoroTime / 60);
    const seconds = pomodoroTime % 60;
    document.getElementById('pomodoro-timer').textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
}

// 初始化
setInterval(updateTime, 1000);
updateTime();
document.getElementById('start-pomodoro').addEventListener('click', startPomodoro);
document.getElementById('stop-pomodoro').addEventListener('click', stopPomodoro);
```

如果连这些脚本干什么的都不知道，也可以问`Qwen2.5-Coder`

1. **HTML**: 创建了两个标签页，一个用于显示当前时间和日期，另一个用于番茄时钟。
2. **CSS**: 添加了一些基本样式，使页面看起来更整洁。
3. **JavaScript**: 实现了时间的实时更新、标签页的切换以及番茄时钟的计时功能。

## 调整、美化


预览一下，效果不太理想，可以根据第一版情况让`Qwen2.5-Coder`继续修改

prompt 如下：有两个需要调整的点：1、Tab 的 title 显示应该是北京时间，十分秒，动态。2、页面内时间和番茄时钟同时显示，不需要点击。另外，主题不够美观，请使用最先进、最美观的形式展现。

然后`Qwen2.5-Coder`给出了调整后的代码

首先是主 HTML 文件：

```html:index.html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="page-title">北京时间</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <div class="card time-display">
            <div class="time-wrapper">
                <h1 class="current-time" id="current-time"></h1>
                <p class="current-date" id="current-date"></p>
            </div>
        </div>
        
        <div class="card pomodoro-container">
            <h2>番茄时钟</h2>
            <div class="timer-display" id="pomodoro-timer">25:00</div>
            <div class="button-group">
                <button id="start-pomodoro">开始</button>
                <button id="pause-pomodoro">暂停</button>
                <button id="reset-pomodoro" class="reset-btn">重置</button>
            </div>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

CSS 文件：

```css:styles.css
:root {
    --primary-color: #2196f3;
    --background-color: #f5f5f5;
    --card-background: #ffffff;
    --text-color: #333333;
}

body {
    font-family: 'Roboto', sans-serif;
    margin: 0;
    padding: 20px;
    background-color: var(--background-color);
    color: var(--text-color);
    min-height: 100vh;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    padding: 20px;
}

.card {
    background: var(--card-background);
    border-radius: 15px;
    padding: 25px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 300px;
}

.card:hover {
    transform: translateY(-5px);
}

.time-display {
    text-align: center;
}

.time-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.current-time {
    font-size: 3.5rem;
    font-weight: 300;
    margin: 0;
    color: var(--primary-color);
}

.current-date {
    font-size: 1.5rem;
    color: #666;
    margin: 10px 0;
}

.pomodoro-container {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.timer-display {
    font-size: 4rem;
    font-weight: 300;
    margin: 20px 0;
    color: var(--primary-color);
}

.button-group {
    display: flex;
    gap: 10px;
    justify-content: center;
}

button {
    padding: 12px 24px;
    border: none;
    border-radius: 25px;
    background-color: var(--primary-color);
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s ease;
}

button:hover {
    background-color: #1976d2;
    transform: scale(1.05);
}

button:active {
    transform: scale(0.95);
}

.reset-btn {
    background-color: #ff5722;
}

.reset-btn:hover {
    background-color: #f4511e;
}
```

JavaScript 文件：

```javascript:script.js
// 更新标题和时间显示
function updateTime() {
    const now = new Date();
    const timeString = now.toLocaleTimeString('zh-CN', { hour12: false });
    const dateString = now.toLocaleDateString('zh-CN', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        weekday: 'long'
    });
    
    // 更新页面标题
    document.title = `北京时间 ${timeString}`;
    
    // 更新页面显示
    document.getElementById('current-time').textContent = timeString;
    document.getElementById('current-date').textContent = dateString;
}

// 番茄时钟相关变量
let pomodoroTime = 25 * 60;
let pomodoroInterval;
let isRunning = false;

// 番茄时钟功能
function updatePomodoroTimer() {
    const minutes = Math.floor(pomodoroTime / 60);
    const seconds = pomodoroTime % 60;
    document.getElementById('pomodoro-timer').textContent = 
        `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
}

function startPomodoro() {
    if (!isRunning) {
        isRunning = true;
        pomodoroInterval = setInterval(() => {
            if (pomodoroTime > 0) {
                pomodoroTime--;
                updatePomodoroTimer();
            } else {
                clearInterval(pomodoroInterval);
                isRunning = false;
                alert('番茄时钟完成！');
            }
        }, 1000);
    }
}

function pausePomodoro() {
    clearInterval(pomodoroInterval);
    isRunning = false;
}

function resetPomodoro() {
    clearInterval(pomodoroInterval);
    isRunning = false;
    pomodoroTime = 25 * 60;
    updatePomodoroTimer();
}

// 事件监听
document.getElementById('start-pomodoro').addEventListener('click', startPomodoro);
document.getElementById('pause-pomodoro').addEventListener('click', pausePomodoro);
document.getElementById('reset-pomodoro').addEventListener('click', resetPomodoro);

// 初始化
setInterval(updateTime, 1000);
updateTime();
updatePomodoroTimer();
```


这个更新后的版本有以下改进：

1. **标题动态更新**：浏览器标签页会实时显示北京时间
2. **现代化设计**：
   - 使用卡片式布局
   - 添加优雅的阴影效果
   - 使用现代化的颜色方案
   - 添加平滑的动画效果
3. **响应式布局**：
   - 使用 CSS Grid 实现自适应布局
   - 在不同屏幕尺寸下都能很好地展示
4. **功能完善**：
   - 时间和番茄时钟同时显示
   - 番茄时钟增加了暂停和重置功能
   - 显示完整的日期信息，包括星期
5. **交互优化**：
   - 按钮添加悬停效果
   - 卡片添加轻微的悬停动画
   - 更清晰的视觉层次

## 部署上线

![](https://r2blog.zhanglearning.com/2024/12/819cc2d664d8a0bf191193852feafefc.png)

`Qwen2.5-Coder`回复如下

当然可以！将你的项目部署到 Vercel 并使用 Cloudflare 作为域名提供商，可以按照以下步骤进行操作。

### 1. 准备项目文件
确保你的项目文件结构如下：
```
my-tomato-clock/
├── index.html
├── styles.css
└── script.js
```

### 2. 创建 Vercel 账户并安装 Vercel CLI
如果你还没有 Vercel 账户，先注册一个：[Vercel 注册页面](https://vercel.com/signup)

安装 Vercel CLI：
```bash
npm install -g vercel
```

### 3. 部署项目到 Vercel
1. 打开终端并导航到你的项目目录：
    ```bash
    cd path/to/my-tomato-clock
    ```

2. 使用 Vercel CLI 部署项目：
    ```bash
    vercel
    ```

3. 按照提示操作：
    - 选择项目目录（默认即可）
    - 输入项目名称（可选）
    - 选择框架（选择 `Other`）
    - 选择是否公开项目（可选）
    - 选择是否自动部署（可选）

4. 部署完成后，Vercel 会提供一个临时的 URL，例如 `https://my-tomato-clock.vercel.app`。

### 4. 配置 Cloudflare
1. 登录到你的 Cloudflare 账户：[Cloudflare 登录页面](https://dash.cloudflare.com/login)

2. 添加域名：
    - 点击 `Add Site` 按钮。
    - 输入你的域名，然后点击 `Add Site`。

3. 获取 Cloudflare 的 DNS 记录：
    - 在 Cloudflare 仪表盘中，进入你的域名页面。
    - 点击 `DNS` 标签。
    - 记录 Cloudflare 提供的两个 DNS 服务器地址（例如 `ns1.cloudflare.com` 和 `ns2.cloudflare.com`）。

4. 更新域名注册商的 DNS 设置：
    - 登录到你的域名注册商账户。
    - 找到 DNS 设置或名称服务器设置。
    - 将域名的名称服务器更改为 Cloudflare 提供的两个地址。
    - 保存更改。

5. 等待 DNS 更改生效（通常需要几分钟到几小时）。

### 5. 在 Cloudflare 中配置 Vercel 的域名
1. 在 Cloudflare 仪表盘中，进入你的域名页面。
2. 点击 `Pages` 标签。
3. 点击 `Create a project` 按钮。
4. 选择 `Custom domain`。
5. 输入你的域名（例如 `mytomatoclock.com`）。
6. 点击 `Next`。
7. 选择 `Custom build`。
8. 输入 Vercel 提供的 URL（例如 `https://my-tomato-clock.vercel.app`）。
9. 点击 `Next`。
10. 点击 `Deploy`。

### 6. 配置 SSL 证书
1. 在 Cloudflare 仪表盘中，进入你的域名页面。
2. 点击 `SSL/TLS` 标签。
3. 确保 SSL 模式设置为 `Flexible` 或 `Full`（推荐 `Full`）。
4. 点击 `Save`。

### 7. 验证部署
1. 等待 DNS 更改生效。
2. 打开你的域名（例如 `https://mytomatoclock.com`），确保一切正常。

### 8. 自动化部署（可选）
如果你希望每次代码更新后自动部署到 Vercel，可以配置 GitHub 集成：
1. 在 Vercel 仪表盘中，进入你的项目页面。
2. 点击 `Git Integration`。
3. 选择你的 GitHub 账户和仓库。
4. 按照提示完成集成。

这样，每次你推送代码到 GitHub，Vercel 会自动部署你的项目。

## 最终效果


手动调整了一两个细节，按照提示，上线后如下

![](https://r2blog.zhanglearning.com/2024/12/01ff925e0a3659c3ff0134d051c56ae5.png)

打开 N 多网页，也不会影响我愉快的看时间

![](https://r2blog.zhanglearning.com/2024/12/f7707e32b1d673eee9f1cc2f44b2877c.png)

使用 Qwen Coder，你可以显著降低开发成本，通过自动化代码生成快速搭建应用框架，将更多资源投入到核心功能开发。Qwen Coder 支持多种编程语言和框架，确保技术栈选择灵活。同时，它能根据具体需求生成定制化代码，轻松调整和优化，确保应用程序完全符合你的期望。