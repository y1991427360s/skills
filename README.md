# 我的 Skills 备份

用于集中备份本机使用的 Agent Skills，方便换电脑、重装或找回。首次备份日期：2026-10-10。

| Skill | 用途 | 文件 |
| --- | --- | --- |
| neat-freak（收尾） | 阶段结束时整理项目文档、核对代码与文档、同步代理记忆 | [SKILL.md](skills/neat-freak/SKILL.md) |
| handoff-prompt（交接） | 为新会话生成可直接复制的上下文交接话术 | [SKILL.md](skills/handoff-prompt/SKILL.md) |

## 文件说明

- 保留本机当前启用版本的完整内容。
- neat-freak 的 references/ 参考文档一并备份。
- 不包含本机旧版 .bak 文件、账号配置、全局记忆或会话记录。
- 仓库保存的是手动备份；本地 skill 后续修改后需要再次提交推送。

## 找回与安装

登录自己的 GitHub 账号后，下载仓库 ZIP，或使用 GitHub CLI 克隆：

~~~powershell
gh repo clone y1991427360s/skills
~~~

将 skills/ 下所需的技能目录完整复制到对应工具的技能目录。复制 neat-freak 时必须包含 references/。

Codex 示例（在克隆后的仓库目录执行；如已有同名 skill，先备份）：

~~~powershell
$target = Join-Path $env:USERPROFILE '.codex\skills'
New-Item -ItemType Directory -Path $target -Force | Out-Null
Copy-Item -LiteralPath '.\skills\neat-freak' -Destination $target -Recurse
Copy-Item -LiteralPath '.\skills\handoff-prompt' -Destination $target -Recurse
~~~

Claude Code 可将目标目录改为 ~/.claude/skills/。复制后重新启动对应工具或开启新会话。

## 更新备份

将本机更新后的技能文件复制回本仓库对应目录，检查 diff 后提交并推送：

~~~powershell
git diff
git add skills
git commit -m "更新技能备份"
git push
~~~