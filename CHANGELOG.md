# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-10-21

### Added
- `make-knowledge-cards` Skill: convert pasted articles or local `.md` / `.txt` files into 5–8 knowledge cards.
- Each card has a fixed four-part structure: title / core knowledge / explanation / example-or-quiz.
- One card per point, automatic deduplication, no fabrication; when the source yields fewer than 5 distinct points, produce only as many as exist and say so (never pad).
- Language follows the source text (Chinese article → Chinese cards, English article → English cards).
- `agents/openai.yaml` interface manifest for OpenAI Agents / Codex.
- `README.md`, `LICENSE` (MIT), and `examples/` samples (technical long-form / short note / repetitive text).
- CI workflow (`.github/workflows/validate.yml`) that runs the vendored `tools/quick_validate.py` on push, pull request, and tag.
