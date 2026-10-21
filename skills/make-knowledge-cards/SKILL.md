---
name: make-knowledge-cards
description: Convert a pasted article or a local Markdown/TXT file into 5–8 concise knowledge cards, each capturing one key point with a title, core knowledge, brief explanation, and an example or self-test question. Use when a user wants to study, review, or distill an article, blog post, note, or .md/.txt document into spaced, memory-friendly cards. Does NOT support web page scraping, PDF files, Anki export, or a graphical interface.
---

# Make Knowledge Cards

## Overview

Turn any plain-text source (pasted article or local Markdown/TXT file) into a set of knowledge cards optimized for review and recall. Each card isolates a single, genuinely important idea and presents it with a title, the core knowledge as one sentence, a short explanation, and either a concrete example or a self-test question.

## When to Use

Use this skill when the user:
- Pastes an article, blog post, essay, or note and asks to "make cards", "turn this into flashcards", "summarize as study cards", "distill into key points", or similar.
- Provides a path to a local `.md` or `.txt` file and wants it converted into cards.
- Wants to review or memorize the essential ideas of a document without re-reading it.

Do not use this skill for other summarization formats (e.g., a prose summary, mind map, or outline) unless the user explicitly wants cards.

## Inputs

Accept the source in one of two forms:

1. **Inline text** — the user pastes the article directly in the conversation. Use it as-is.
2. **Local file path** — the user points to a `.md` or `.txt` file. Read the file with the Read tool before processing.

If the user supplies only a filename without a path, ask for the full path or the text itself. Never invent or assume file contents.

## Workflow

1. **Read the source.** For inline text, work from the pasted content. For a file, read it fully before summarizing.
2. **Identify the load-bearing ideas.** Determine which points are genuinely important — the concepts, facts, definitions, principles, or decisions a reader must understand. Ignore filler, repetition, anecdotes, and meta commentary unless they carry the core message.
3. **Deduplicate.** Merge overlapping or restated ideas into a single card. Do not create two cards for the same point phrased differently.
4. **Draft one card per idea.** Write each card around exactly one knowledge point. If a point has a major sub-point that stands alone, it may become its own card; otherwise keep it inside the parent card's explanation.
5. **Choose the fourth element.** For each card, include either a concrete **example** drawn from the source or a **self-test question** that checks understanding. Prefer the example when the source provides one; otherwise use the self-test question.
6. **Count honestly.** Produce 5–8 cards when the source supports that many distinct points. If the source yields fewer than 5 distinct, important ideas, produce only as many as exist (3, 2, or even 1). When producing fewer than 5 cards, append a one-line note in the source language stating how many distinct points the source actually supported — for example, "原文仅包含 N 个明确知识点，故生成 N 张卡片，未强行凑数" — so the user knows the shorter output is intentional, not an error. Never pad with trivial, redundant, or fabricated cards to reach a quota.
7. **Output the cards** in the format below, in the same language as the source.

## Card Format

Render the cards as a Markdown list. Use this exact structure for every card:

```
## 卡片 N：<标题>
**核心知识**：<用一句话概括该知识点>
**简明解释**：<2–4 句话，用读者能懂的语言解释，不堆砌术语>
**例子 / 自测**：<来自原文的具体例子，或一道检查理解的自测题>
```

English-source variant (keep the field labels meaningful in the source language):

```
## Card N: <Title>
**Core knowledge**: <one-sentence summary of the point>
**Brief explanation**: <2–4 sentences in plain language>
**Example / Self-test**: <a concrete example from the source, or a question that checks understanding>
```

Field constraints for every card:
- **标题 (Title):** names the single idea; specific, not generic (e.g., "TCP 三次握手", not "网络通信").
- **核心知识 (Core knowledge):** one declarative sentence capturing the essence.
- **简明解释 (Brief explanation):** 2–4 sentences; define terms on first use; avoid repeating the title verbatim.
- **例子 / 自测 (Example / Self-test):** must be grounded in the source. If using an example, take it from the text or clearly derive it from stated concepts. If using a self-test question, it must be answerable from the card's own content.

## Quality Rules

- **Extract what matters.** Prioritize concepts, definitions, principles, causes, and decisions over trivia, examples-as-filler, or stylistic flourishes.
- **One point per card.** A card that tries to teach two unrelated ideas should be split.
- **No duplication.** Collapse restated ideas into one card.
- **No fabrication.** Every claim must trace to the source. Do not add facts, statistics, names, dates, or examples that are not present. If a card needs an example and the source lacks one, use a self-test question instead of inventing an example.
- **No forced quantity.** The 5–8 range is a target, not a requirement. When the source is thin, output fewer cards and say so.
- **Preserve meaning.** Paraphrase freely for clarity, but never change what the source claims.

## Unsupported Features

This skill intentionally does **not** support:
- **Web page scraping** — provide the article text or a local file; do not fetch URLs.
- **PDF files** — extract the text to `.md`/`.txt` first, then submit it.
- **Anki or other spaced-repetition export** — output is plain Markdown cards, not `.apkg`/`.csv` import files.
- **A graphical user interface** — interaction is through conversation and text files only.

If the user requests any of these, decline politely and suggest the supported path (e.g., "请将 PDF 文本复制出来，或先转为 .md/.txt 再交给我").

## Output Example

Input (pasted, partial):
> 缓存用于加速数据访问。最常见的两种是本地缓存和分布式缓存。本地缓存速度快但容量有限；分布式缓存可横向扩展，但存在一致性问题……

Output:
```
## 卡片 1：缓存的作用
**核心知识**：缓存通过暂存高频访问的数据来加速读取、降低后端压力。
**简明解释**：当相同数据被反复请求时，直接从更快的存储层返回结果，可显著减少数据库或远程调用的开销。
**例子 / 自测**：什么场景下引入缓存收益最大？回想你见过的"热点数据反复查询"的例子。

## 卡片 2：本地缓存 vs 分布式缓存
**核心知识**：本地缓存低延迟但容量受限，分布式缓存可扩展但带来一致性挑战。
**简明解释**：本地缓存驻留在进程内，访问最快却有内存上限；分布式缓存跨节点共享、可水平扩容，但多副本间的数据同步会产生一致性问题。
**例子 / 自测**：若某数据要求强一致，你会优先选哪种缓存？为什么？
```

When the source supports 5–8 points, continue numbering; when it supports fewer, stop and note the count.
