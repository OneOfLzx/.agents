# .agents

我的全局 Agent 规则、专长 Agent 文档和自有 skills。

```text
AGENTS.md    全局规则，在这里编辑
agents/      专长 Agent 文档，暂不启用
skills/      自有 skills
```

## 首次使用（Codex，macOS / Linux）

**1. 在用户主目录下载仓库：**

```bash
cd ~
git clone https://github.com/OneOfLzx/.agents.git
```

如果已有非空的 `~/.agents`，先合并现有内容，不要删除或覆盖。

**2. 让 Codex 读取全局规则：**

```bash
mkdir -p ~/.codex
ln -s ~/.agents/AGENTS.md ~/.codex/AGENTS.md
```

软链接让两个路径指向同一份文件，以后只编辑仓库里的 `AGENTS.md`。
如果 `~/.codex/AGENTS.md` 已存在，先备份并按需合并原有规则；上面的命令不会覆盖已有文件。
如果设置过 `CODEX_HOME`，将目标目录 `~/.codex` 换成该目录。

**3. 开一个新的 Codex 会话。**

Codex 从 `~/.agents/skills/` 发现 skills，从链接读取全局规则。
`agents/` 下的 Markdown 仅用于保存专长文档，不会自动注册为 Codex Agent。
如有 `~/.codex/AGENTS.override.md`，它会优先于 `AGENTS.md`。

## 更新

在仓库里执行 `git pull --ff-only`，然后开新会话。软链接只需创建一次。

## 添加自己的 skill

1. 创建 `skills/<name>/SKILL.md` 和所需资源。
2. 在根目录 `.gitignore` 追加 `!/skills/<name>/`。
3. 检查改动，再提交。

外来或插件附带的 skills 不加入白名单：保留在本机，可以使用，但不上传。
