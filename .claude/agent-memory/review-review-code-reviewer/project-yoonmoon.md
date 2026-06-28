---
name: project-yoonmoon
description: The yoonmoon repo is a Korean writing-polish Claude Code skill marketplace; reviews are content/structure checks on markdown skills + JSON manifests, not app code
metadata:
  type: project
---

The repo at /Volumes/Dev/IdeaProjects/yunmun is the `yoonmoon` plugin/marketplace (GitHub amondnet/yoonmoon).

It ships 6 skills under `skills/`: detect, humanize, proofread, restyle, translate-polish, polish-all (orchestrator added in PR #2). Each skill is a `SKILL.md` (YAML frontmatter + markdown body) plus `references/*.md`. Manifests: `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`.

**Why:** No application source code — review criteria are JSON validity, YAML frontmatter validity, skill-name uniqueness (dir must equal frontmatter `name`), engineering standards (file <=500 LOC, DRY), and logical coherence of the skill prose.

**How to apply:** When reviewing this repo, validate JSON with a parser, confirm `name:` matches the directory, check LOC counts, and read reference-path links to confirm targets exist. The shared AI-tell taxonomy in `humanize/references/ai-tell-taxonomy.md` has 10 categories; cats 1 (번역투), 2 (피동·사동), 6 (형식명사·명사화) overlap with translationese handled by translate-polish.
