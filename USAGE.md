# Claude Code Setup 使用指南

## 🎯 快速开始

这个仓库包含了完整的 Claude Code 配置，集成了飞书智能通知系统和 VS Code 开发环境优化。

## 📁 文件结构

```
my-claude-code-setup/
├── CLAUDE.md                        # Claude Code 主配置文件
├── vscode-claude-enhanced-settings.json  # VS Code 增强设置
├── claude-code-snippets.json        # Claude Code 代码片段
├── vscode-claude-tasks.json         # VS Code 任务配置
├── USAGE.md                         # 使用指南 (本文件)
└── README.md                        # 项目说明
```

## 🚀 配置安装

### 1. Claude Code 全局配置

将 `CLAUDE.md` 复制到您的项目根目录或全局位置：

```bash
# 全局配置
cp CLAUDE.md ~/CLAUDE.md

# 或项目配置
cp CLAUDE.md /path/to/your/project/CLAUDE.md
```

### 2. VS Code 配置

#### 设置文件
将 `vscode-claude-enhanced-settings.json` 的内容复制到 VS Code 用户设置：

1. 打开 VS Code
2. 按 `Ctrl+Shift+P` (或 `Cmd+Shift+P`)
3. 输入 "Preferences: Open Settings (JSON)"
4. 将配置内容合并到您的 `settings.json`

#### 代码片段
将 `claude-code-snippets.json` 添加到 VS Code 代码片段：

1. 按 `Ctrl+Shift+P` (或 `Cmd+Shift+P`)
2. 输入 "Preferences: Configure User Snippets"
3. 选择 "python.json"
4. 将片段内容合并到文件中

#### 任务配置
将 `vscode-claude-tasks.json` 复制到项目的 `.vscode` 目录：

```bash
mkdir -p .vscode
cp vscode-claude-tasks.json .vscode/tasks.json
```

## ✨ 功能特性

### 🤖 飞书智能通知

- **自动分析**: 智能提取任务信息和执行状态
- **多种调用方式**: 智能分析、手动指定、命令行调用
- **实时通知**: 每个 Claude Code 任务完成后自动发送飞书消息

### 🎨 VS Code 开发环境

- **Vitesse 主题**: 优雅的深色/浅色主题
- **Input Mono 字体**: 专业的编程字体
- **智能工具集成**: ESLint、Copilot、GitLens 等
- **文件嵌套**: 清晰的项目结构显示

### ⚡ 快速开发

- **代码片段**: `cn`、`cnm`、`cnf` 快捷键
- **VS Code 任务**: 一键测试和演示
- **智能建议**: 开启粘性滚动和内联建议

## 🔧 使用方法

### 智能通知 (推荐)

在任何 Python 脚本中添加：

```python
import sys
sys.path.append("G:/AGI/message-pusher")
from claude_auto_summarizer import send_conversation_summary

# 任务完成后调用
send_conversation_summary("用户请求", "Claude回应")
```

### 快捷键使用

在 VS Code 中：

- 输入 `cn` + Tab → 插入智能通知代码
- 输入 `cnm` + Tab → 插入手动通知代码
- 输入 `cnf` + Tab → 插入通知助手函数

### VS Code 任务

按 `Ctrl+Shift+P`，输入 "Tasks: Run Task"，选择：
- **Claude: Test Feishu Notification** - 测试通知功能
- **Claude: Quick Notification Demo** - 演示通知场景

## 📱 飞书通知配置

### Webhook 设置

当前配置的 Webhook URL：
```
https://www.feishu.cn/flow/api/trigger-webhook/e6704c788710bd238211e9d833129b49
```

### 消息格式

每条通知包含：
- **任务名称**: 智能提取或手动指定
- **执行状态**: success/failed/running
- **结果详情**: 详细的执行结果
- **任务类型**: Bash/Write/Edit/Custom
- **项目信息**: 自动检测项目名称和路径

## 🎯 实际应用场景

### 代码生成任务
```python
notify_claude_task_completion(
    "生成React组件代码",
    "成功生成了5个React组件，包含TypeScript类型定义和测试文件。"
)
```

### 数据处理任务
```python
notify_claude_task_completion(
    "CSV数据清洗",
    "处理了3个文件，清理了1,200条重复数据，质量提升至98%。"
)
```

### 部署任务
```python
notify_claude_task_completion(
    "Docker应用部署",
    "构建成功，部署完成，服务已启动并通过健康检查。"
)
```

## 🔍 故障排除

### 通知发送失败

1. 检查网络连接
2. 验证 Webhook URL 是否正确
3. 确保 message-pusher 路径配置正确

### VS Code 配置问题

1. 确保扩展已安装
2. 检查设置是否正确合并
3. 重启 VS Code 使配置生效

### 代码片段不工作

1. 确认片段文件位置正确
2. 检查作用域设置 (scope: "python")
3. 重新加载 VS Code 窗口

## 📚 更多资源

- [Claude Code 官方文档](https://claude.ai/code)
- [Anthony's VS Code Settings](https://github.com/antfu/vscode-settings)
- [Vitesse Theme](https://github.com/antfu/vscode-theme-vitesse)

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个配置！

---

🎉 享受您的 Claude Code 开发体验！