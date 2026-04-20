---
name: day-scaffold
description: Scaffold daily frontend learning folders and starter files. Use when the user says dayN (for example day4) or asks to initialize a new learning day directory with index.html and knowledge.md.
---

# Day Scaffold

## Purpose

Create a new day folder for frontend learning and initialize:

- `index.html`
- `knowledge.md`

Default folder naming:

- `week1-dayN-<topic>`
- Example: `day4` -> `week1-day4-position`

If topic is unknown, use:

- `week1-dayN`

## Trigger Phrases

Use this skill when the user says:

- `day4`
- `创建 day5`
- `初始化 day6`
- `帮我建 day7 目录`

## Inputs

- Required: day number (`day4`, `day5`, ...)
- Optional: topic slug (`position`, `responsive`, `js-dom`)

## Workflow

1. Parse day number from user input.
2. Infer topic from user message if available.
3. Build target directory name:
   - if topic exists: `week1-dayN-<topic>`
   - else: `week1-dayN`
4. Create files with starter content.
5. Report created paths and next steps.

## Starter Templates

### `index.html`

Use this template (replace `DAY_LABEL` with `DayN`):

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>DAY_LABEL 练习</title>
    <style>
      * { box-sizing: border-box; }
      body {
        margin: 0;
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
        line-height: 1.5;
        color: #1f2937;
        background: #f5f7fb;
      }
      main {
        max-width: 960px;
        margin: 0 auto;
        padding: 24px 16px;
      }
      .card {
        background: #fff;
        border: 1px solid #e5e7eb;
        border-radius: 10px;
        padding: 16px;
      }
    </style>
  </head>
  <body>
    <main>
      <section class="card">
        <h1>DAY_LABEL 练习页面</h1>
        <p>在这里开始你的练习。</p>
      </section>
    </main>
  </body>
</html>
```

### `knowledge.md`

Use this template (replace `DAY_LABEL` with `DayN`):

```md
# DAY_LABEL 学习笔记

## 今日目标
- 

## 核心知识点
- 

## 实战任务
- 

## 遇到的问题
- 

## 解决方案
- 

## 今日总结
- 
```

## Execution Notes

- Prefer creating files directly via editor tools.
- Keep content concise and editable.
- Use ASCII by default.

## Output Format

After scaffolding, report:

- created directory path
- created files
- optional next step suggestion (for example: "要不要我顺手生成 DayN 的任务清单？")
