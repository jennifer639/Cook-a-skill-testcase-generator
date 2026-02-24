# Cook-a-skill

> A curated collection of reusable AI skill definitions for Claude — structured, documented, and ready to plug in.

---

## What is a "Skill"?

A **skill** is a Markdown (`.md`) file that instructs Claude how to behave as a specialized expert for a specific task. Think of it as a detailed system prompt, packaged in a standardized format so it can be reused, versioned, and shared across projects.

Each skill defines:
- **What it does** — the scope and purpose
- **When to activate** — trigger conditions
- **How to behave** — step-by-step workflow, output format, quality rules
- **What not to do** — explicit anti-patterns

---

## Repository Structure

```
cook-a-skill/
├── README.md                  ← You are here
├── skills/
│   ├── smartqc/
│   │   └── smartqc-test-case-generator.md
│   ├── [your-next-skill]/
│   │   └── skill.md
│   └── ...
└── examples/
    ├── smartqc-sample-output.md
    └── ...
```

---

## Available Skills

| Skill | Description | Author | Version |
|---|---|---|---|
| [SmartQC — Test Case Generator](./skills/smartqc/smartqc-test-case-generator.md) | Generates structured test cases + report templates from a feature spec (Web / API / Mobile) | Jennifer | v1.0 |

---

## How to Use a Skill

### Option 1 — Paste into Claude's System Prompt
Copy the full content of the skill `.md` file and paste it as the system prompt before starting a conversation.

### Option 2 — Reference in Your Prompt
Attach the `.md` file to your conversation and tell Claude:
> "Follow the instructions in the skill file I've attached."

### Option 3 — Use with Claude API
```python
import anthropic

with open("skills/smartqc/smartqc-test-case-generator.md", "r") as f:
    skill_prompt = f.read()

client = anthropic.Anthropic()
message = client.messages.create(
    model="claude-opus-4-6",
    max_tokens=4096,
    system=skill_prompt,
    messages=[
        {"role": "user", "content": "Generate test cases for: [paste your spec here]"}
    ]
)
print(message.content[0].text)
```

---

## Skill File Format

Every skill in this repo follows this standard header:

```yaml
---
name: skill-name
description: >
  One-paragraph description of what this skill does and when to use it.
author: Your Name
---
```

Followed by structured Markdown sections:
- `## WHAT THIS SKILL DOES`
- `## TRIGGER CONDITIONS`
- `## INPUT`
- `## WORKFLOW` (step-by-step)
- `## OUTPUT QUALITY CHECKLIST`
- `## WHAT NOT TO DO`

---

## Skill Design Principles

These principles guide every skill in this collection:

1. **Start immediately** — Skills should not ask excessive clarifying questions before producing output. Auto-detect from context; flag ambiguities inline.
2. **Concrete over vague** — Test data, expected results, and examples must always use real values, never placeholders like "valid email."
3. **Graceful degradation** — Skills should handle interruptions cleanly (e.g., token cutoffs) and tell the user how to resume.
4. **Security by default** — Sensitive data in inputs (passwords, API keys, PII) is masked automatically without disturbing the workflow.
5. **Versioned output** — Outputs should carry version headers so results are traceable and reproducible.

---

## Contributing a New Skill

1. **Fork** this repository
2. **Create** a new folder under `skills/` named after your skill
3. **Write** your skill `.md` file following the standard format above
4. **Test** your skill against at least 3 different real inputs
5. **Submit** a pull request with:
   - The skill file
   - At least one example input → output in `examples/`
   - Updated skill table in this README

### Skill Quality Checklist (before PR)

- [ ] Header YAML is complete (`name`, `description`, `author`)
- [ ] Trigger conditions are clearly defined
- [ ] Workflow steps are numbered and unambiguous
- [ ] At least one concrete example (input + output excerpt)
- [ ] "What NOT to do" section is included
- [ ] Tested against edge cases and ambiguous inputs

---

## Roadmap

Skills planned or in progress:

| Skill | Status |
|---|---|
| SmartQC — Test Case Generator | ✅ Available |
| API Documentation Generator | 🔄 In progress |
| PRD Writer (Product Requirements) | 📋 Planned |
| Code Review Assistant | 📋 Planned |
| Bug Report Formatter | 📋 Planned |
| Release Note Generator | 📋 Planned |
| Merge Automation — Auto Test Runner | 📋 Planned |

---

## License

Each skill may carry its own license. Check the individual skill file for details.  
Repository template and structure: © Cook-a-Skill Contributors.

---

## Author & Maintainer

**Jennifer**
Have a skill idea or improvement? Open an issue or submit a PR.
