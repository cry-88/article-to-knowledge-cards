# 贡献指南 / Contributing

感谢你考虑为 `make-knowledge-cards` 做贡献！本仓库是一个开源 Agent Skill，欢迎反馈问题、改进文档或完善 Skill 指令。

## 仓库结构

- `skills/make-knowledge-cards/SKILL.md` — Skill 核心指令（**主要维护对象**）
- `skills/make-knowledge-cards/agents/openai.yaml` — OpenAI Agents / Codex 界面元数据
- `tools/quick_validate.py` — 内置校验脚本（与官方 `skill-creator` 一致，仅标准库）
- `.github/workflows/validate.yml` — CI，push / PR / 打 tag 时自动校验 Skill
- `examples/` — 不同输入类型的样例（输入 + 输出）
- `README.md`、`CHANGELOG.md`、`LICENSE`（MIT）

## 本地开发

1. Fork 并克隆本仓库。
2. （可选）本地校验 Skill 结构：
   ```bash
   python tools/quick_validate.py skills/make-knowledge-cards
   ```
   输出 `Skill is valid!` 即通过。CI 会自动在每次提交时跑同样的检查。

## 如何贡献

- **提 Issue**：发现 Bug、措辞歧义或希望新增能力，请先开 Issue 描述场景与期望。
- **提 PR**：
  1. 从 `main` 切出特性分支（如 `fix/xxx` 或 `feat/xxx`）；
  2. 修改相关文件（通常是 `SKILL.md` 或文档）；
  3. 若是行为改动，请在 `examples/` 补充或更新对应样例；
  4. 确保 `tools/quick_validate.py` 通过；
  5. 在 `CHANGELOG.md` 的 `[Unreleased]` 或对应版本中记录改动；
  6. 提交 PR 到 `main`。

## 改动 Skill 指令时的原则

- 保持**纯指令驱动**：除非必要，不要引入脚本依赖。
- 任何输出规则（提取重点、一卡一点、去重、不编造、不硬凑）都要在 `SKILL.md` 中明示，并用 `examples/` 佐证。
- 修改后请在 `README.md` / `CHANGELOG.md` 同步说明，保持文档与真实功能一致。

## 行为边界（请勿在 PR 中加入）

以下能力当前**明确不支持**，新增前请先在 Issue 中讨论：网页抓取、PDF 解析、Anki 导出、图形界面。

## 许可

本仓库以 MIT 许可证开源。提交贡献即表示你同意以相同许可证发布你的改动。
