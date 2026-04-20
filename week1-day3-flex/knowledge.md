# Day3 学习文档：Flex 布局实战

## 1. 今天要掌握什么

Day3 的核心是：**让盒子按规则“自动排队”**。  
你已经有 Day2 的盒模型基础，今天重点是用 Flex 解决“横向/纵向对齐、换行、响应式切换”。

- 理解 Flex 的两层角色：容器（container）与子项（item）
- 理解主轴与交叉轴
- 掌握 6 个高频属性：`display`、`flex-direction`、`justify-content`、`align-items`、`gap`、`flex-wrap`
- 能完成 3 个常见场景：导航栏、卡片流、响应式 footer

---

## 2. Flex 一句话定义

Flex 是一维布局系统，擅长处理一行或一列中的对齐和分配空间问题。

- 一维 = 主要解决“一个方向”的排布
- Grid 更适合二维布局（行 + 列同时控制）

---

## 2.1 Flex 布局的演进过程（大白话版）

可以把前端布局理解成“人类在跟网页排版打仗”的历史：

1. 早期主要靠普通文档流 + `float`（浮动）硬排版  
   - 问题：本来是为“图文环绕”设计的，却被拿来做整站布局，清除浮动很痛苦。

2. 后来有人大量使用 `inline-block`、`position` 来凑布局  
   - 问题：对齐麻烦、间距容易出 bug、响应式适配成本高。

3. 再后来出现 Flex，专门解决“一行/一列的对齐和分配”  
   - 优点：对齐简单、写法直观、响应式友好。

4. 现在的主流做法  
   - 一维排布（导航、卡片流、按钮组）优先用 Flex  
   - 二维网格（仪表盘、复杂后台）优先用 Grid  
   - 两者配合，而不是二选一。

一句话总结：  
**Flex 不是“更高级的写法”，而是“专门为布局而生的工具”，所以比过去那些绕路方案省心很多。**

---

## 3. 先记住这两个概念

## 3.1 容器和子项

- 给父元素写 `display: flex;`，它就变成 Flex 容器
- 容器的**直接子元素**自动变成 Flex 子项

大白话理解：

- 容器 = “队长”  
- 子项 = “队员”  
- 队长负责下命令（横着站？竖着站？间隔多大？），队员按命令排队。

代码举例（和你现在页面一致）：

```html
<header>
  <h1>Thomas的个人简介</h1>
  <nav>...</nav>
</header>
```

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

解释：

- `header` 是容器（队长）
- `h1` 和 `nav` 是子项（队员）
- `justify-content: space-between` 相当于“一个站左边，一个站右边”
- `align-items: center` 相当于“都站一条水平线上，别高低不齐”

## 3.2 主轴和交叉轴

- 默认 `flex-direction: row`：主轴是水平，交叉轴是垂直
- `flex-direction: column`：主轴变垂直，交叉轴变水平

记忆法：
- `justify-content` 管主轴
- `align-items` 管交叉轴

大白话例子：

- `row` 时，你在管“左右排队”，所以 `justify-content` 像在管“左右站位”
- `column` 时，你在管“上下排队”，所以 `justify-content` 变成管“上下站位”

再举一个你页面里的例子（项目卡片）：

```css
#projects ul {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
```

解释：

- `#projects ul` 是容器（队长）
- 每个 `li` 是子项（队员）
- 空间够就一排多站几个，不够就自动换到下一排（`wrap`）

---

## 4. Day3 的 6 个核心属性

## 4.1 `display: flex`

把普通流布局切换为 Flex 布局的入口。

```css
.box {
  display: flex;
}
```

## 4.2 `flex-direction`

控制子项主排列方向。

```css
.row { flex-direction: row; }      /* 默认 */
.col { flex-direction: column; }   /* 垂直 */
```

## 4.3 `justify-content`

主轴对齐方式。

```css
justify-content: flex-start;
justify-content: center;
justify-content: space-between;
```

## 4.4 `align-items`

交叉轴对齐方式。

```css
align-items: stretch;   /* 默认 */
align-items: center;
align-items: flex-start;
```

## 4.5 `gap`

Flex 子项之间的统一间距。  
优先用 `gap`，比给每项加 `margin-right` 更干净。

## 4.6 `flex-wrap`

是否允许换行。

```css
flex-wrap: nowrap; /* 默认，不换行 */
flex-wrap: wrap;   /* 空间不足自动换行 */
```

---

## 4.7 选择器补充：子代选择器与后代选择器

这两个选择器在布局实战中非常常用，尤其是你现在这种结构化页面。

### 子代选择器（`>`）

写法：

```css
A > B
```

含义：只匹配 **A 的直接子元素 B**（中间不能隔层级）。

示例（来自你页面）：

```css
footer > div {
  flex: 1 1 320px;
}
```

解释：只会选中 `footer` 的第一层 `div`，不会影响更深层的 `div`。

### 后代选择器（空格）

写法：

```css
A B
```

含义：匹配 **A 内任意层级** 的 B（可以隔多层）。

示例（来自你页面）：

```css
#projects li {
  flex: 1 1 220px;
}
```

解释：会选中 `#projects` 区域里所有层级中的 `li`。

### 什么时候用哪个？

- 需要精确控制“当前层级”时，用 `>`（子代）
- 需要统一控制“整个区域某类元素”时，用空格（后代）

常见坑：

1. 后代选择器范围太大，误伤不该改的元素  
2. 子代选择器层级不匹配，导致“写了但不生效”

---

## 5. 你当前页面里的 Flex 映射（对应 index.html）

## 5.1 Header 左右布局

你已在 `header` 使用：

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

作用：
- 标题和导航分居两侧
- 不同高度元素也能垂直对齐

## 5.2 导航链接横向排列

```css
nav {
  display: flex;
  gap: 12px;
}
```

作用：
- 链接自然横排
- 间距统一、可维护

## 5.3 项目区卡片流（重点）

```css
#projects ul {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

#projects li {
  flex: 1 1 220px;
}
```

作用：
- 宽屏并排，小屏自动换行
- `220px` 是卡片“理想基础宽度”

## 5.4 Footer 响应式切换

```css
footer {
  display: flex;
  gap: 20px;
}

@media (max-width: 640px) {
  footer {
    flex-direction: column;
  }
}
```

作用：
- 桌面端两栏并排
- 手机端自动堆叠成一列

---

## 6. `flex: 1 1 220px` 怎么读（必须懂）

`flex` 是 `flex-grow flex-shrink flex-basis` 的简写：

- `1`（grow）：有剩余空间时可以放大
- `1`（shrink）：空间不足时可以缩小
- `220px`（basis）：初始参考宽度

直觉理解：  
“我希望每张卡片先按 220px 排，但空间允许就伸展，不够就收缩并换行。”

---

## 7. Day3 常见坑（重点）

1. `justify-content` 和 `align-items` 用反了  
   - 先确认主轴方向，再决定谁管谁

2. 忘了 `flex-wrap: wrap`，导致小屏挤爆  
   - 卡片流几乎都要加 `wrap`

3. 仍用 `margin-right` 控导航间距  
   - 用 `gap` 更统一，维护成本更低

4. 给子项写了 `flex`，但父元素没 `display:flex`  
   - 子项的 Flex 属性会失效

5. 只在桌面看效果，不测移动端  
   - 至少检查 375px / 768px / 1024px 三档

---

## 8. Day3 提交前自测清单

- `header`：左右布局成立（标题左，导航右）
- `nav`：横向 + `gap` 间距正确
- `projects`：卡片可换行，无挤压溢出
- `footer`：桌面端并排、移动端堆叠
- 全局仍保留 `box-sizing: border-box`
- 手机宽度无横向滚动条

---

## 9. 今天的学习产出模板（可复制到 README）

```md
## Day3 学习总结（Flex）

### 我做了什么
- 完成 header 的 Flex 左右布局
- 完成项目卡片流（支持自动换行）
- 完成 footer 的响应式切换（桌面两栏、移动端一栏）

### 我学会了什么
- 主轴/交叉轴的区别
- `justify-content` 与 `align-items` 的使用边界
- `flex: 1 1 220px` 的实际意义

### 我遇到的问题
- （填写今天遇到的问题）

### 我如何解决
- （填写解决过程）

### 明天要做什么
- Day4：定位与常见页面交互（固定头部、悬浮按钮、回到顶部）
```

---

## 10. 明日衔接（Day4 预告）

Day4 建议学习定位（`relative/absolute/fixed/sticky`）并配合 Day3 的 Flex 页面做两个实战：

- 固定顶部导航（`sticky`）
- 右下角悬浮“回到顶部”按钮（`fixed`）

这样你会把“排布能力（Flex）+ 定位能力（Position）”连接起来，页面开发会顺很多。

---

## 附录：完整 `index.html` 代码

```html
<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>个人简介</title>
        <style>
            *, *::before, *::after {
                box-sizing: border-box;
            }

            body {
                background-color: #f5f7fb;
                margin: 0;

                /* 全局字体 */
                font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
                /* 行高 （无单位数字，比如1.5），表示当前字体大小的1.5倍，这样当子元素字体大小不同时，行高会自动按比例缩放。 */
                line-height: 1.5;
                color: #1f2937;
            }

            header,
            main,
            footer {
                max-width: 1000px;
                margin: 0 auto;
                padding: 0 16px;
            }

            header {
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding-top: 20px;
                padding-bottom: 12px;
            }

            section {
                background: #fff;
                border: 1px solid #e5e7eb;
                border-radius: 10px;
                padding: 20px;
            }
            /* 每个 section 下方留出 2rem 间距(2个rem，表示当前字体大小的2倍  */
            /* section {
                margin-bottom: 2rem;
            }
            */

            /* 相邻兄弟选择器：选择紧挨着的下一个兄弟元素
            含义：紧接在另一个 section 后面的 section，在其上方添加间距。
            优点：不会给第一个 section 添加上边距，也不会给最后一个添加下边距，且间距不会叠加（因为只设置了上边距）。
             */
            /* section + section {
                margin-top: 2rem;
            } */

            /* 如果所有 section 都放在同一个容器内（例如 <main>），可以： */
            main {
                display: flex;
                flex-direction: column;
                gap: 2rem;
                margin-top: 16px;
                margin-bottom: 24px;
            }

            nav {
                display: flex;
                gap: 12px;
            }

            nav a {
                color: #1d4ed8;
                text-decoration: none;
                padding: 6px 10px;
                border-radius: 8px;
            }

            nav a:hover {
                background: #dbeafe;
            }

            #intro img {
                display: block;
                width: 120px;
                height: 120px;
                border-radius: 50%;
                margin-bottom: 12px;
            }

            #projects ul {
                list-style: none;
                padding: 0;
                margin: 12px 0 0;
                display: flex;
                flex-wrap: wrap;
                gap: 12px;
            }

            #projects li {
                flex: 1 1 220px;
                border: 1px solid #e2e8f0;
                background: #f8fafc;
                border-radius: 8px;
                padding: 12px;
            }

            .field {
                display: flex;
                flex-direction: column;
                gap: 6px;
                margin-bottom: 12px;
            }

            input,
            textarea {
                width: 100%;
                padding: 10px 12px;
                border: 1px solid #cbd5e1;
                border-radius: 8px;
            }

            textarea {
                min-height: 120px;
                resize: vertical;
            }

            button {
                background: #2563eb;
                color: #fff;
                border: 1px solid #1d4ed8;
                border-radius: 8px;
                padding: 10px 16px;
                cursor: pointer;
            }

            button:hover {
                background: #1d4ed8;
            }

            footer {
                display: flex;
                justify-content: space-between;
                align-items: flex-start;
                gap: 20px;
                background: #fff;
                border: 1px solid #e5e7eb;
                border-radius: 10px;
                padding-top: 20px;
                padding-bottom: 20px;
                margin-bottom: 24px;
            }

            footer > div {
                flex: 1 1 320px;
            }

            footer p {
                margin: 0;
            }

            footer > p {
                color: #64748b;
                font-size: 14px;
                margin-top: 8px;
            }

            @media (max-width: 640px) {
                header {
                    flex-direction: column;
                    align-items: flex-start;
                    gap: 10px;
                }

                nav {
                    flex-wrap: wrap;
                }

                footer {
                    flex-direction: column;
                }
            }
        </style>
    </head>
    <body>
        <header>
            <h1>Thomas的个人简介</h1>
            <nav>
                <a href="#intro">关于我</a>
                <a href="#skills">技能列表</a>
                <a href="#projects">项目</a>
            </nav>
        </header>
        <main>
            <section id="intro">
                <h2>自我介绍</h2>
                <img src="./images/avatar.png" alt="thomas">
                <p>我是一个热爱编程的年轻人，喜欢探索新技术，喜欢挑战自己，喜欢分享知识。</p>
            </section>
            <section id="skills">
                <h2>技能列表</h2>
                <ul>
                    <li>HTML</li>
                    <li>CSS</li>
                    <li>JavaScript</li>
                    <li>VUE</li>
                    <li>Python</li>
                </ul>
            </section>
            <section id="projects">
                <h2>项目</h2>
                <ul>
                    <li>项目1</li>
                    <li>项目2</li>
                    <li>项目3</li>
                </ul>
            </section>
        </main>
        <footer>
            <div>
                <h3>联系方式</h3>
                <p><a href="mailto:630023774@qq.com">邮箱: 630023774@qq.com</a></p>
            </div>
            <div>
                <h3>给我留言</h3>
                <form action="#" method="post">
                    <div class="field">
                        <label for="name">姓名:</label>
                        <input type="text" id="name" name="name" placeholder="请输入您的姓名" required>
                    </div>
                    <div class="field">
                        <label for="email">邮箱:</label>
                        <input type="email" id="email" name="email" placeholder="请输入您的邮箱" required>
                    </div>
                    <div class="field">
                        <label for="message">留言:</label>
                        <textarea id="message" name="message" placeholder="请输入您的留言" required></textarea>
                    </div>
                    <button type="submit">提交</button>
                </form>
            </div>
            <p>版权所有 © 2026 个人简介</p>
        </footer>
    </body>

</html>
```
