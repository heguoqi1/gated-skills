# 上传 `gated-skills` 到 GitHub

日期：2026-10-13

## 1. 需求复述

把 `D:\skill\gated-skills` 仓库内容推送到 `https://github.com/heguoqi1/gated-skills.git`。远程仓是空仓，本地不是 git 仓。认证用 HTTPS + Personal Access Token。`需求文档.md` 不进首次提交。

## 2. 要你拍板的点

### 2.1 仓库根 `README.md` 怎么办

GitHub 默认渲染仓库根的 `README.md`，目前只有 `skills/README.md`。三选一：

- a. 把 `skills/README.md` 提到仓库根（原位保留副本）。GitHub 首页即可看到总览。
- b. 仓库根另写一份新的 `README.md`，`skills/README.md` 留原位作单技能目录说明。略多一份但边界清晰。
- c. 不放 README，GitHub 靠仓库描述 + 文件列表。

### 2.2 PAT 怎么处理

推送时会触发用户名/PAT 提示。三选一：

- a. 我 push 时让你在终端临时粘贴 PAT，一次性用完即弃。
- b. 提前配 git credential helper（`git config --global credential.helper manager` 或 `store`），PAT 缓存后我直接 push。
- c. 我只准备 commit（`git init` + `add` + `commit`），remote + push 你自己跑。

### 2.3 `docs/` 子目录（含本设计文档）是否进库

- a. 进。`docs/specs/2026-10-13-github-publish-design.md` 与更早的 `docs/2026-10-13-ask-explain-test-design.md` 都公开。
- b. 只进 `skills/`，整 `docs/` 写进 `.gitignore`。

## 3. 打算改的文件

新增：
- `D:\skill\gated-skills\.gitignore`
- 视 2.1 选项，可能新增或移动 `D:\skill\gated-skills\README.md`
- 视 2.2 选项，可能需配置 `~/.gitconfig` 的 credential helper

新增文件的内容预览：

`.gitignore` 最小集（按 2.3 调整）：
```
# personal
需求文档.md

# OS
.DS_Store
Thumbs.db
desktop.ini

# editors
.vscode/
.idea/
*.swp
```

## 4. 不改的范围

- 不修改 `skills/`、`skills/README.md`、`skills/<名>/SKILL.md` 任何文件。
- 不动 `需求文档.md` 本身（只不追踪，不删除）。
- 不在 GitHub 网页端创建或修改任何设置（你已建好空仓；描述你也手设）。
- 不创建 `LICENSE`（你要加再说）。
- 不动 `D:\skill\` 下的其他目录（agent-skills、superpowers 等）。

## 5. 做法

步骤级（不贴大段命令实现，确认后写具体命令）：

1. 按 2.1 / 2.2 / 2.3 的回答，确定要新建或修改的文件清单。
2. 写 `.gitignore`（按 2.3 调整）。
3. 写或移动 `README.md`（按 2.1 调整）。
4. `git init -b main` 在 `D:\skill\gated-skills\`。
5. `git config user.name` / `user.email`（缺失时用本仓库局部配置，不动 `--global`）。
6. `git add .` —— `.gitignore` 应挡掉 `需求文档.md`。
7. `git status` 自查：要进库的文件是否齐全、不该进的都没进。
8. `git commit -m "..."`。
9. `git remote add origin https://github.com/heguoqi1/gated-skills.git`。
10. `git push -u origin main` —— 触发 PAT 提示，按 2.2 选择的方式处理。
11. 推送成功后输出去远程的 final commit hash。

## 6. 怎么验证

- 浏览器打开 `https://github.com/heguoqi1/gated-skills`：根目录应见 `skills/`、`.gitignore`、按 2.1 决定的 `README.md`。
- `需求文档.md` 不出现。
- 按 2.3 决定，决定 `docs/` 是否出现。
- 本地 `git log --oneline` 与 GitHub 上 `Insights → Commits` 第一条 commit 一致。
- 在仓库页面设描述为：`中文 AI 代理技能集。跨宿主通用（Cursor / Claude Code / Codex 等），遵循 SKILL.md 规范。`

## 7. 确认后才会做的事

按 2.1 / 2.2 / 2.3 你的回答执行：

- 写 `.gitignore`
- 写或移动 `README.md`
- `git init` / `add` / `commit`
- 配 remote
- push（按你定的 PAT 处理方式）
- 不做的事：不在网页端建仓、不设描述、不创建 LICENSE、不动其他目录
