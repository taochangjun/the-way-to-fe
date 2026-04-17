Day2 任务清单（盒模型 + 基础排版，2小时）
目标：把你 Day1 的页面做成可读、有间距、有卡片感，并真正理解 content/padding/border/margin 与 box-sizing。

0）准备（5分钟）
在 index.html 里整理 <style>：把 Day1 里“只为测试滚动”的样式先删掉（例如 body { height: 200vh; }，除非你明确还要用它做练习）
建议顺手改：html lang="zh-CN"（内容中文时更规范）
1）全局排版（25分钟）
给 body 设置：背景色、文字颜色、基础字号
给页面内容加“容器宽度”：例如 main 外层包一层 div.page 或在 body 里用 max-width + margin: 0 auto + padding
验收：大屏不“铺满一整行难读”，小屏不贴边
2）盒模型必修（30分钟）
明确并实践：
padding：卡片内部留白
border：卡片边界
margin：卡片之间外部间距
加一行全局规则：*, *::before, *::after { box-sizing: border-box; }
验收：你能口头解释：为什么加了 border 后宽度会变化、以及 border-box 如何解决这个问题
3）把三个 section 做成“卡片”（25分钟）
每个 section：圆角、边框或阴影（二选一即可）、内边距
标题与内容间距合理（h2 与下面内容）
验收：三个区块视觉一致（同一套规则，不要各写各的）
4）替换 <br> 为 CSS 间距（15分钟）
去掉头像与段落之间的 <br>
用 img 的 display + margin 或给 p 加 margin-top（任选一种清晰方案）
验收：结构更干净，间距仍舒服
5）表单区域排版（20分钟）
footer 里两块内容（联系方式 / 留言）做成两列或上下堆叠都可，但要对齐整齐
表单项纵向间距统一（每个字段一组 div.field）
textarea：设置 min-height、width: 100%（在小屏更好用）
验收：表单不挤、不飘、对齐一致
6）自测清单（10分钟）
打开 DevTools，选中一个卡片，确认 computed 里盒模型是否符合预期
检查：小屏（手机宽度）是否没有横向溢出滚动条（常见是某元素 width: 100% 又叠加 padding 导致）
检查：链接、按钮点击区域是否足够大（至少不“点文字才生效”）
7）提交（10分钟）
建议两次 commit：

style: improve layout with box model
refactor: remove br spacing; polish form layout
Day2 完成标准（通过线）
满足这 4 条就算过关：

全局 border-box 已加，并能解释原因
三个 section 卡片化且风格统一
去掉 <br> 做间距，结构更语义化
表单排版整齐、移动端不溢出
