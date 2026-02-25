# 📋 SKILL CARD — SmartQC Test Case Generator

| Section | Content |
|---|---|
| **Skill Name** | SmartQC Test Case Generator |
| **What's Automated** | Reading a feature spec (.md) → auto-generating a complete test suite: Happy Path, Edge Cases, Negative Cases, Security, API-specific, Cross-Platform, plus edge case analysis with ambiguity flags and a pre-filled test report template |
| **BEFORE: Manual** | QC Engineer reads spec → opens blank doc → writes test cases one by one → misses edge cases → writes report template from scratch after execution. **3–6 hours per module. 2–3 working days for a full feature.** |
| **AFTER: With Skill** | Upload or paste spec.md → skill auto-detects feature type, platforms, actors, business rules → outputs 28+ test cases across all categories + report template in a single response. **~2–5 minutes. Zero blank fields.** |
| **Tools / AI Used** | Claude (Anthropic) — prompt-based skill running a 5-step pipeline with 6 automated quality gates inside a Claude Project |
| **Limitations** | Does not auto-run tests · No direct Jira/TestRail push (v1.0) · No faker/data generator · No visual regression · Output quality depends on input spec quality |
| **Roadmap** | Auto-export to `.xlsx` (Jira-compatible) · Accept Figma + Postman collection as input · Jira API integration for auto ticket creation · AI browser agent to auto-execute test cases |
