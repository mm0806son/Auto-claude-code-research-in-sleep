# ARIS · cn-overlay 中文工作流分支

本分支（`cn-overlay`）是 [wanshuiyin/Auto-claude-code-research-in-sleep](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) 的中文化覆盖层，由 [@mm0806son](https://github.com/mm0806son) 维护。

> 仅 `cn-overlay` 分支可见；`main` 分支永远只跟 `upstream/main` 同步。

## 设计原则

Agent ↔ User 对话用中文，学术写作产物（`.tex` / `.bib` / 代码）保留英文。

上游 `skills/shared-references/output-language.md` 已定义完整 per-skill 语言策略，cn-overlay 只补一个上游遗漏：让 `/research-review` 也按这套策略走（其余 skill 上游已自行接入）。

## 安装到新项目

```bash
git clone https://github.com/mm0806son/Auto-claude-code-research-in-sleep.git \
  ~/Auto-claude-code-research-in-sleep
cd ~/Auto-claude-code-research-in-sleep
git checkout cn-overlay

bash tools/install_aris.sh /path/to/your/project
claude mcp add codex -s user -- codex mcp-server
```

新项目的 `CLAUDE.md` 加上以下任一即可触发中文输出：

```markdown
## Pipeline Status
language: zh
```

或直接用中文跟 agent 对话——上游 `output-language.md` 自动检测。

## 从上游 sync 红利

```bash
cd ~/Auto-claude-code-research-in-sleep
git fetch upstream

git checkout main
git merge --ff-only upstream/main
git push origin main

git checkout cn-overlay
git rebase upstream/main
git push --force-with-lease origin cn-overlay
```

skill 是软链——sync 后所有项目自动用上新版本，无需重装。

## 当前 cn-overlay 上的覆盖项

| 路径 | 类型 | 说明 |
|---|---|---|
| `skills/research-review/SKILL.md` | 补丁 | 加 `## Output Protocols` 引用 `output-language.md`（上游遗漏） |
| `README_CN_OVERLAY.md` | 新增 | 本文件 |

## 冲突解决

`git rebase upstream/main` 时如果 `skills/research-review/SKILL.md` 冲突，通常是上游自己补上了同一条引用——比对一下二选一保留即可。

## 维护者

- **Fork**: [@mm0806son](https://github.com/mm0806son)
- **Upstream**: [@wanshuiyin](https://github.com/wanshuiyin)

License 继承上游。
