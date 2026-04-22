# 渲染原理 Labs（最小实验）

对应文档：

1. `lab01-pipeline-transform-vs-left.html` -> 渲染流水线与动画属性差异
2. `lab02-cssom-cascade-specificity.html` -> CSSOM/层叠/优先级
3. `lab03-layout-containing-block-sticky.html` -> 包含块与 sticky 行为
4. `lab04-flex-grid-comparison.html` -> Flex 与 Grid 方案对照
5. `lab05-reflow-repaint-zindex.html` -> 重排重绘与层叠上下文

使用方式：

- 直接用浏览器打开每个 html 文件
- 开 DevTools（Performance / Elements / Computed）观察差异

---

## 每个 Lab 的观察 Checklist

## Lab01：`transform` vs `left`

文件：`lab01-pipeline-transform-vs-left.html`

- [ ] 打开 Performance，先录制 `left` 动画一次
- [ ] 再录制 `transform` 动画一次
- [ ] 对比两段记录里 Layout/Paint/Composite 的占比
- [ ] 结论：为什么动画通常推荐 `transform`

## Lab02：CSSOM / 层叠 / 优先级

文件：`lab02-cssom-cascade-specificity.html`

- [ ] 在 Elements 面板选中 `#target`，查看 `color` 最终来源
- [ ] 观察哪些规则被划线覆盖
- [ ] 点击按钮切换 `highlight`，看命中规则变化
- [ ] 结论：优先级和书写顺序谁在起作用

## Lab03：包含块 + sticky

文件：`lab03-layout-containing-block-sticky.html`

- [ ] 下滑页面，观察 sticky 的触发时机
- [ ] 检查角标是否稳定贴在卡片右上角
- [ ] 尝试去掉父元素 `position: relative` 看角标是否跑偏
- [ ] 结论：absolute 参照系为什么重要

## Lab04：Flex vs Grid 对照

文件：`lab04-flex-grid-comparison.html`

- [ ] 缩放窗口，看两种方案在不同宽度下的表现
- [ ] 对比代码可读性：哪种更接近你的布局意图
- [ ] 记录“同一需求下两种方案的差异”
- [ ] 结论：这类场景你更该选 Flex 还是 Grid

## Lab05：重排重绘 + z-index

文件：`lab05-reflow-repaint-zindex.html`

- [ ] 录制点击“改 width”，观察是否触发布局计算
- [ ] 录制点击“改 color”，观察是否主要是重绘
- [ ] 观察 `transform` 元素与 `z-index` 的堆叠关系
- [ ] 结论：重排和重绘的成本差异 + z-index 排错思路

---

## 建议记录模板（每个 Lab 一段）

```md
## LabX 观察记录

### 我看到了什么
- 

### 我的结论
- 

### 我还不确定的问题
- 
```
