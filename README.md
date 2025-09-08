# 🐱 喵喵AI聊天应用模板

一个基于 Cloudflare Workers AI 的简单易部署聊天应用模板。该模板为构建具有流式响应的AI聊天应用提供了一个干净的起点。

[![部署到 Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/cloudflare/templates/tree/main/llm-chat-app-template)

<!-- dash-content-start -->

## 演示

该模板展示了如何使用 Cloudflare Workers AI 构建具有流式响应的AI聊天界面。功能包括：

- 使用服务器发送事件 (SSE) 实时流式传输AI响应
- 轻松自定义模型和系统提示
- 支持 AI Gateway 集成
- 简洁响应式UI，兼容移动端和桌面端

## 特性

- 💬 简洁响应式聊天界面
- ⚡ 服务器发送事件 (SSE) 流式响应
- 🧠 由 Cloudflare Workers AI 大语言模型驱动
- 🛠️ 使用 TypeScript 和 Cloudflare Workers 构建
- 📱 移动端友好设计
- 🔄 在客户端维护聊天历史
- 🔎 内置可观测性日志
<!-- dash-content-end -->

## 快速开始

### 前置条件

- [Node.js](https://nodejs.org/) (v18 或更新版本)
- [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/)
- 拥有 Workers AI 访问权限的 Cloudflare 账户

### 安装

1. 克隆此仓库：

   ```bash
   git clone https://github.com/cloudflare/templates.git
   cd templates/llm-chat-app
   ```

2. 安装依赖：

   ```bash
   npm install
   ```

3. 生成 Worker 类型定义：
   ```bash
   npm run cf-typegen
   ```

### 开发

启动本地开发服务器：

```bash
npm run dev
```

这将在 http://localhost:8787 启动本地服务器。

注意：使用 Workers AI 即使在本地开发时也会访问您的 Cloudflare 账户，这将产生使用费用。

### 部署

部署到 Cloudflare Workers：

```bash
npm run deploy
```

### 监控

查看与任何已部署 Worker 相关的实时日志：

```bash
npm wrangler tail
```

## 项目结构

```
/
├── public/             # 静态资源
│   ├── index.html      # 聊天UI HTML文件
│   └── chat.js         # 聊天UI前端脚本
├── src/
│   ├── index.ts        # 主要 Worker 入口点
│   └── types.ts        # TypeScript 类型定义
├── test/               # 测试文件
├── wrangler.jsonc      # Cloudflare Worker 配置
├── tsconfig.json       # TypeScript 配置
└── README.md           # 本文档
```

## 工作原理

### 后端

后端使用 Cloudflare Workers 构建，并使用 Workers AI 平台生成响应。主要组件包括：

1. **API 端点** (`/api/chat`)：接受包含聊天消息的 POST 请求并流式传输响应
2. **流式传输**：使用服务器发送事件 (SSE) 实时流式传输AI响应
3. **Workers AI 绑定**：通过 Workers AI 绑定连接到 Cloudflare 的AI服务

### 前端

前端是一个简单的 HTML/CSS/JavaScript 应用程序，它：

1. 提供聊天界面
2. 将用户消息发送到API
3. 实时处理流式响应
4. 在客户端维护聊天历史

## 自定义

### 更改模型

要使用不同的AI模型，请更新 `src/index.ts` 中的 `MODEL_ID` 常量。您可以在 [Cloudflare Workers AI 文档](https://developers.cloudflare.com/workers-ai/models/) 中找到可用模型。

### 使用 AI Gateway

模板包含用于 AI Gateway 集成的注释代码，它提供了额外的功能，如速率限制、缓存和分析。

要启用 AI Gateway：

1. 在您的 Cloudflare 控制面板中[创建 AI Gateway](https://dash.cloudflare.com/?to=/:account/ai/ai-gateway)
2. 取消注释 `src/index.ts` 中的网关配置
3. 将 `YOUR_GATEWAY_ID` 替换为您实际的 AI Gateway ID
4. 根据需要配置其他网关选项：
   - `skipCache`：设置为 `true` 以绕过网关缓存
   - `cacheTtl`：设置缓存生存时间（秒）

了解更多关于 [AI Gateway](https://developers.cloudflare.com/ai-gateway/) 的信息。

### 修改系统提示

可以通过更新 `src/index.ts` 中的 `SYSTEM_PROMPT` 常量来更改默认系统提示。

### 样式

UI 样式包含在 `public/index.html` 的 `<style>` 部分中。您可以修改顶部的 CSS 变量来快速更改配色方案。

## 🐱 猫咪主题自定义

### 修改为猫咪主题

1. **更新 `public/index.html`**：
   ```html
   <title>🐱 喵喵AI助手</title>
   <h1>🐱 喵喵AI助手</h1>
   <p>你的贴心猫咪AI伙伴 🐾</p>
   ```

2. **更新系统提示** (`src/index.ts`)：
   ```typescript
   const SYSTEM_PROMPT = "你是一只可爱的猫咪AI助手，名叫小喵。你的性格温柔、友善、有点调皮。在回答问题时，偶尔会用'喵~'来表达，但不要过度使用。";
   ```

3. **猫咪主题配色**：
   ```css
   :root {
     --primary-color: #ff6b35;     /* 橙猫色 */
     --primary-hover: #e55a2b;
     --user-msg-bg: #fff4e6;       /* 温暖奶茶色 */
     --assistant-msg-bg: #f0f9ff;  /* 浅蓝色 */
   }
   ```

## 资源

- [Cloudflare Workers 文档](https://developers.cloudflare.com/workers/)
- [Cloudflare Workers AI 文档](https://developers.cloudflare.com/workers-ai/)
- [Workers AI 模型](https://developers.cloudflare.com/workers-ai/models/)

## 部署命令

```bash
# 安装依赖
npm install

# 本地开发
npm run dev

# 部署到生产环境
npm run deploy

# 查看实时日志
npm run tail
```

---

🐾 **现在你有了一个完整的中文猫咪主题AI聊天应用！** 🐱
