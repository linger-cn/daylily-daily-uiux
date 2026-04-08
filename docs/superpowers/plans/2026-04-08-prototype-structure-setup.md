# 原型目录结构初始化执行计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 创建 `prototypes/` 根目录，并根据“资产自治型”方案初始化一个示例项目结构。

**Architecture:** 采用方案 A（资产自治型），每个项目拥有独立的 `styles/` 和 `assets/` 文件夹。

**Tech Stack:** HTML, CSS (Vanilla), Tailwind CSS (via CDN)

---

### Task 1: 创建原型根目录及示例项目结构

**Files:**
- Create: `prototypes/`
- Create: `prototypes/example-project/styles/`
- Create: `prototypes/example-project/assets/`

- [ ] **Step 1: 创建目录结构**

运行: `mkdir -p prototypes/example-project/styles prototypes/example-project/assets`

- [ ] **Step 2: 验证目录创建**

运行: `ls -R prototypes`
预期: 看到 `example-project` 及其子目录 `styles` 和 `assets`。

- [ ] **Step 3: 提交空目录结构**

由于 git 不跟踪空目录，我们可以创建一个 `.gitkeep` 文件或直接在下一步创建文件。这里先跳过提交，在 Task 2 中创建文件后一起提交。

---

### Task 2: 初始化示例项目样式与页面

**Files:**
- Create: `prototypes/example-project/styles/main.css`
- Create: `prototypes/example-project/index.html`

- [ ] **Step 1: 创建示例样式文件**

内容:
```css
/* prototypes/example-project/styles/main.css */
:root {
  --project-primary: #4f46e5;
}

.project-card {
  border: 2px solid var(--project-primary);
  padding: 1rem;
  border-radius: 0.5rem;
}
```

- [ ] **Step 2: 创建项目入口页面**

内容:
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example Project - 原型展示</title>
    <link rel="stylesheet" href="./styles/main.css">
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 p-8">
    <div class="max-w-2xl mx-auto">
        <header class="mb-8">
            <h1 class="text-3xl font-bold text-gray-900">Example Project 原型入口</h1>
            <p class="text-gray-600 mt-2">这是采用“资产自治型”方案创建的示例项目。</p>
        </header>

        <section class="project-card bg-white shadow-sm">
            <h2 class="text-xl font-semibold mb-4">页面列表</h2>
            <ul class="space-y-2">
                <li>
                    <a href="#" class="text-indigo-600 hover:underline">示例页面 1 (待创建)</a>
                </li>
            </ul>
        </section>

        <footer class="mt-12 text-sm text-gray-500">
            <a href="../../index.html" class="hover:text-gray-700">← 返回主设计系统</a>
        </footer>
    </div>
</body>
</html>
```

- [ ] **Step 3: 验证文件引用**

手动或使用工具确认 `index.html` 能正确加载 `./styles/main.css`。

- [ ] **Step 4: 提交变更**

运行: `git add prototypes/ && git commit -m "feat: initialize prototypes directory with example-project"`

---

### Task 3: 验证全局样式引用（可选验证）

**Files:**
- Modify: `prototypes/example-project/index.html`

- [ ] **Step 1: 添加全局样式引用测试**

在 `index.html` 的 `<head>` 中添加对根目录 `themes/default.css` 的引用（注释掉或共存），验证路径正确性。

```html
<!-- 引用全局 Design System 样式 -->
<link rel="stylesheet" href="../../themes/default.css">
```

- [ ] **Step 2: 验证路径**

确保路径 `../../themes/default.css` 指向正确的全局样式文件。

- [ ] **Step 3: 恢复并提交**

确认无误后，保留或移除测试引用并提交。
