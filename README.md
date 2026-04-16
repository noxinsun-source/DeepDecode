<div align="center">

# 🔍 DeepDecode · 深度解码

### *From paper claim to operator-level code — understand the why behind every line.*
### *从论文创新点到算子级代码，解码任务与代码之间的内在逻辑*

[![Claude Code](https://img.shields.io/badge/Claude%20Code-7%20Skills-blueviolet?logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Stars](https://img.shields.io/github/stars/noxinsun-source/DeepDecode?style=social)](https://github.com/noxinsun-source/DeepDecode)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

</div>

---

## What it does

DeepDecode is a **Claude Code skill suite** that bridges ML papers and their implementations.

Given a GitHub URL, it automatically:

1. **Finds the paper** — scans README, searches the web, or accepts your PDF
2. **Maps paper claims → code functions** — locates exactly which functions implement each contribution
3. **Explains every line** — generates operator-level task↔code tables: *what this expression does, why it's written this way, what breaks if you change it*

```
/full-analysis https://github.com/DEEP-PolyU/LinearRAG
```

```
✅ Step 0  LinearRAG — Nano tier (6 files / 1078 lines)
✅ Step 1  Architecture: 2 🔥 core files, 4 ⚙️ boilerplate
✅ Step 2  Data flow: 5 transformation hops
✅ Step 3  Paper found: LinearRAG ICLR'26 → 5 innovation functions located
❓ Step 4  Run L4 deep analysis on all 5 functions? [Y/n]
✅ Step 5  Report saved → 03.资料库/代码分析/LinearRAG/REPORT.md
```

---

## The 7 Skills

| Command | What it does |
|---------|-------------|
| `/full-analysis [url]` | ⭐ Full pipeline, one command. Auto-sizes, auto-finds paper, all phases. |
| `/inno-scan [url]` | Paper discovery + map contribution claims → functions (grep-based, token-efficient) |
| `/code-explain [url] --file f.py --func Foo` | Single-function deep dive: L3 flowchart + L4 line-by-line task↔code table |
| `/repo-map [url]` | File tree with 🔥 CORE / 📦 INFRA / ⚙️ BOILERPLATE labels |
| `/repo-callgraph [url]` | AST call graph + data contracts (dataclass, Pydantic, ABC) |
| `/data-flow [url]` | Data shape transformations from input to output |
| `/repo-compare [url1] [url2]` | Side-by-side comparison of two repos solving the same problem |

---

## Installation

**Into an Obsidian vault** (recommended):
```bash
git clone https://github.com/noxinsun-source/DeepDecode \
  "/path/to/vault/.claude/skills/DeepDecode"
bash "/path/to/vault/.claude/skills/DeepDecode/install.sh" \
  "/path/to/vault/.claude/skills/"
```

**Standalone Claude Code**:
```bash
git clone https://github.com/noxinsun-source/DeepDecode ~/.claude/skills/DeepDecode
bash ~/.claude/skills/DeepDecode/install.sh ~/.claude/skills/
```

Open Claude Code and type `/full-analysis` — if it autocompletes, you're ready.

---

## Usage

```bash
# Simplest: just give the GitHub URL
/full-analysis https://github.com/user/repo

# Quick mode (architecture + innovation map, skip deep dive)
/full-analysis https://github.com/user/repo --mode quick

# Deep mode (full L4 line-by-line analysis on all core functions)
/full-analysis https://github.com/user/repo --mode deep

# Already have the paper PDF?
/full-analysis https://github.com/user/repo --paper /path/to/paper.pdf

# Point at one specific function you want to understand
/code-explain https://github.com/user/repo --file src/model.py --func train_step

# Resume an interrupted session
/full-analysis https://github.com/user/repo --resume
```

Works on any repo size. Repos with 500k+ lines of code are handled by switching to grep-only mode — the paper-guided innovation scan stays token-efficient at any scale.

---

## Example output

See [`examples/linearrag-full-analysis.md`](examples/linearrag-full-analysis.md) — a complete analysis of [LinearRAG (ICLR 2026)](https://arxiv.org/abs/2510.10114), including:
- Paper claim → function mapping table (5 innovations)
- L3 algorithm flowcharts for each core function
- L4 line-by-line task↔code tables with paper citations

---

## Platforms

Works in any environment where Claude Code runs:

| Platform | How to use |
|----------|-----------|
| **Claude Code CLI** | `cd your-vault && claude`, then type commands |
| **VS Code + Claude Code extension** | Type commands in the sidebar panel |
| **Obsidian + Claudian plugin** | Type commands in the right-side panel |

Results are saved as Markdown in your vault — Mermaid diagrams render natively in Obsidian.
