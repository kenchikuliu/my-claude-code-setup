# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## AI Guidance

* Ignore GEMINI.md and GEMINI-*.md files
* To save main context space, for code searches, inspections, troubleshooting or analysis, use code-searcher subagent where appropriate - giving the subagent full context background for the task(s) you assign it.
* After receiving tool results, carefully reflect on their quality and determine optimal next steps before proceeding. Use your thinking to plan and iterate based on this new information, and then take the best next action.
* For maximum efficiency, whenever you need to perform multiple independent operations, invoke all relevant tools simultaneously rather than sequentially.
* Before you finish, please verify your solution
* Do what has been asked; nothing more, nothing less.
* NEVER create files unless they're absolutely necessary for achieving your goal.
* ALWAYS prefer editing an existing file to creating a new one.
* NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.
* When you update or modify core context files, also update markdown documentation and memory bank
* When asked to commit changes, exclude CLAUDE.md and CLAUDE-*.md referenced memory bank system files from any commits. Never delete these files.

## Memory Bank System

This project uses a structured memory bank system with specialized context files. Always check these files for relevant information before starting work:

### Core Context Files

* **CLAUDE-activeContext.md** - Current session state, goals, and progress (if exists)
* **CLAUDE-patterns.md** - Established code patterns and conventions (if exists)
* **CLAUDE-decisions.md** - Architecture decisions and rationale (if exists)
* **CLAUDE-troubleshooting.md** - Common issues and proven solutions (if exists)
* **CLAUDE-config-variables.md** - Configuration variables reference (if exists)
* **CLAUDE-temp.md** - Temporary scratch pad (only read when referenced)

**Important:** Always reference the active context file first to understand what's currently being worked on and maintain session continuity.

### Memory Bank System Backups

When asked to backup Memory Bank System files, you will copy the core context files above and @.claude settings directory to directory @/path/to/backup-directory. If files already exist in the backup directory, you will overwrite them.

## Project Overview

## 🚀 Claude Code 飞书智能通知系统

### 集成配置

Claude Code 已集成智能飞书通知系统，能够自动从对话交互中提取任务信息并发送到飞书群。

**飞书Webhook配置:**
- Webhook URL: `https://www.feishu.cn/flow/api/trigger-webhook/e6704c788710bd238211e9d833129b49`
- 格式: 飞书自动化流程标准JSON格式

### 使用方法

#### 方法1: 智能对话分析（推荐）

```python
# 导入智能分析模块
import sys
sys.path.append("G:/AGI/message-pusher")

from claude_auto_summarizer import send_conversation_summary

# 在任务完成时调用
user_input = "用户的原始请求"
claude_output = "Claude的完整回应"

send_conversation_summary(user_input, claude_output)
```

#### 方法2: 手动通知

```python
import sys
sys.path.append("G:/AGI/message-pusher")

from claude_notify_final import send_claude_notification

send_claude_notification(
    task_name="任务名称",
    status="success",  # success|failed|running
    result="任务结果描述",
    task_type="Custom",  # Custom|Bash|Write|Edit
    duration_sec=30
)
```

#### 方法3: 命令行调用

```bash
# 智能分析方式
python "G:/AGI/message-pusher/claude_auto_summarizer.py" "用户输入" "Claude输出"

# 手动指定方式
python "G:/AGI/message-pusher/claude_notify_final.py" "任务名" "success" "结果" "Custom" 30
```

### 通用集成函数

```python
def notify_claude_task_completion(task_description, output_summary="", status="success"):
    """通用的Claude Code任务完成通知函数"""
    import sys, os

    notify_path = os.environ.get("CLAUDE_NOTIFY_PATH", "G:/AGI/message-pusher")
    sys.path.append(notify_path)

    try:
        from claude_auto_summarizer import send_conversation_summary
        send_conversation_summary(task_description, output_summary)
    except ImportError:
        print("Claude通知系统未找到，请检查路径配置")
    except Exception as e:
        print(f"发送Claude通知失败: {e}")

# 在任何Claude Code脚本末尾添加：
notify_claude_task_completion(
    "当前脚本执行的任务描述",
    "脚本执行的结果和输出摘要"
)
```

## 📱 VS Code 集成配置

### VS Code 增强设置

基于 Anthony's VS Code Settings 优化的 Claude Code 专用配置：

```json
{
  // Claude Code 集成设置
  "claude.code.integration.enabled": true,
  "claude.notification.feishu.enabled": true,
  "claude.notification.webhook": "https://www.feishu.cn/flow/api/trigger-webhook/e6704c788710bd238211e9d833129b49",
  "claude.tasks.auto.notify": true,
  "claude.debug.verbose": false,
  "claude.workspace.detection": true,

  // 基于Anthony's优化的开发环境
  "workbench.colorTheme": "Vitesse Dark",
  "editor.fontFamily": "Input Mono, monospace",
  "workbench.iconTheme": "catppuccin-mocha",
  "workbench.productIconTheme": "icons-carbon",
  "workbench.sideBar.location": "right",

  // ESLint 配置 (antfu/eslint-config)
  "eslint.quiet": true,
  "eslint.validate": ["javascript", "typescript", "vue", "markdown", "json"],

  // 开发效率提升
  "editor.inlineSuggest.enabled": true,
  "editor.stickyScroll.enabled": true,
  "github.copilot.enable": { "*": true, "markdown": true },
  "explorer.fileNesting.enabled": true
}
```

### VS Code 代码片段

Claude Code 专用代码片段，支持快速插入通知代码：

| 快捷键 | 功能 | 描述 |
|--------|------|------|
| `cn` | 智能通知 | 快速插入智能对话分析通知 |
| `cnm` | 手动通知 | 手动指定状态和结果的通知 |
| `cnf` | 助手函数 | 通用的Claude通知助手函数 |

### 推荐扩展 (27个精选)

基于 Anthony Fu 的扩展配置：

**核心开发工具:**
- `antfu.vite` - Vite 集成
- `Vue.volar` - Vue 3 支持
- `dbaeumer.vscode-eslint` - ESLint 集成
- `GitHub.copilot` - AI 代码助手

**主题和视觉:**
- `antfu.theme-vitesse` - Vitesse 主题
- `Catppuccin.catppuccin-vsc-icons` - Catppuccin 图标
- `antfu.icons-carbon` - Carbon 产品图标

**质量和效率:**
- `usernamehw.errorlens` - 错误高亮
- `streetsidesoftware.code-spell-checker` - 拼写检查
- `eamodio.gitlens` - Git 增强

### VS Code 任务配置

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Claude: Test Feishu Notification",
      "type": "shell",
      "command": "python",
      "args": ["path/to/test_feishu_notify.py"],
      "group": "test"
    },
    {
      "label": "Claude: Quick Notification Demo",
      "type": "shell",
      "command": "python",
      "args": ["path/to/demo_claude_notification.py"],
      "group": "test"
    }
  ]
}
```



## ALWAYS START WITH THESE COMMANDS FOR COMMON TASKS

**Task: "List/summarize all files and directories"**

```bash
fd . -t f           # Lists ALL files recursively (FASTEST)
# OR
rg --files          # Lists files (respects .gitignore)
```

**Task: "Search for content in files"**

```bash
rg "search_term"    # Search everywhere (FASTEST)
```

**Task: "Find files by name"**

```bash
fd "filename"       # Find by name pattern (FASTEST)
```

### Directory/File Exploration

```bash
# FIRST CHOICE - List all files/dirs recursively:
fd . -t f           # All files (fastest)
fd . -t d           # All directories
rg --files          # All files (respects .gitignore)

# For current directory only:
ls -la              # OK for single directory view
```

### BANNED - Never Use These Slow Tools

* ❌ `tree` - NOT INSTALLED, use `fd` instead
* ❌ `find` - use `fd` or `rg --files`
* ❌ `grep` or `grep -r` - use `rg` instead
* ❌ `ls -R` - use `rg --files` or `fd`
* ❌ `cat file | grep` - use `rg pattern file`

### Use These Faster Tools Instead

```bash
# ripgrep (rg) - content search 
rg "search_term"                # Search in all files
rg -i "case_insensitive"        # Case-insensitive
rg "pattern" -t py              # Only Python files
rg "pattern" -g "*.md"          # Only Markdown
rg -1 "pattern"                 # Filenames with matches
rg -c "pattern"                 # Count matches per file
rg -n "pattern"                 # Show line numbers 
rg -A 3 -B 3 "error"            # Context lines
rg " (TODO| FIXME | HACK)"      # Multiple patterns

# ripgrep (rg) - file listing 
rg --files                      # List files (respects •gitignore)
rg --files | rg "pattern"       # Find files by name 
rg --files -t md                # Only Markdown files 

# fd - file finding 
fd -e js                        # All •js files (fast find) 
fd -x command {}                # Exec per-file 
fd -e md -x ls -la {}           # Example with ls 

# jq - JSON processing 
jq. data.json                   # Pretty-print 
jq -r .name file.json           # Extract field 
jq '.id = 0' x.json             # Modify field
```

### Search Strategy

1. Start broad, then narrow: `rg "partial" | rg "specific"`
2. Filter by type early: `rg -t python "def function_name"`
3. Batch patterns: `rg "(pattern1|pattern2|pattern3)"`
4. Limit scope: `rg "pattern" src/`

### INSTANT DECISION TREE

```
User asks to "list/show/summarize/explore files"?
  → USE: fd . -t f  (fastest, shows all files)
  → OR: rg --files  (respects .gitignore)

User asks to "search/grep/find text content"?
  → USE: rg "pattern"  (NOT grep!)

User asks to "find file/directory by name"?
  → USE: fd "name"  (NOT find!)

User asks for "directory structure/tree"?
  → USE: fd . -t d  (directories) + fd . -t f  (files)
  → NEVER: tree (not installed!)

Need just current directory?
  → USE: ls -la  (OK for single dir)
```
