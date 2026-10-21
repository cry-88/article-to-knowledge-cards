# 示例 / Examples

本目录提供 `make-knowledge-cards` 在**不同类型输入**下的样例，用于演示 Skill 的行为边界与输出质量。

每个示例由「输入文件」与「对应输出文件」组成（`output_cognitive_load.md` 例外：其原文为对话中直接粘贴，未单独留存输入文件）。

| 输入 | 输出 | 演示要点 |
|---|---|---|
| `input_technical.md` | `output_technical.md` | 技术长文 → 提炼出 8 张彼此独立、且均可在原文找到依据的卡片 |
| `input_short.txt` | `output_short.md` | 极短笔记 → 只生成 **1 张**卡片并附「未强行凑数」说明 |
| `input_repetitive.txt` | `output_repetitive.md` | 重复啰嗦文本 → **去重**为少量真实知识点 |
| （对话粘贴） | `output_cognitive_load.md` | 英文长文 → 8 张英文卡片，验证语言跟随原文 |

## 如何复现

把某个输入文件交给 Skill，例如：

> 把 `examples/input_technical.md` 做成知识卡片

或直接打开对应的 `output_*.md` 查看生成结果。

## 这些示例说明了什么

- **提取重点**：只保留真正重要的独立知识点，过滤重复与铺垫。
- **一卡一点**：每张卡片只讲一个知识点。
- **去重**：换说法重复出现的同一观点合并为一张。
- **不编造**：所有内容都可在原文中找到依据。
- **不硬凑**：原文知识点不足 5 个时，如实少生成并说明，绝不灌水。
