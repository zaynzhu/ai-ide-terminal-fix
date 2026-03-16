MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[🇺🇸 English](README.md)

**一行规则，彻底终结 AI 在终端里瞎跑单行命令导致的卡死与报错。**

## 🤔 痛点

在使用各类 AI 辅助编程工具（如 Cursor, Trae, Windsurf）时，AI 经常会试图通过 `node -e "..."` 或 `python -c "..."` 在终端单行执行复杂的逻辑。

由于 Windows PowerShell 和 Bash 对单/双引号、`%`、`$` 的转义规则完全不同，这种行为会导致：
- ❌ PowerShell 将 SQL 注释里的 `%` 误解析为 `ForEach-Object` 导致终端卡死。
- ❌ 复杂的 JSON 字符串在命令行拼接时引号闭合失败。
- ❌ AI 沙箱环境丢失关键的环境变量（如 `.env` 里的数据库密码）。

## 💡 解决方案

本规则强制约束 AI 的行为模式，将其从“危险的单行命令狂人”转变为“严谨的工程化专家”。它会强制 AI：
1. 创建带有 `temp_` 前缀的独立临时脚本文件。
2. 在脚本内部显式引入 `dotenv` 加载环境变量。
3. 执行文件，并在完成后自动删除清理现场。

## 🚀 快速开始

根据你使用的 IDE，将本仓库中 [`rules/rule_zh-CN.md`](rules/rule_zh-CN.md) 的内容复制到你的项目根目录下：

- **Cursor**: 复制并追加到 `.cursorrules`
- **Windsurf**: 复制并追加到 `.windsurfrules`
- **Trae**: 复制并追加到 `.trae/rules/project_rules.md` 
- **CLI 代理 (Cline / Aider)**: 粘贴到你的 Custom System Prompt 中

---

### 🛡️ 防御机制说明

为了防止 AI 生成的临时测试数据污染你的代码库，强烈建议在你的项目 `.gitignore` 中添加以下规则：

```
gitignore
# Ignore AI temporary scripts
temp_*
```