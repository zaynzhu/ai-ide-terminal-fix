---
name: safe-terminal-runner
description: 强制 AI 采用“临时文件+环境变量隔离”的模式运行脚本，彻底解决 Windows 下单行命令转义报错、终端卡死问题。
tags: [terminal, robust, backend, windows-fix]
---

# 终端执行与脚本运行规则 (Terminal & Script Execution Rules)

在需要执行包含复杂逻辑、环境变量、特殊字符（如单/双引号、括号、`%`、`$`等）的 Node.js 脚本或数据库操作时，必须遵守以下强制规则：

## 🚫 绝对禁止 (Prohibited)
- **绝对禁止**使用 `node -e "..."` 或 `python -c "..."` 这种单行内联脚本来执行复杂的逻辑。
- 严禁在终端单行命令中拼接包含 SQL 语句、JSON 解析或复杂正则的字符串，以防 Windows PowerShell 或 Bash 环境下的转义错误和命令别名冲突（例如将 `%` 误解析为 `ForEach-Object`）。

## ✅ 强制做法 (Mandatory)
当需要运行一次性脚本（如更新数据库结构、迁移数据、测试 API）时：

1. **创建临时文件**：先在项目合适的目录（如 `scripts/` 或当前操作目录）生成一个完整的临时脚本文件（如 `temp_update_db.js` 或 `temp_task.ts`）。
2. **写入完整代码**：将所有逻辑清晰地写入该文件。临时脚本必须在文件顶部显式加载环境变量，不依赖外部环境注入：
    ```javascript
    import 'dotenv/config'; // ESM
    // 或
    require('dotenv').config(); // CJS
    ```
3. **执行文件**：在终端通过标准命令运行该文件，例如 `node temp_update_db.js`。
4. **清理现场**：确认结果后必须立即删除该临时文件，保持项目整洁。

> **注意**：所有临时脚本统一使用 `temp_` 前缀命名，并在 `.gitignore` 中加入 `temp_*` 规则，防止意外提交。

## ⚠️ 异常处理 (Error Handling)
如果执行过程中终端卡住或出现意外的 prompt 提示，必须立即停止当前操作，检查转义规则，并改用独立文件执行的方式重试。
