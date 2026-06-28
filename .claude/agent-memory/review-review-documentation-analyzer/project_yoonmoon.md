---
name: project_yoonmoon
description: yoonmoon plugin structure — 6 Korean text-polishing skills (5 leaf + 1 orchestrator polish-all), file layout, translationese-research.md location
metadata:
  type: project
---

yoonmoon is a Claude Code plugin for Korean text polishing with 6 skills: humanize, detect, translate-polish, proofread, restyle, and polish-all (orchestrator added in PR #2).

**Why:** PR #1 added translate-polish, proofread, restyle and moved translationese-research.md from skills/humanize/references/ to skills/translate-polish/references/. PR #2 added polish-all orchestrator skill that chains all 5 leaf skills in sequence (detect→proofread→translate-polish→humanize→restyle→detect QA).

**How to apply:** When reviewing PRs:

- translationese-research.md lives at skills/translate-polish/references/ (not humanize)
- polish-all references sibling skills by `plugin:skill` name (e.g. `yoonmoon:detect`), NOT by relative file path. Changed during PR #2 review (maintainer direction): an orchestrator must not couple to siblings' internal file layout, so it invokes them via the `Skill` tool. Flag any reintroduced `../`/`../../` cross-skill file path in polish-all as a regression.
- README intro says "다섯 스킬과, 이를 전과정으로 묶는 풀코스 스킬을 제공한다" (5+1=6, consistent with "여섯 스킬 모두" in usage section)
- The PR #1 stale "두 스킬" issue on old README:41 is now replaced by "여섯 스킬 모두" in PR #2
- SKILL.md phases 0-7 map to pipeline-guide.md phases 1-6 (pipeline-guide omits phase 0=input-parse and phase 7=output, which are not skill-specific)
- dedup rule: translate-polish handles AI-tell categories 1·2·6; humanize handles 3·4·5·7·8·9·10 — consistent between SKILL.md and pipeline-guide.md
