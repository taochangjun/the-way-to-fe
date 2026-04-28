# 前端自学 Day1-Day30 日计划表

> 节奏建议：工作日 1.5-2h，周末 3-4h。  
> 每天固定结构：30 分钟学习 + 60 分钟实战 + 20 分钟复盘。

## Day1-Day10（HTML/CSS/响应式 + JS基础 + DOM入门）

| Day | 学习重点 | 实战任务 | 验收标准 |
|---|---|---|---|
| Day1 | HTML 语义化、页面结构 | 个人主页基础结构（header/main/section/footer） | 页面结构清晰，只有一个 `h1` |
| Day2 | 盒模型、间距管理、`border-box` | 卡片化页面、表单排版 | 无 `<br>` 调间距，布局不溢出 |
| Day3 | Flex 布局 | 导航 + 卡片流 + footer 响应式 | 能解释主轴/交叉轴，布局可换行 |
| Day4 | Position 定位 | sticky 导航 + absolute 角标 + fixed 回顶 | 能说清四种定位的适用场景 |
| Day5 | Responsive 响应式 | 375/768/1024 三档布局切换 | 无横向滚动，手机可读可点 |
| Day6 | JS 基础语法与数据类型 | 变量/条件/循环 + 小算法练习 | 能独立写基础流程控制，不依赖复制粘贴 |
| Day7 | 函数与作用域 | 函数拆分、参数/返回值、作用域与闭包直觉 | 能把一段脚本拆成 3-5 个职责清晰的函数 |
| Day8 | 数组与对象高阶操作 | `map/filter/reduce/find/some` 做数据转换与统计 | 能用数据驱动思路组织列表数据 |
| Day9 | DOM 操作与事件（1） | 选择元素、改文本/样式、事件监听、表单实时回显 | 能用 `querySelector` + `addEventListener` 完成交互 |
| Day10 | DOM 操作与事件（2） | `createElement/append/remove` + 事件委托 + `localStorage` 小整合 | 可完成原生 JS 小 Todo（增删改查+持久化） |

## Day11-Day30（进阶总览：异步与语言进阶 → 工程化与 TS → Vue 生态 → 网络与综合项目）

> 你已具备 **HTML/CSS 布局**，并在 Day6-Day10 完成了 **JS 基础 + DOM 两天入门**。Day11 起按「全栈友好」顺序推进：**异步与事件循环** → **原型/模块化** → **工程化与 TypeScript** → **Vue3 系统化** → **网络与后端交互** → **性能与综合实战**。  
> 组件库建议二选一贯穿管理端：**Ant Design Vue**（与下文后台项目一致）或 **Element Plus**（文档与社区同样成熟）。

### 阶段划分（对应进阶路线一至七）

| 阶段 | Day 范围 | 方向 |
|---|---|---|
| A | Day11–14 | JavaScript 进阶（异步、事件循环、原型与 class、模块化） |
| B | Day16–18 | 工程化与工具链（包管理、Vite、Git、环境变量与代理） |
| C | Day19–20 | TypeScript 必学基础 + 接入 Vue SFC |
| D | Day21–25 | Vue3 深度实战（组合式 API、通信、Router、Pinia、Composables） |
| E | Day26–27 | 网络与后端交互（Axios、CORS/代理、API 心智；可选 WebSocket 最小 demo） |
| F | Day28–30 | 性能入门、综合项目（后台管理或博客全栈）、部署与总结 |

### Day11-Day20

| Day | 学习重点 | 实战任务 | 验收标准 |
|---|---|---|---|
| Day11 | 异步编程 | `Promise`、`async/await`、错误处理；`Promise.all` / `race`；用 `fetch` 调 REST，管理 loading / error | 请求失败有提示，并发场景能选对 API |
| Day12 | 事件循环（Event Loop） | 宏任务 / 微任务 / 执行栈；点击回调与 `setTimeout` 顺序实验；渲染时机初识 | 能口述一轮事件循环，并解释常见输出顺序 |
| Day13 | 原型链与 `class` | 原型链心智；`class` 语法；手写简易 **EventBus** | 能把“对象复用”与组件思维建立联系 |
| Day14 | 模块化（ES Module） | 拆分 `api/utils/store` 模块并导入导出；理解默认导出与具名导出 | 代码分层清晰，主入口不再臃肿 |
| Day15 | 阶段小复盘（JS 进阶） | 做一个“任务板”小页面：含异步加载、模块拆分、基础交互 | 能独立串联 Day11-Day14 知识点 |
| Day16 | 包管理与 Vite 脚手架 | `npm` / `pnpm`；`create vue` 或 Vite 模板；勾选 **ESLint + Prettier** | 能 `install`、`dev`、`lint` / `format`，读懂 `package.json` |
| Day17 | Git 协作 | 分支、合并、冲突解决、**PR/MR 流程**（可与自己的远程仓库练习） | 能独立完成一次 feature → main 的合并 |
| Day18 | Vite 进阶 | **环境变量**（`.env`）、`server.proxy` 开发代理、路径别名 | 本地调后端无跨域拦路，生产构建能区分环境 |
| Day19 | TypeScript 基础 | 注解、`interface` / `type`、联合 `|`、交叉 `&`、**泛型入门** | 新写代码无明显滥用 `any` |
| Day20 | TS 接入 Vue3 | `defineProps<{ }>()`、`ref<T>`、`computed` 类型；逐步迁移一小页 | SFC 中类型报错能独立对照文档解决 |

### Day21-Day30

| Day | 学习重点 | 实战任务 | 验收标准 |
|---|---|---|---|
| Day21 | 组合式 API 系统化 | `ref` / `reactive`、`computed`、`watch` / `watchEffect`、生命周期；**重构**此前小项目一页 | 能解释 `ref` vs `reactive`，副作用可控 |
| Day22 | 组件通信与插槽 | `props` / `emits`、`v-model`、`provide` / `inject`；默认 / 具名 / **作用域插槽**；封装 **通用 Modal、表格封装** | 子组件不越权改父数据，通信路径清晰 |
| Day23 | Vue Router 4 | 路由表、**动态路由**、**嵌套路由**、编程式导航、**路由守卫** | 多页壳子跑通（博客：首页/详情/后台登录 或 管理端布局） |
| Day24 | Pinia | `state` / `getters` / `actions`、**模块化** store；登录态、列表缓存 | 跨路由状态一致，store 与视图分层 |
| Day25 | Composables | 封装 `useFetch`、`useLocalStorage` 等；与 Pinia 边界划分 | 可复用逻辑抽离后，页面组件明显变薄 |
| Day26 | Axios 与鉴权 | 实例、请求/响应拦截器（**token**、统一错误提示）、401 处理 | 业务页请求路径统一，错误有用户可见反馈 |
| Day27 | CORS 与 API 心智 | 复盘 Vite 代理与 **CORS**；REST 资源命名；**WebSocket** 最小聊天/通知 demo（可选） | 能说清浏览器、网关、后端在跨域中的责任 |
| Day28 | 性能优化入门 | **路由懒加载**；组件 / 组件库 **按需引入**；`transform` 做动画；`<img loading="lazy">` 或 `IntersectionObserver` | 至少一项可量化或可感知的优化（包体或首屏） |
| Day29 | 综合实战冲刺 | **Vue3 + TS + Pinia + Router + 组件库**：后台管理（登录拦截、表格表单、**CRUD**、mock 或真实 API） | 核心业务流程完整，代码结构可维护 |
| Day30 | 部署、文档与延展清单 | 部署（Vercel / Netlify / 自有服务器）；**README + 演示说明**；列出可选延展（**Nuxt**、**Vitest**、移动端） | 有可访问链接；能向他人讲清架构与难点 |

**Day29 项目对标**：文档中的「完整后台管理系统」；若更偏全栈叙事，可改为 **个人博客**（文章列表/详情/后台登录与 CRUD），技术栈不变。

---

## 每天复盘模板（建议复制到各 Day 的 `knowledge.md`）

```md
## 今日学习总结

### 我学了什么
- 

### 我做了什么
- 

### 我遇到的问题
- 

### 我如何解决
- 

### 明天计划
- 
```

---

## 阶段验收目标

- Day10：完成“先数据再视图”的 DOM 小项目（数组驱动渲染 + 事件 + 存储）
- Day15：JavaScript 进阶闭环（异步 + 事件循环 + 原型 + 模块化能说清）
- Day18：工程化工具链跑通（Vite + 规范工具 + Git 协作一次）
- Day20：TypeScript 能读写进 Vue SFC，类型错误可自解
- Day25：Vue3 + Router + Pinia + Composables 架构清晰，可支撑业务页
- Day30：完成 1 个可上线、可演示、可写进简历的 **TS + Vue3 综合项目**（管理端或博客全栈二选一）
