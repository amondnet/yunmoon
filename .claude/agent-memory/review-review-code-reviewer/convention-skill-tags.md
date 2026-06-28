---
name: convention-skill-tags
description: yoonmoon SKILL.md files use role/workflow/phase/resources/outputFormat XML-ish tags but never an <output> wrapper tag
metadata:
  type: project
---

In yoonmoon `SKILL.md` files, the body uses pseudo-XML section tags like `<role>`, `<resources>`, `<workflow>`, `<phase n=...>`, `<outputFormat>`, `<preservationRules>`, `<followupCommands>`, `<outOfScope>`.

None of the 5 original skills (humanize, detect, proofread, restyle, translate-polish) use an `<output>...</output>` wrapper tag.

**Why:** During PR #2 review a finding claimed `skills/polish-all/SKILL.md` ended with a stray `</output>` (line 107) and `references/pipeline-guide.md` with `</output>` (line 91). That finding was a FALSE POSITIVE — verified against the actual files: SKILL.md ends at line 106 with `</outOfScope>`, pipeline-guide.md has 90 lines, and grep finds zero `<output>` tags. The reviewer had misattributed its own result-wrapper markup as file content (evidence-misattribution failure class). The general convention below still holds; the specific PR #2 example did not occur.

**How to apply:** The house convention (no `<output>` wrapper tag) is real and useful. But before flagging an unbalanced tag, OPEN the cited file/line and confirm the markup actually exists there — do not trust a finding that may have captured wrapper markup. Unmatched tags are a real defect only when present in the file.
