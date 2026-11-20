# .agents

个人 AI 配置仓库：保存自己的 skills、全局规则和专长 agent 文档。

## 目录

```text
.agents/
├── AGENTS.md          # 全局规则的源文件，目前是占位内容
├── agents/            # 专长 agent 文档；template.md 暂不启用
└── skills/            # 自有 skills 和已有辅助文件
```

本地可以同时安装外来或插件附带的 skills，但它们不纳入这个仓库。
本仓库没有新增安装脚本，不创建软链接，也不修改工具配置。

## 首次使用

在自己的**用户主目录**打开终端，执行：

```bash
git clone https://github.com/OneOfLzx/.agents.git
```

Git 使用仓库名作为目录名，因此得到 `~/.agents/`，无需指定目标目录或再搬动文件。
仓库根目录已经直接包含 `skills/`，不要再套一层 `.agents/`。

如果终端不在用户主目录，先执行 `cd ~`。如果已有非空的 `~/.agents`（例如工具已安装了 skills），
不要删除或覆盖它：普通 clone 无法写入非空目录，需要单独合并现有内容。

## Codex 加载范围

| 内容 | 当前效果 |
| --- | --- |
| `~/.agents/skills/<name>/SKILL.md` | Codex 的个人 skill 搜索位置；新安装或更新后可开新会话检查加载情况 |
| `~/.agents/AGENTS.md` | 保存全局规则源文件；仅放在这里不会自动成为 Codex 的全局规则 |
| `~/.agents/agents/*.md` | 保存专长 agent 文档，不自动注册或启用 |

Codex 的默认全局规则位置是 `~/.codex/AGENTS.md`。
当前官方文档中的个人专长 agent 使用 `~/.codex/agents/*.toml`，不是任意 Markdown 文件。
此仓库暂不做这些加载适配。项目目录里的 `AGENTS.md` 也可能按目录作用域被读取，
但那不等于在所有项目中全局生效。其他 harness 的加载约定需要分别核对。

官方参考：[AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)、
[Skills](https://learn.chatgpt.com/docs/build-skills)、
[Subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents)。

## 只提交自己的 skills

根目录 `.gitignore` 对 `skills/` 使用白名单：默认忽略其直接子项，
只放行明确列出的自有目录与已有辅助文件。迁移时以原仓库已经跟踪的内容为初始白名单。

新增自己的 skill 时：

1. 创建 `skills/<name>/SKILL.md` 及所需资源。
2. 在根目录 `.gitignore` 的白名单追加 `!/skills/<name>/`。
3. 用 `git status --short` 和 `git diff --cached` 检查要提交的内容。

外来 skills 留在本机，不加入白名单；安装记录 `.skill-lock.json` 也被忽略。
Git 忽略只控制提交范围，不影响工具加载。白名单目录内的资源可以被跟踪，
因此在提交前仍需检查差异；不要用 `git add -f` 绕过白名单导入外来内容。
`.gitignore` 不会自动移除已经跟踪的文件。

`skills/.gitignore` 和 `skills/manage_skills_soft_link.py` 是原仓库已有文件，本次仅保留。
没有执行该软链接脚本，也没有新建或修改软链接。

## 更新

在本仓库内执行 `git pull --ff-only`。新增或更新内容后开新会话检查工具加载情况。

## Git 历史

本仓库保留原 skills 仓库的历史，通过一次普通提交把原文件路径调整到 `skills/` 下，
并新增规则文档与白名单。未重写历史；本地安装的外来内容未上传。
