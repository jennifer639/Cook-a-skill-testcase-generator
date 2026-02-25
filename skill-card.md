# 🧪 Skill Card — SmartQC Test Case Generator

| Field | Details |
|---|---|
| **Skill Name** | SmartQC — Test Case Generator |
| **What Gets Automated** | The entire test case writing process from a spec file: feature analysis, main flow & business rule identification, generation of happy path / edge case / negative case / security case — plus a ready-to-use report template so QC only needs to fill in pass/fail |
| **BEFORE: Manual Work** | Read spec → think through each case manually → type into Google Sheet. Takes **3–6 hours** per complex module. Easy to miss edge & negative cases, inconsistent format across team members, depends on individual experience, no standard report template |
| **AFTER: With Skill** | Upload `.md` spec → AI analyzes → generates test cases + report template → QC reviews & supplements. Takes only **10–15 minutes** per module. Wider coverage, 100% consistent format, usable by anyone regardless of experience level, report template included |
| **Tools / AI Used** | **Claude** (Anthropic) — build skill, write instructions, test & iterate <br> **Claude Project** — deploy and run the skill <br> **ChatGPT Codex** (OpenAI) — refine instructions, generate sample test case examples |
| **Limitations** | Output quality depends on the level of detail in the input spec — vague spec leads to incomplete test cases <br> No direct integration with test management tools (TestRail, Jira Xray…) for auto-import <br> Does not yet cover performance testing & load testing <br> QC review is still required — AI may miss domain-specific business context |
| **Roadmap** | **Phase 2:** Direct import to Jira / TestRail — no more manual copy-paste <br> **Phase 3:** Accept bug history as additional input → prioritize test cases for high-risk areas <br> **Phase 4:** Auto-generate test data suited to each environment (staging / production) <br> **Phase 5:** Multi-spec support — process multiple modules at once, detect cross-module dependencies |
