# 🛡️ Safe Script Runner for AI IDEs

[![Support](https://img.shields.io/badge/Support-Cursor%20%7C%20Trae%20%7C%20Windsurf%20%7C%20Cline-blue)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[🇨🇳 中文文档 (Chinese)](README_zh-CN.md)

**A single rule to stop AI from freezing your terminal with broken single-line commands.**

## 🤔 The Problem

When using AI-assisted coding tools (like Cursor, Trae, Windsurf, or Cline), the AI often tries to execute complex logic using single-line inline scripts in the terminal, such as `node -e "..."` or `python -c "..."`.

Because environments like Windows PowerShell and Bash have completely different rules for escaping single/double quotes, `%`, and `$`, this behavior often leads to:
- ❌ PowerShell misinterpreting `%` in SQL comments as `ForEach-Object`, causing the terminal to freeze and wait for input.
- ❌ Broken quote closures when parsing complex JSON strings in the CLI.
- ❌ Loss of crucial environment variables (like database passwords from `.env`) within the AI sandbox.

## 💡 The Solution

This directive forces the AI to abandon the risky "inline command" habit and adopt a strict, robust engineering workflow:
1. Create a standalone temporary script file prefixed with `temp_`.
2. Explicitly load `dotenv` to ensure environment variables are present.
3. Execute the file cleanly, and automatically delete it afterward to maintain a pristine workspace.

## 🚀 Quick Start

Depending on your IDE, copy the contents of [`rules/rule.md`](rules/rule.md) (or [`rules/rule_zh-CN.md`](rules/rule_zh-CN.md) for Chinese prompts) into your project's configuration file:

- **Cursor**: Append to `.cursorrules`
- **Windsurf**: Append to `.windsurfrules`
- **Trae**: Append to `.trae/rules/project_rules.md`
- **CLI Agents (Cline / Aider)**: Paste into your Custom System Prompt.

---

### 🛡️ Best Practice

To prevent the AI's temporary test data or hardcoded credentials from polluting your repository, add the following to your project's `.gitignore`:

```
gitignore
# Ignore AI temporary scripts
temp_*
```