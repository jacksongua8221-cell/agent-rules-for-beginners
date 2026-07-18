# AGENTS.md 小白开发必备规则模板

一个给 Codex、Claude Code、Cursor、ChatGPT Agent、多 Agent 协作使用的通用 `AGENTS.md` 模板。

它的目标很简单：让 AI Agent 少废话、少写垃圾日志、不乱改文件、不迎合错误需求、做事前先问清楚、做完必须验证。

## 适合谁

- 刚开始用 AI 写代码的小白开发者
- 经常让 AI Agent 改项目、部署项目的人
- 使用 Codex / Claude Code / Cursor / GitHub Copilot Agent 的用户
- 需要多 Agent 协作，但不想日志爆炸、上下文污染的人
- 想把项目规则固定下来，避免 AI 乱发挥的人

## 解决什么问题

- AI 一直讨好你，不敢指出错误
- 对话越来越长，Agent 越来越慢
- 多 Agent 把日志、报告、上下文写爆
- 一个项目的日志串到另一个项目
- AI 没读代码就开始乱改
- AI 顺手改了你没让它改的文件
- AI 说完成了，但没有验证
- 中文乱码时乱猜内容
- 生产环境被误改、密钥被写进日志

## 文件内容

核心文件：

```text
AGENTS.md
```

它包含：

- Agent 启动规则
- 项目前置问答规则
- 不迎合用户规则
- Karpathy 风格工程规则
- 多 Agent 协作限制
- 日志输出限制
- 项目日志隔离
- UTF-8 中文乱码处理
- 生产环境安全规则
- Agent 总结格式

## 快速安装

### 方法一：手动复制

把本仓库里的 `AGENTS.md` 复制到你的项目根目录：

```text
your-project/
  AGENTS.md
  package.json
  src/
```

然后在新对话开头告诉 Agent：

```text
开工前先读取项目根目录 AGENTS.md，并声明已加载。必须遵守其中规则。
```

### 方法二：PowerShell 复制

```powershell
Copy-Item ".\AGENTS.md" "你的项目路径\AGENTS.md" -Force
```

### 方法三：作为全局母版

你可以放一份到固定目录：

```text
D:\AI-Rules\AGENTS.md
```

以后新项目开始时复制一份到项目根目录。

## 推荐使用方式

每个项目根目录都放一份：

```text
project-a\AGENTS.md
project-b\AGENTS.md
project-c\AGENTS.md
```

不要只放在 `.codex`、系统目录或某个聊天记录目录里。  
最稳的方式就是：**每个项目根目录一份**。

## 多 Agent 使用建议

默认最多同时 3 个 Agent：

- 实现 Agent
- 验收 / QA Agent
- 部署 / 集成 Agent

每个 Agent 必须有明确边界：

```text
前端 Agent：只改 UI 和交互
后端 Agent：只改 API 和数据库
验收 Agent：只检查，不写业务代码
```

任务完成后，Agent 只写短总结，不保留长日志。

## 日志限制

推荐所有命令都限制输出：

```powershell
some-command 2>&1 | Select-Object -Last 80
```

```bash
some-command 2>&1 | tail -n 80
```

不要把几千行构建日志、部署日志、测试日志复制给 Agent。  
那会污染上下文、拖慢响应、浪费 token，还可能把磁盘写爆。

## SEO 关键词

AGENTS.md, AI Agent rules, Codex AGENTS.md, Claude Code CLAUDE.md, Cursor rules, 多 Agent 协作, AI 编程规范, 小白开发, AI 写代码规则, Agent 日志限制, Karpathy coding rules, AI 项目约束模板。

## 参考

灵感参考：

- [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)

本模板在此基础上加入了更适合小白开发和多 Agent 协作的规则：日志隔离、进度汇报、UTF-8 乱码处理、生产安全、任务关闭总结。

## License

MIT
