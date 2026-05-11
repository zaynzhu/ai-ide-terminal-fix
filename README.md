<div align="center">

# ✦ AI Rules Hub

**个人 AI 规则合集** · 将专业行为约束封装为可复用的规则文件

[![Rules](https://img.shields.io/badge/rules-1-6366f1?style=flat-square&logo=shield-check&logoColor=white)](./rules/)
[![License](https://img.shields.io/badge/license-MIT-0ea5e9?style=flat-square)](./LICENSE.md)

</div>

---

## 什么是 Rule？

Rule 是不构成独立 Skill、但值得全局遵守的行为约束。它比 Skill 更轻量——几条规则、几句话，就能让 AI 避开特定场景下的常见坑。每个 Rule 以单个 Markdown 文件存放在 `rules/` 目录下。

---

## 规则索引

| &nbsp; | 规则 | 简介 | 使用方式 |
|:------:|------|------|---------|
| 🛡️ | [**safe-terminal-runner**](./rules/safe-terminal-runner.md) | 禁止 AI 用单行内联脚本执行复杂逻辑，强制采用"临时文件+环境变量隔离"模式，解决 Windows 下转义报错与终端卡死 | 追加到 `.cursorrules` / `.windsurfrules` / 系统提示 |

---

## 如何使用

根据你使用的 IDE 或工具，将对应规则文件的内容复制到项目配置中：

- **Cursor**: 追加到 `.cursorrules`
- **Windsurf**: 追加到 `.windsurfrules`
- **Trae**: 追加到 `.trae/rules/project_rules.md`
- **CLI Agents (Cline / Aider)**: 粘贴到 Custom System Prompt
- **Claude Code / Opencode**: 将规则文件路径告知工具，或复制到系统提示

> 🛡️ **防御提示**：为防止 AI 生成的临时脚本污染代码库，建议在项目 `.gitignore` 中添加 `temp_*` 规则。

---

## 目录结构

```
ai-ide-terminal-fix/
├── README.md
├── LICENSE.md
└── rules/
    └── <rule-name>.md     ← 每条规则一个文件
```

---

## 添加新规则

```bash
# 1. 创建规则文件（小写连字符命名）
touch rules/my-new-rule.md

# 2. 在本文件的规则索引中补充一行记录
```

---

<div align="center">
<sub>持续更新中 · 欢迎 Fork 构建你自己的规则库</sub>
</div>