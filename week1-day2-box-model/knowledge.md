# Day2 学习文档：盒模型与基础排版

## 1. 今天要掌握什么

Day2 的核心不是“把页面做漂亮”，而是建立稳定的布局认知：

- 理解 CSS 盒模型：`content`、`padding`、`border`、`margin`
- 理解 `box-sizing: border-box` 为什么是现代项目默认配置
- 能把页面内容组织成可维护的卡片布局
- 用 CSS 间距替代结构性标签（比如 `<br>`）
- 完成基础表单排版，并避免移动端溢出

---

## 2. 盒模型（Box Model）快速理解

每个 HTML 元素都可以看成一个盒子，从里到外是：

1. `content`：内容区（文字、图片）
2. `padding`：内边距（内容和边框之间的空间）
3. `border`：边框
4. `margin`：外边距（与其他元素的距离）

一个记忆口诀：

- `padding` 是“盒子里面的留白”
- `margin` 是“盒子外面的距离”

---

## 3. `box-sizing` 必须掌握

## 默认行为（`content-box`）

浏览器默认是 `content-box`。如果你设置：

- `width: 300px`
- `padding: 20px`
- `border: 2px solid`

实际渲染宽度会大于 300px，因为 `padding` 和 `border` 会额外叠加。

## 推荐行为（`border-box`）

使用 `border-box` 后，`width` 就是“最终可见宽度”，`padding` 和 `border` 会被包含进去。

推荐全局写法：

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```
让页面中所有元素（包括伪元素 ::before 和 ::after）都使用 border-box 盒模型。伪元素暂时用不到，先不深究。
这条规则能显著减少布局错位和移动端横向滚动问题。


## 注意事项

这段代码要放在样式表最前面，避免被后续规则覆盖（除非有更高优先级）。

有些第三方组件可能依赖于 content-box，但绝大多数现代组件库（如 Ant Design、Element Plus）内部会自己重置，或者它们的设计就兼容 border-box。

如果你需要某些元素恢复 content-box（比如第三方组件内部），可以单独给该元素设置 box-sizing: content-box。

---

## 4. Day2 任务背后的知识点

## 4.1 全局排版

目标是让页面“可读”：

- `font-family`：保证字体一致
- `line-height`：提高阅读舒适度
- `max-width + margin: 0 auto + padding`：控制阅读宽度并居中

示例思路：

```css
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
  line-height: 1.6;
  color: #1f2937;
  background: #f5f7fb;
}

.page {
  max-width: 900px;
  margin: 0 auto;
  padding: 24px;
}
```

## 4.2 section 卡片化

目标是让内容有层次：

- 用 `padding` 做内部留白
- 用 `border` 或 `box-shadow` 做分层
- 用 `border-radius` 提升观感一致性

示例：

```css
section {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 20px;
}

section + section {
  margin-top: 16px;
}
```

## 4.3 间距管理方式

你在 Day1 中用了 `<br>` 做视觉间距。Day2 要改成 CSS 控制：

- 不用 `<br>` 调布局
- 使用 `margin` 或容器 `gap` 管理间距

示例：

```css
#intro img {
  display: block;
  width: 120px;
  height: 120px;
  border-radius: 50%;
  margin-bottom: 12px;
}
```

## 4.4 表单排版基础

目标是“对齐整齐、输入舒适”：

- 每个字段用统一结构（如 `.field`）
- `label` 和输入框上下布局更稳定
- 输入框和文本域设置 `width: 100%`，配合 `border-box` 防溢出

示例：

```css
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
```

---

## 5. Day2 常见坑（重点）

1. 给元素 `width: 100%`，又加大 `padding`，导致小屏横向滚动  
   - 解决：全局 `border-box`

2. 用 `<br>` 或大量空行调间距  
   - 解决：统一用 `margin/padding/gap`

3. 每个 section 写一套不同样式  
   - 解决：抽公共规则，保证视觉一致

4. 表单 `label` 没和 `for/id` 关联  
   - 解决：可访问性基础必须保留

5. 只看“视觉差不多”，不看 DevTools 盒模型  
   - 解决：至少检查一次 computed 盒模型

---

## 6. Day2 自测清单（提交前）

- 已设置全局 `box-sizing: border-box`
- `section` 使用统一卡片规则（边框/阴影、圆角、内边距）
- 去掉了结构性 `<br>` 间距写法
- 表单字段有统一间距，`textarea` 有最小高度
- 手机宽度下无横向滚动条
- 你能解释：`padding`、`border`、`margin` 分别在解决什么问题

---

## 7. 今天的学习产出模板（可直接复制到 README）

```md
## Day2 学习总结

### 我做了什么
- 完成全局排版与页面容器
- 为 section 增加统一卡片样式
- 将 `<br>` 间距替换为 CSS margin
- 优化表单字段布局和输入体验

### 我学会了什么
- 盒模型四层结构：content/padding/border/margin
- 为什么项目里推荐全局 border-box
- 如何避免移动端横向溢出

### 我遇到的问题
- （填写你今天遇到的真实问题）

### 我如何解决
- （填写解决过程）

### 明天要做什么
- 进入 Day3：Flex 布局实战（导航 + 三列卡片）
```

---

## 8. 明日衔接（Day3 预告）

Day3 会重点进入 Flex。你今天的卡片、间距、表单基础打好后，明天只需要关注“主轴/交叉轴”和“容器-子项关系”，学习效率会高很多。
