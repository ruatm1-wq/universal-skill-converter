# 🦾 Universal Skill Converter

> **跨 14 种 AI Agent 格式的智能 Skill 生命周期管理引擎**  
> **Cross-platform skill format converter & lifecycle manager for 14 AI agents**

[![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)](https://python.org)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Agents](https://img.shields.io/badge/agents-14-orange)](#supported-agents)
[![GitHub](https://img.shields.io/badge/GitHub-repo-black?logo=github)](https://github.com/ruatm1-wq/universal-skill-converter)

---

**中文** | [English](#english)

---

## 中文

### 📖 简介

Universal Skill Converter **v2.0** 是一个**零依赖、单文件**的 Python 工具，能让你的 AI Agent skill 在 14 种主流格式之间自由转换。无论你是 Cursor 用户、Windsurf 开发者、Cline 爱好者还是 Reasonix 重度用户——同一个 skill 文件，一键同步到所有 Agent。

**一句话：写一次 skill，到处运行。**

### ✨ 核心能力

| 功能 | 说明 |
|:-----|:------|
| **格式转换** | 14 种 Agent 格式互相转换，无损字段映射 |
| **自动检测** | 根据文件扩展名、目录结构和 Frontmatter 关键词自动识别格式 |
| **依赖扫描** | 检测二进制工具、环境变量、Python/NPM 包依赖 |
| **兼容性评分** | A/C/F 三级评分 + 字段丢失分析 + 渲染测试 |
| **双向同步** | `sync` 命令批量同步整个 skill 目录到多个 Agent |
| **自动监控** | `watch` 命令监听文件变化，自动同步 |
| **环境感知** | 扫描项目目录，自动检测在用哪些 Agent |
| **自安装** | 把自己安装为当前 Agent 的 Skill，下次直接 `run_skill` 调用 |
| **一键引导** | 下载后一条命令完成全流程配置 |

### 🚀 快速开始

```bash
# 下载
curl -O https://raw.githubusercontent.com/ruatm1-wq/universal-skill-converter/main/universal-skill-converter.py
# 或
wget https://raw.githubusercontent.com/ruatm1-wq/universal-skill-converter/main/universal-skill-converter.py

# ⭐ 一键引导（检测环境 → 自安装 → 使用说明）
python universal-skill-converter.py --bootstrap

# 基础用法
python universal-skill-converter.py install my-skill.md          # 安装 skill
python universal-skill-converter.py check my-skill.md            # 检测兼容性
python universal-skill-converter.py inspect my-skill.md          # 查看信息
python universal-skill-converter.py list                         # 列出已安装
```

### 📋 命令参考

| 命令 | 说明 | 示例 |
|:-----|:------|:------|
| `install <file>` | 安装 skill（自动检测目标环境） | `install foo.md --to cursor,windsurf` |
| `inspect <file>` | 查看 skill 详细信息 | `inspect foo.md` |
| `check <file>` | 检测兼容性 + 依赖 | `check foo.md --json` |
| `list` | 列出已安装技能 | `list --agent windsurf` |
| `convert <file> --to <fmt>` | 导出为指定格式 stdout | `convert foo.md --to openclaw` |
| `install-dir <dir>` | 批量安装目录 | `install-dir ./skills/` |
| `sync --from <dir>` | 双向同步 | `sync --from ./skills/ --to all` |
| `watch <dir>` | 监控目录自动同步 | `watch ./skills/ --to reasonix,cursor` |
| `config` | 配置管理 | `config set default_targets cursor,windsurf` |
| `--detect-agent` | 检测当前 Agent 环境 | `--detect-agent` |
| `--self-install` | 自安装为 skill | `--self-install` |
| `--bootstrap` | ⭐ 一键引导 | `--bootstrap` |

**通用参数：** `--to <a,b>` 目标列表 / `--dry-run` 预览 / `--backup` 备份 / `--json` JSON 输出

### 🤖 支持的 14 种 Agent

| ID | Agent | 格式 | 文件位置 |
|:---|:------|:-----|:---------|
| `reasonix` | Reasonix Code | 单文件 `.md` | `.reasonix/skills/<name>.md` |
| `hermes` | Hermes Agent | 子目录 + SKILL.md | `.hermes/skills/<name>/SKILL.md` |
| `opencode` | OpenCode | 子目录 + SKILL.md | `.config/opencode/skills/<name>/SKILL.md` |
| `claude-code` | Claude Code | 子目录 + plugin.json | `.claude/plugins/<name>/SKILL.md` |
| `openai-codex` | OpenAI Codex | 子目录 + plugin.json | `.agents/plugins/<name>/SKILL.md` |
| `cursor` | Cursor | 单文件 `.mdc` | `.cursor/rules/<name>.mdc` |
| `windsurf` | Windsurf | 单文件 `.windsurfrules` | `.windsurfrules` |
| `cline` | Cline | 纯 markdown | `.clinerules` |
| `roo-code` | Roo Code | 纯 markdown | `.clinerules` + `.roomodes` |
| `github-copilot` | GitHub Copilot | 单文件 | `.github/copilot-instructions.md` |
| `continue` | Continue.dev | JSON 配置 | `~/.continue/config.json` |
| `aider` | Aider | CONVENTIONS.md | `CONVENTIONS.md` |
| `skills-cli` | Skills CLI | 子目录 + SKILL.md | `.skills/<name>/SKILL.md` |
| `openclaw` | OpenClaw | 子目录 + SKILL.md + metadata | `~/.openclaw/workspace/skills/<name>/SKILL.md` |

### 💡 典型场景

**场景 1：从网上下载一个 skill 装到所有 Agent**
```bash
python universal-skill-converter.py install ~/Downloads/research-skill.md --to all
```

**场景 2：把 Cursor 规则共享给 Cline 和 Windsurf**
```bash
python universal-skill-converter.py convert .cursor/rules/coding.mdc --to cline
```

**场景 3：同步整个技能库**
```bash
python universal-skill-converter.py sync --from ./my-skills/ --to reasonix,cursor,openclaw
```

**场景 4：自安装后从 Agent 内调用**
```python
# 在 Reasonix Code 中：
run_skill("skill-converter", "install foo.md --to cursor,windsurf")
```

---

## English

### 📖 Introduction

**Universal Skill Converter v2.0** is a **zero-dependency, single-file** Python tool that freely converts AI Agent skills across 14 mainstream formats. Write your skill once, deploy everywhere.

### ✨ Core Features

- **Format Conversion** — Convert between 14 agent formats with lossless field mapping
- **Auto-Detect** — Automatically identify format from file extension, directory structure, and frontmatter keywords
- **Dependency Scan** — Detect required binaries, environment variables, Python/NPM packages
- **Compatibility Check** — A/C/F score + field-loss analysis + render testing
- **Bidirectional Sync** — Batch sync entire skill directories to multiple agents
- **Auto Watch** — Monitor directory changes and auto-sync
- **Environment Detection** — Scan project directory to detect which agents are in use
- **Self-Install** — Install the converter itself as a skill for your agent
- **One-Click Bootstrap** — Single command to detect, install, and configure

### 🚀 Quick Start

```bash
# Download
curl -O https://raw.githubusercontent.com/ruatm1-wq/universal-skill-converter/main/universal-skill-converter.py

# ⭐ Bootstrap: detect → self-install → guide
python universal-skill-converter.py --bootstrap

# Basic usage
python universal-skill-converter.py install my-skill.md
python universal-skill-converter.py check my-skill.md
python universal-skill-converter.py inspect my-skill.md
python universal-skill-converter.py list
```

### 📋 Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| `install <file>` | Install skill (auto-detect targets) | `install foo.md --to cursor,windsurf` |
| `inspect <file>` | View skill details | `inspect foo.md` |
| `check <file>` | Check compatibility & deps | `check foo.md --json` |
| `list` | List installed skills | `list --agent windsurf` |
| `convert <file> --to <fmt>` | Export to format (stdout) | `convert foo.md --to openclaw` |
| `install-dir <dir>` | Batch install directory | `install-dir ./skills/` |
| `sync --from <dir>` | Bidirectional sync | `sync --from ./skills/ --to all` |
| `watch <dir>` | Watch & auto-sync | `watch ./skills/ --to reasonix,cursor` |
| `config` | Config management | `config set default_targets cursor` |
| `--detect-agent` | Detect agent environment | `--detect-agent` |
| `--self-install` | Self-install as skill | `--self-install` |
| `--bootstrap` | ⭐ One-click bootstrap | `--bootstrap` |

**Common flags:** `--to <a,b>` targets / `--dry-run` preview / `--backup` backup / `--json` JSON output

### 🤖 Supported Agents (14)

`reasonix` · `hermes` · `opencode` · `claude-code` · `openai-codex` · `cursor` · `windsurf` · `cline` · `roo-code` · `github-copilot` · `continue` · `aider` · `skills-cli` · `openclaw`

### 💡 Use Cases

**Download a skill → install everywhere**
```bash
python universal-skill-converter.py install ~/Downloads/research-skill.md --to all
```

**Share Cursor rules with Cline & Windsurf**
```bash
python universal-skill-converter.py convert .cursor/rules/coding.mdc --to cline
```

**Sync your entire skill library**
```bash
python universal-skill-converter.py sync --from ./my-skills/ --to reasonix,cursor,openclaw
```

---

## ⚙️ Configuration

Config file: `~/.skill-converter/config.json`

```json
{
  "default_targets": ["reasonix"],
  "watch_dirs": [],
  "backup_enabled": true,
  "poll_interval": 2.0,
  "path_overrides": {}
}
```

```bash
python universal-skill-converter.py config show
python universal-skill-converter.py config set default_targets reasonix,cursor,windsurf
python universal-skill-converter.py config path reasonix D:/my-custom-path/skills
```

## 📦 Zero Dependencies

Single Python 3 file, no third-party libraries. The `watch` command optionally uses `watchdog` (falls back to polling).

## 🧪 Development

```bash
# Verify bracket balance
node -e "
const c = require('fs').readFileSync('universal-skill-converter.py','utf8');
let s = c.replace(/(['\"])(?:(?!\1|\\\\).|\\\\.)*\1/g,'').replace(/#.*$/gm,'');
console.log('{}:', (s.match(/\{/g)||[]).length - (s.match(/\}/g)||[]).length);
console.log('():', (s.match(/\(/g)||[]).length - (s.match(/\)/g)||[]).length);
"
```

## 📄 License

MIT
