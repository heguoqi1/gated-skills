# 三个独立技能

`ask-before-acting`、`explain-before-change`、`test-feature`。每个技能可单独拷到任何读取 `SKILL.md` 的宿主使用。

## 每个技能做什么

- **ask-before-acting**：请求含未消缺口时，一次问完再停；无缺口则复述后动手。
- **explain-before-change**：改源码前先写说明文档，等用户确认后再动。
- **test-feature**：按用户指定的功能点、通过标准、跑法跑测，出五项报告。

## 触发口令

| 技能 | 命中即加载的口令 |
|---|---|
| ask-before-acting | 「有什么不懂的先问我再执行」「先问再做」「先问再动」 |
| explain-before-change | 「先说明，不要改项目」「出说明文档，确认后再执行」「先出文档」 |
| test-feature | 「测这个功能」「按我的要求测」「按指定方式测」 |

## 怎么拷

把单个技能目录拷到目标宿主的项目级或用户级路径。项目级只对当前仓库生效，用户级对该机器上的该宿主全局生效。

| 宿主 | 项目级 | 用户级 |
|---|---|---|
| Cursor | `<项目>/.cursor/skills/<技能名>/` | `~/.cursor/skills/<技能名>/` |
| Claude Code | `<项目>/.claude/skills/<技能名>/` | `~/.claude/skills/<技能名>/` |
| Codex、Copilot CLI、Gemini CLI | 以该宿主文档为准 | `~/.agents/skills/<技能名>/` |

表里没有的宿主：把它读取 `SKILL.md` 的那个目录当目标路径，拷过去。
