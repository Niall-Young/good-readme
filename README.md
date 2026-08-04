# 双语 README 守门员 / Bilingual README Guardian

一个面向 Codex 当前打开项目的可复用 Skill：在每轮项目变更完成后判断 README 是否受影响，并在需要时创建或同步维护中英文内容。

A reusable Skill for the project currently open in Codex: after each implementation turn, it decides whether the README is affected and creates or synchronizes its Chinese and English content when needed.

[中文](#中文) | [English](#english)

---

<a id="中文"></a>
## 中文

### 项目简介

本项目用于设计和梳理 `maintain-bilingual-readme` Skill。Skill 安装在 `~/.codex/skills/maintain-bilingual-readme`，可服务于以后在 Codex 左侧打开的不同项目。

### 核心能力

- 将 Codex 当前工作区视为项目边界，不把父级 Git 仓库误当成目标项目。
- 在每轮实际变更后收集 diff、README、清单文件、配置和公共接口等证据。
- 根据用户可见行为、安装运行方式、依赖配置、API、CLI、目录结构和限制是否变化，决定创建、更新或保留 README。
- 使用同一份 `README.md` 和页内锚点提供中文 / English 切换。
- 强制两种语言在命令、链接、版本、警告和功能状态上保持一致。
- 在交付前校验内容依据、语言对齐、链接、路径、命令和最终 diff。

### 快速开始

在 Codex 中显式调用：

```text
$maintain-bilingual-readme 检查本轮变更，并同步维护当前项目的双语 README。
```

Skill 的描述也覆盖常见实现任务，可被 Codex 隐式选用。它不是独立运行的后台 Hook；门禁由 Codex 在一次实现任务结束前执行。

### 使用方法

典型结果只有三种：

- `README: created`：项目缺少 `README.md`，基于仓库证据创建双语文档。
- `README: updated`：变更影响用户或贡献者，需要同步更新中英文对应内容。
- `README: unchanged`：变更不影响文档事实，并给出简短依据。

### README 内容结构

默认结构按需裁剪，不保留空章节：

1. 项目简介
2. 核心能力
3. 快速开始
4. 使用方法
5. 配置（按需）
6. 项目结构（按需）
7. 开发与验证
8. API / CLI、部署、排障、贡献和许可证（按需）

### 开发与验证

```sh
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  ~/.codex/skills/maintain-bilingual-readme

~/.codex/skills/maintain-bilingual-readme/scripts/inspect_readme_context.py "$PWD"
```

[English](#english) · [返回顶部](#双语-readme-守门员--bilingual-readme-guardian)

---

<a id="english"></a>
## English

### Overview

This project designs and maps the `maintain-bilingual-readme` Skill. The Skill is installed at `~/.codex/skills/maintain-bilingual-readme` and can serve different projects opened from the Codex sidebar.

### Features

- Treat the current Codex workspace as the project boundary instead of accidentally targeting an ancestor Git repository.
- Gather evidence after each real change from the diff, README, manifests, configuration, and public interfaces.
- Decide whether to create, update, or preserve the README based on changes to visible behavior, setup, dependencies, configuration, APIs, CLIs, structure, or limitations.
- Provide a Chinese / English switch in one `README.md` using stable in-page anchors.
- Keep commands, links, versions, warnings, and feature status consistent across both languages.
- Verify evidence, language parity, links, paths, commands, and the final diff before handoff.

### Quick Start

Invoke it explicitly in Codex:

```text
$maintain-bilingual-readme assess this turn's changes and synchronize the current project's bilingual README.
```

Its description also covers common implementation tasks, so Codex may select it implicitly. It is not an independent background hook; Codex applies the gate before completing an implementation task.

### Usage

The gate produces exactly one of three outcomes:

- `README: created`: the project lacks `README.md`, so a bilingual document is created from repository evidence.
- `README: updated`: the change affects users or contributors, so the corresponding Chinese and English content is synchronized.
- `README: unchanged`: the change does not affect documented facts, with a concise reason provided.

### README Content Structure

The default structure is trimmed to the project and never retains empty sections:

1. Overview
2. Features
3. Quick Start
4. Usage
5. Configuration (when needed)
6. Project Structure (when needed)
7. Development and Verification
8. API / CLI, deployment, troubleshooting, contributing, and license (when needed)

### Development and Verification

```sh
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  ~/.codex/skills/maintain-bilingual-readme

~/.codex/skills/maintain-bilingual-readme/scripts/inspect_readme_context.py "$PWD"
```

[中文](#中文) · [Back to top](#双语-readme-守门员--bilingual-readme-guardian)
