# 🧪 Skill Card — SmartQC Test Case Generator


---

## What Gets Automated
The entire test case writing process from spec: feature analysis, main flow identification, and generation of happy path / edge case / negative case / security case — plus a test report template so QC only needs to fill in pass/fail.

---

## BEFORE — Manual Work

| | |
|---|---|
| ⏱ Time | 3–6 hours per complex module |
| 🔄 Process | Read spec → think through each case manually → type into Google Sheet |
| ❌ Problems | Easy to miss edge & negative cases; inconsistent format across team members; depends on individual experience; no standard report template |

---

## AFTER — With Skill

| | |
|---|---|
| ⏱ Time | 10–15 minutes per module |
| 🔄 Process | Upload `.md` spec → AI analyzes → generates test cases + report template → QC reviews & supplements |
| ✅ Improvements | Wider coverage (happy path, edge, negative, security), consistent format, usable by anyone regardless of experience level, report template included |

---

## Tools / AI Used

- **Claude** (Anthropic) — build skill, write instruction, test & iterate
- **Claude Project** — deploy and run the skill
- **ChatGPT Codex** (OpenAI) — help refine instructions, generate sample test case examples

---

## Limitations

- Output quality depends on the level of detail in the input spec — vague spec leads to incomplete test cases
- No direct integration with test management tools (TestRail, Jira Xray…) for auto-import
- Does not yet cover performance testing & load testing scenarios
- QC review is still required — AI may miss domain-specific business context

---

## Roadmap

- **Phase 2:** Direct import to Jira / TestRail — no more manual copy-paste
- **Phase 3:** Accept bug history as additional input → prioritize test cases for high-risk areas
- **Phase 4:** Auto-generate test data suited to each environment (staging/prod)
- **Phase 5:** Multi-spec support — process multiple modules at once, detect cross-module dependencies
