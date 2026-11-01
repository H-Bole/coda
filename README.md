# Coda／尾声

两个独立的纯指令技能，用于在用户明确调用时收尾。技能源码为英文，执行时使用用户的语言回复。不需要脚本、运行时依赖或网络服务。

[English](README.en.md) · [术语表](GLOSSARY.md) · [MIT 许可证](LICENSE)

## 选择范围

| 技能 | 范围 | 历史遗留 |
| --- | --- | --- |
| [`coda`](skills/coda) | 本轮任务的文件、临时产物与进程 | 保留，不扩大清理范围 |
| [`coda-workspace`](skills/coda-workspace) | 工作区收尾，包括历史清理候选的检查 | 先列具体清单，逐项获得用户批准；执行前复核，状态变化则跳过 |

两者各自包含完整的 `SKILL.md` 和 `agents/openai.yaml`，可以单独安装。不因任务完成自动触发，也不要求每轮生成总结文件。

## 安装与调用

使用 Magpie 自行安装：

1. 获取[仓库](https://github.com/H-Bole/coda)，按 Magpie 实际支持的导入方式操作。
2. 分别选择两个技能目录导入：[skills/coda](https://github.com/H-Bole/coda/tree/main/skills/coda) 和 [skills/coda-workspace](https://github.com/H-Bole/coda/tree/main/skills/coda-workspace)。仓库根目录不是单个技能目录；不要假定 Magpie 会自动识别并安装两者。
3. 刷新宿主或开启新会话，确认 `coda` 和 `coda-workspace` 两个入口各出现一次。
4. 卸载通过 Magpie 管理，不要直接删除可能被其他安装共用的源目录。

本项目不创建 Junction，也不改写已有宿主配置。不依赖特定 Magpie 菜单名称。

### Codex

- 在技能选择器中选择，或明确输入 `$coda` / `$coda-workspace`。
- 支持 `/skills` 的 CLI、IDE 宿主也可通过该入口选择；不保证 `/coda` 是 Codex 的斜杠命令。
- 两个技能的 `agents/openai.yaml` 均声明 `policy.allow_implicit_invocation: false`，仅在用户明确调用时使用。

### Claude Code

- 调用 `/coda` 或 `/coda-workspace`。
- 两个技能使用通用标准 frontmatter；仅靠技能正文不足以在宿主层禁止隐式调用。安装时需在 Claude Code 的宿主设置中配置：

```json
{
  "skillOverrides": {
    "coda": "user-invocable-only",
    "coda-workspace": "user-invocable-only"
  }
}
```

请按已有设置结构合并，不要覆盖整份配置。该设置适用于个人或项目目录技能，不适用于插件提供的技能。该设置由用户或安装管理器处理，本项目不代为修改。

调用方式参照 [Codex 技能文档](https://learn.chatgpt.com/docs/build-skills)与 [Claude Code 技能文档](https://code.claude.com/docs/en/skills)。

## 收尾边界

- 先读项目规则，核对文件与进程的归属、引用和占用。本轮仅可删除确认已废弃且归属明确的产物。
- 不凭名称、时间戳或 Git 状态判断可删。原件、正式成果、依赖、共享资源、归属未知或仍在使用的内容保留。
- 工作区历史候选先列出具体路径或进程及理由，逐项获得批准。执行前重新核对；内容、引用、占用或进程身份变化时跳过并报告。
- 移动文件前检查引用。已有合理存放位置的内容不迁移，避免为整理而改目录。
- 进程须结合启动时间、命令行和任务关联判断，不能仅凭 PID、端口或名称关闭。非任务进程、常驻服务及共享进程保留。
- Windows 删除优先使用精确绝对路径的 `Remove-Item -LiteralPath`，不默认添加 `-Force` 或 `-Recurse`。删除目录前检查路径与剩余内容；核对 Junction 或符号链接的类型和目标，只删除链接本身，不进入目标。
- 操作失败或被策略阻止时，不换工具绕过；报告具体残留与限制。仅有 `blocked by policy` 时，不推断存在自动审批拒绝。
- 不默认提交或推送、清缓存、安装依赖、修改业务代码或运行大范围测试。

完成后简短说明整理、删除和关闭了什么，保留了什么，以及未验证或未完成的事项。空间统计区分文件逻辑大小与实际测得的磁盘空间变化；无法实测时不声称已释放多少空间。

## 验证状态

验证范围为格式检查和隔离行为场景。Magpie 本机安装、刷新及两个入口的实际调用仍待验收；Claude Code 尚未实机验证。宿主入口可见不等于安全边界已通过验证。
