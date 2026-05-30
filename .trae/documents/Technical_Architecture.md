# 技术架构文档 - 山西方言Emoji猜词（晋在Emoji）

## 1. 技术选型
- **前端核心**：纯 HTML5 + CSS3 + 原生 JavaScript (ES6+)。
- **页面布局**：Viewport + rem + Flexbox，响应式竖屏设计。
- **音频合成**：Web Speech API (`SpeechSynthesisUtterance`)。
- **图像生成**：原生 Canvas 2D API（避免依赖 html2canvas）。
- **数据存储**：LocalStorage（用于存储最高分记录）。
- **运行环境**：纯离线环境，单文件运行，零网络请求。

## 2. 目录与文件结构
- **单一交付物**：`index.html`（所有 CSS 和 JS 全部内联，无任何外部资源如图片 CDN、字体文件等）。最终文件大小严格控制在 8MB 以内。

## 3. 核心状态机设计
应用将基于一个全局的状态机来控制页面渲染和逻辑走向：
- `START`：初始状态，展示开场画面。
- `PLAYING`：答题状态，倒计时开始，等待用户交互。
- `FEEDBACK`：反馈状态，展示正误结果和释义，屏蔽一切点击，维持 1.5 秒。
- `NEXT`：内部过渡状态，判断是否完成 10 题，循环进入 `PLAYING` 或进入 `RESULT`。
- `RESULT`：结算状态，展示得分、称号及回顾列表。

## 4. 核心模块与函数
- **题库管理 (`prepareQuestions`)**：
  - 使用 Fisher-Yates 算法实现洗牌函数 (`shuffle`)。
  - 从完整题库中随机抽取 10 题，并将每题的 4 个选项进行打乱。
- **渲染引擎 (`renderX`)**：
  - 基于当前状态直接操作 DOM。
  - `renderStart()`、`renderQuestion()`、`showFeedback()`、`renderResult()`。
- **计时器模块 (`Timer`)**：
  - 使用 `setInterval` 配合 CSS `transition` 控制进度条。
  - 精确倒计时 8 秒，到 0 后触发超时逻辑，自动进入 `FEEDBACK`。
- **发音模块 (`speakWord`)**：
  - 实例化 `SpeechSynthesisUtterance`。
  - 设置 `lang = 'zh-CN'`, `rate = 0.9` 优化方言听感。
- **分享卡片生成 (`generateShareCard`)**：
  - 创建离线离屏 `<canvas>`，设置尺寸 750x1334。
  - 使用 `CanvasRenderingContext2D` 绘制背景、文字、对错记录。
  - 导出 Base64 URL (`canvas.toDataURL('image/png')`) 并替换 DOM 中的 `<img>` 标签，实现长按保存。

## 5. 合规与稳定性约束
- **防抖与防连点**：在进入 `FEEDBACK` 状态后立刻设置 `answered = true`，忽略后续的所有选项点击。
- **异常捕获**：关键模块（如 Web Speech API, LocalStorage）需加入 `try-catch`，提供降级或容错提示，确保游戏不会白屏。
- **资源内联**：所有 emoji 作为文本处理，不使用图片资源。UI 装饰（如窗花）采用 CSS 绘制或内联 SVG。