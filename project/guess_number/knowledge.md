# Guess Number 学习笔记：`index.html` 中的 JavaScript 知识点

本文结合 `project/guess_number/index.html` 的实际代码，系统梳理这个小游戏里用到的 JS 核心知识。

## 1. 变量声明：`const` 与 `let`

### 1.1 `const`：引用不变
页面先通过 DOM 查询拿到元素，并用 `const` 保存：

- `const guessInput = document.getElementById("guessInput");`
- `const guessBtn = document.getElementById("guessBtn");`

这里用 `const` 的原因：

- 这些变量在初始化后不会被重新赋值到别的元素。
- 代码语义更清晰：这是“固定引用”。

### 1.2 `let`：状态会变化
游戏状态使用 `let`：

- `let targetNumber = 0;`（目标数字会在新游戏时变化）
- `let attempts = 0;`（猜测次数不断变化）
- `let guessHistory = [];`（历史记录不断追加/清空）

这体现了一个常见模式：

- **DOM 引用用 `const`**
- **业务状态用 `let`**

---

## 2. 随机数生成：`Math.random()` + `Math.floor()`

代码：

```js
function randomInt1To100() {
  return Math.floor(Math.random() * 100) + 1;
}
```

含义拆解：

- `Math.random()` 产生 `[0, 1)` 的小数
- `* 100` 变成 `[0, 100)`  
- `Math.floor(...)` 向下取整，得到 `0~99`
- `+ 1` 映射成 `1~100`

这是前端里最经典的“区间随机整数公式”。

---

## 3. 函数拆分与职责分离

该小游戏把逻辑拆成 4 个函数，每个函数职责单一：

### 3.1 `randomInt1To100`
- 只负责随机数生成（纯计算逻辑）。

### 3.2 `resetGame`
- 只负责“初始化/重置状态 + 重置界面”。
- 包括：重新生成目标数、清空次数与历史、恢复输入框与按钮状态。

### 3.3 `validateGuess(rawValue)`
- 只负责输入校验，返回错误信息或 `null`。
- 好处：把“校验规则”从主流程剥离出来，主流程更清晰。

### 3.4 `handleGuess`
- 负责一次完整猜测流程（读取输入 -> 校验 -> 更新状态 -> 给提示）。

这种写法就是“主流程函数 + 工具函数”的常见组织方式，便于维护和测试。

---

## 4. 输入处理与类型转换

### 4.1 读取输入值
- `guessInput.value` 读取的是**字符串**。

### 4.2 去空格判断
- `rawValue.trim() === ""` 检查空输入。

### 4.3 转数字
- `const value = Number(rawValue);`
- 将字符串转换成数字，后续才能做大小比较。

### 4.4 判断是否整数
- `Number.isInteger(value)` 用于限制输入为整数，避免 `12.5` 这种情况。

### 4.5 范围校验
- `value < 1 || value > 100` 保证题目约束（1-100）。

---

## 5. 条件判断：`if / else if / else`

核心比较逻辑：

- `guess > targetNumber` -> `猜大了`
- `guess < targetNumber` -> `猜小了`
- 否则就是猜中

并且校验阶段也使用 `if` 提前返回错误：

```js
if (error) {
  message.textContent = error;
  return;
}
```

这是非常实用的“**早返回（guard clause）**”写法，减少嵌套层级。

---

## 6. 状态更新：计数与历史数组

### 6.1 次数累加
- `attempts += 1;`

### 6.2 历史记录
- `guessHistory.push(guess);` 把每次有效猜测追加到数组末尾。

### 6.3 数组展示
- ``guessHistory.join(", ")`` 将数组转成字符串展示在页面。

说明：

- 这个项目里没有显式 `for/while` 循环；
- 但 `join` 在内部完成了“遍历拼接”，可以理解为“数组 API 封装了循环行为”。

---

## 7. DOM 操作：读、写、显隐、禁用

### 7.1 查询元素
- `document.getElementById(...)`

### 7.2 更新文本
- `element.textContent = "...";`
- 用于提示信息、次数、历史记录。

### 7.3 控件禁用/启用
- `guessInput.disabled = true/false`
- `guessBtn.disabled = true/false`

### 7.4 按钮显示/隐藏
- `newGameBtn.style.display = "none"`（隐藏）
- `newGameBtn.style.display = "inline-block"`（显示）

### 7.5 焦点控制
- `guessInput.focus()` 让用户重置后可直接输入，提升交互体验。

---

## 8. 事件监听：`addEventListener`

代码里绑定了三类事件：

- 点击“猜”：`guessBtn.addEventListener("click", handleGuess)`
- 输入框回车：`guessInput.addEventListener("keydown", ...)`
- 点击“新游戏”：`newGameBtn.addEventListener("click", resetGame)`

重点：

- 回车监听里判断 `event.key === "Enter"`，实现键盘操作支持；
- 同时判断 `!guessBtn.disabled`，避免游戏结束后重复触发猜测逻辑。

---

## 9. 模板字符串（反引号）

代码多次使用模板字符串动态拼接内容：

- `` `已猜次数：${attempts}` ``
- `` `历史猜测：${guessHistory.join(", ")}` ``
- `` `恭喜！猜中了！共用 ${attempts} 次` ``

好处是可读性强，比字符串加号拼接更清晰。

---

## 10. 初始化时机

脚本末尾调用：

- `resetGame();`

作用：

- 页面一加载就进入“可玩状态”，不需要用户先点“新游戏”。
- 保证 `targetNumber` 一定有值，避免未初始化状态。

---

## 11. 这份代码体现的工程思路

1. **先建状态**：目标数、次数、历史。
2. **再写规则**：输入校验、大小比较。
3. **最后连交互**：按钮点击、回车、新游戏。
4. **函数单一职责**：重置、校验、猜测处理分离。

这就是从“能跑”到“好维护”的关键一步。

---

## 12. 可继续练习的方向

- 增加“剩余机会”（例如最多 10 次）
- 增加难度选择（1-100 / 1-500）
- 把最佳成绩保存到 `localStorage`
- 把内联脚本拆到独立 `main.js`

这些都能在当前代码结构上平滑扩展。
