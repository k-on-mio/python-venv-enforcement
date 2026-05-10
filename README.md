# python-venv-enforcement

一个 OpenCode / Claude Code 技能，强制 AI 编程助手掌写 Python 脚本时使用虚拟环境。

每当 AI 要写带外部依赖的 Python 脚本时，必须先创建并激活 venv — 没有例外。

## 功能

- 自动检测需要外部依赖的 Python 任务
- 强制在 `pip install` 之前创建 venv
- 处理 Windows 执行策略限制的绕过方案
- 反辩心理表：针对 AI 可能产生的各种借口逐一反驳
- 兼容 OpenCode、Claude Code 等支持 Superpowers 的智能体

## 安装

将 `SKILL.md` 放入对应智能体的 skills 目录：

**OpenCode：**
```
~/.config/opencode/skills/python-venv-enforcement/SKILL.md
```

**Claude Code：**
```
~/.claude/skills/python-venv-enforcement/SKILL.md
```

## 使用

技能自动触发。只要让 AI 写一个 Python 脚本，它会在写代码之前先搭好 venv。

## 许可

MIT
