# search-planner

研究搜索 skill：给 agent 的"查资料 → 找信源 → 归纳成带引用结论"流程。

## 它做什么

- **触发边界**：只有"大概目标、需要搜索"的任务才用；已知具体网址时直接用 WebFetch，不走本 skill
- **默认管线**（四角色，模型只是当前示例映射，可替换）：
  1. **拆分**：大范围目标拆成多个中范围子问题（示例：DeepSeek 网页版，或 Kimi）
  2. **搜索**：每个子问题带引用检索（示例：秘塔 AI 搜索，中范围及以下最合适；深度搜索免费限次）
  3. **总结**：整理成 agent 好取用的中间产物，推荐目录式（先总结全部搜索内容，再给完整内容目录）（示例：ChatGPT，连接不稳时 Kimi 是主场景）
  4. **成稿**：agent 按索引组合结论、标注来源（材料少时 agent 自己归纳，跳过中间环节）
- **所有规则都是推荐基线**：具体跳不跳、走哪条路，由 agent 按材料量、任务性质、用户 token 余量等具体情况判断
- **补充路**：必应（盲搜）、百度（明确指定的资源，不能盲搜）

## 安装

本仓库布局即 skill 目录布局（`SKILL.md` 在根目录），**clone 到 skills 目录下的 `search-planner/` 文件夹**即可（目录名须与 SKILL.md 里的 `name` 一致）：

| 工具 | 装到哪 |
|---|---|
| ZCode（全局） | `~/.agents/skills/search-planner/` |
| ZCode（项目级） | `<project>/.agents/skills/search-planner/` |
| Claude Code（全局） | `~/.claude/skills/search-planner/` |
| Claude Code（项目级） | `<project>/.claude/skills/search-planner/` |

```bash
# 通用：任意支持 .agents/skills 的 agent 工具（macOS / Linux）
git clone https://github.com/xlb276/search-planner-skill ~/.agents/skills/search-planner
```

不认识的 agent 工具：找它的 skill/指令目录（多数认 `.agents/skills/`），放不进去时按 SKILL.md 里"通用性说明"一节处理。

## 目录

```
search-planner/                ← clone 目标目录
├── SKILL.md                   # 触发条件 + 管线 + 平替/跳过规则 + 输出要求
└── references/
    └── tools-comparison.md    # 各工具（网页端）优缺点、额度、快照说明
```

> `references` 里的工具清单是 2026-10 快照；新模型/新工具出现时按 SKILL.md"模型可替换"一节的角色特征判断能不能顶进对应环节，不必改本仓库（或者顺手提个 PR 更新 references）。

## 许可

未附 LICENSE。如需复用请自行协商；欢迎 PR。
