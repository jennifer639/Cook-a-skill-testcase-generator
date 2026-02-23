# SPEC: Test Case Generator — Full Pipeline
> Skill for QC Team | Platform: Claude Project | Version: 1.0 | Date: 2025-02-23

---

## 1. SKILL OVERVIEW

| Field | Details |
|---|---|
| **Skill Name** | SmartQC — Test Case Generator Full Pipeline |
| **Users** | QC / Tester / QA Manager |
| **Platform** | Claude Project |
| **Input** | A feature spec `.md` file (Web App / API Backend / Mobile App) |
| **Output** | (1) Complete test case list + (2) Ready-to-fill test report template |

---

## 2. PROBLEM STATEMENT

### Before the skill (manual process)
- Reading spec → writing test cases manually: takes **3–6 hours** for one complex module
- Easy to miss **edge cases**, **negative cases**, **API error cases**
- Each QC writes in different formats → hard to review, hard to maintain
- After testing, must **write the report from scratch** → additional 1–2 hours
- Depends on individual experience → large gap between junior and senior output

### After the skill
- Feed spec → **generate test cases in 2–5 minutes**
- Full coverage: happy path, edge cases, negative cases, cross-platform cases
- Consistent, standardized format 100% of the time
- Report template generated simultaneously → QC only needs to fill in Pass/Fail
- Senior QC knowledge **encoded into the skill** → juniors can use it immediately

---

## 3. INPUT

### 3.1 Required Input
- **Spec `.md` file** describing the feature to be tested

### 3.2 Information the Skill Auto-Detects from Spec
The skill will **automatically analyze** the spec to identify:
- Feature type: Web UI / API / Mobile / Combined
- Main flows (happy paths)
- Boundary conditions (edge cases)
- Error scenarios (negative cases)
- Cross-platform factors if applicable

### 3.3 Optional Input (user may additionally provide)
```
- Test environment: staging / production / local
- Platforms to cover: Web / iOS / Android / API
- Focus level: Critical only / Full coverage
- Available test data (if any)
```

---

## 4. OUTPUT

The skill produces **2 artifacts** in a single run:

---

### OUTPUT 1: Test Cases Document

#### Format per test case:

```
### TC-[MODULE]-[NUM]: [Short test case name]

| Field         | Details |
|---------------|---------|
| Priority      | 🔴 Critical / 🟡 Major / 🟢 Minor |
| Type          | Happy Path / Edge Case / Negative / Performance / Security |
| Platform      | Web / iOS / Android / API / All |
| Precondition  | [Conditions required before testing] |
| Test Data     | [Specific data to use for testing] |

**Steps:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Expected Result:**
- [Clear, measurable expected outcome]

**Notes:** [Additional notes if needed]
```

#### Test case grouping structure:

```
## SECTION 1: Happy Path Cases
## SECTION 2: Edge Cases
## SECTION 3: Negative Cases
## SECTION 4: Cross-Platform Cases (if applicable)
## SECTION 5: API-specific Cases (if applicable)
## SECTION 6: Security & Validation Cases
```

#### Priority Rules (auto-assigned):
| Priority | When assigned |
|---|---|
| 🔴 Critical | Core business flow, data integrity, auth, payment |
| 🟡 Major | Secondary flows, UI/UX correctness, error handling |
| 🟢 Minor | Rare edge cases, cosmetic issues, performance nice-to-have |

---

### OUTPUT 2: Test Report Template

```markdown
# TEST REPORT — [Feature Name]

**Test Date:** ___________
**Tester:** ___________
**Environment:** ___________
**Build/Version:** ___________
**Browser/Device:** ___________

---

## SUMMARY

| Metric | Count |
|---|---|
| Total Test Cases | [auto-fill] |
| 🟢 Pass | ___ |
| 🔴 Fail | ___ |
| ⏭️ Skip | ___ |
| 🚫 Blocked | ___ |
| Pass Rate | __% |

---

## DETAILED RESULTS

| TC ID | Test Case Name | Priority | Result | Bug ID | Notes |
|---|---|---|---|---|---|
| TC-001 | [auto-fill] | 🔴 | Pass / Fail / Skip | | |
| TC-002 | [auto-fill] | 🟡 | Pass / Fail / Skip | | |
...

---

## BUG SUMMARY (if any)

| Bug ID | Related TC | Description | Severity | Status |
|---|---|---|---|---|
| BUG-001 | TC-XXX | | Critical/Major/Minor | Open |

---

## CONCLUSION & ASSESSMENT

**Feature ready for release:** ☐ Yes  ☐ No  ☐ Conditional

**Release conditions (if Conditional):**
-

**Remaining risks:**
-

**Additional notes:**
-
```

---

## 5. DETAILED WORKFLOW

```
INPUT: spec.md file
        │
        ▼
[STEP 1] ANALYZE SPEC
- Read and fully understand the spec
- Identify: feature type, actors, main flows
- List all business rules
- Detect ambiguities (unclear parts → flag for QC)
        │
        ▼
[STEP 2] MAP TEST SCENARIOS
- Outline scenarios by group:
  • Happy path (user does everything correctly)
  • Edge case (boundary values, empty, max length...)
  • Negative case (wrong input, missing permission, timeout...)
  • Cross-platform (if spec mentions Web + Mobile + API)
        │
        ▼
[STEP 3] GENERATE TEST CASES
- Write each TC in standard format
- Auto-assign Priority according to rules
- Suggest specific Test Data (no blanks left)
- Assign structured TC IDs (TC-[MODULE]-[NUM])
        │
        ▼
[STEP 4] EDGE CASE ANALYSIS
- Highlight especially important edge cases
- Flag ambiguities in spec (unclear sections)
- Suggest clarification questions for PO/Dev if needed
        │
        ▼
[STEP 5] GENERATE REPORT TEMPLATE
- Create report template with TC IDs pre-filled
- QC only needs to fill in: Pass/Fail/Skip + Bug ID
        │
        ▼
OUTPUT: Test Cases Document + Report Template
```

---

## 6. EDGE CASES THE SKILL MUST HANDLE

### 6.1 Spec-level edge cases (analyzed from spec)
- **Empty / null input**: blank fields, null, undefined
- **Boundary values**: min, max, min-1, max+1
- **Special characters**: `<script>`, `'`, `"`, emoji, unicode characters
- **Max length**: exceeding the allowed character limit
- **Concurrent actions**: multiple users performing the same action simultaneously
- **Network issues**: timeout, connection dropped mid-action
- **Permission boundaries**: unauthorized user attempting to access restricted resources

### 6.2 Platform-specific edge cases
| Platform | Specific edge cases |
|---|---|
| **Web App** | Responsive breakpoints, cross-browser (Chrome/Firefox/Safari/Edge), page refresh mid-action, browser back button |
| **API Backend** | Rate limiting, invalid token, expired token, malformed JSON, SQL injection, oversized payload, wrong HTTP method |
| **Mobile App** | Low memory, background/foreground switch, push notification received while using app, 2G/3G network, screen rotation, keyboard obscuring content |

### 6.3 Skill-level edge cases (handling input)
- **Spec too short / missing information**: Skill still generates output and flags clearly "Needs clarification: [list of questions]"
- **Spec with multiple modules**: Skill separates by module, uses different TC ID prefixes
- **Spec in Vietnamese / English / mixed**: Skill handles both, outputs in the same language as the spec

---

## 7. INPUT / OUTPUT EXAMPLES

### EXAMPLE 1 — API Login Feature

**Input spec (summary):**
```markdown
## Login API
- Endpoint: POST /api/auth/login
- Input: email, password
- Success: returns JWT token (expires in 24h)
- Fail: wrong password → 401, account locked after 5 failed attempts
```

**Output test cases (excerpt):**

```markdown
### TC-LOGIN-001: Successful login with valid email and password
| Priority | 🔴 Critical |
| Type | Happy Path |
| Platform | API |
| Test Data | email: test@example.com, password: ValidPass123! |

Steps:
1. Send POST /api/auth/login with body: {"email":"test@example.com","password":"ValidPass123!"}
2. Receive response

Expected Result:
- Status: 200 OK
- Response body contains: {"token": "<jwt_string>"}
- Token is decodable, expiry = 24h from login time

---

### TC-LOGIN-005: Account locked after 5 incorrect password attempts
| Priority | 🔴 Critical |
| Type | Edge Case |
| Platform | API |

Steps:
1. Send POST /api/auth/login with wrong password → repeat 5 times
2. Send the 6th request

Expected Result:
- Attempts 1–4: 401 {"error": "Invalid credentials"}
- Attempt 5: 401 + account is locked
- Attempt 6: 423 Locked or 401 with a distinct message

---

### TC-LOGIN-009: Send request with missing password field
| Priority | 🟡 Major |
| Type | Negative |
| Platform | API |
| Test Data | Body: {"email":"test@example.com"} |

Steps:
1. Send POST /api/auth/login without the password field

Expected Result:
- Status: 400 Bad Request
- Body contains error message identifying the missing field
```

---

### EXAMPLE 2 — Web App: Upload Avatar Feature

**Input spec (summary):**
```markdown
## Upload Avatar
- User uploads a profile picture
- Accepted formats: JPG, PNG, WEBP
- Size limit: 5MB
- After upload: cropped to 1:1 ratio, saved to S3
```

**Output test cases (excerpt):**
```markdown
### TC-AVATAR-003: Upload file exceeding 5MB
| Priority | 🔴 Critical |
| Type | Edge Case |
| Platform | Web |
| Test Data | JPG file 5.1MB |

Steps:
1. Go to profile page → click "Change avatar"
2. Select a JPG file of 5.1MB
3. Click Upload

Expected Result:
- Error message displayed: "File is too large. Please select a file under 5MB"
- File is not uploaded to the server
- Previous avatar remains unchanged

---

### TC-AVATAR-007: Upload on mobile — screen rotation during crop
| Priority | 🟡 Major |
| Type | Edge Case |
| Platform | Mobile (iOS & Android) |

Steps:
1. Open app → go to profile page → click "Change avatar"
2. Select a photo from the gallery
3. While the crop screen is displayed → rotate device 90°

Expected Result:
- Crop UI adjusts automatically to the new orientation
- No crash, selected photo is not lost
```

---

## 8. RETRY MECHANISM

When the AI fails to generate output (due to API errors, timeouts, or incomplete responses), the skill must handle failures gracefully rather than returning a blank or broken result.

### Failure Triggers
| Trigger | Description |
|---|---|
| API timeout | AI call takes longer than 30 seconds with no response |
| Incomplete output | Response is cut off mid-generation (token limit hit) |
| Malformed response | Output missing required fields or structure is broken |
| Rate limit hit | Too many requests in a short window |

### Retry Strategy
```
ATTEMPT 1 — Full generation
  │ If fails →
ATTEMPT 2 — Retry with same prompt after 5s delay
  │ If fails →
ATTEMPT 3 — Retry with simplified prompt (reduce scope, generate section by section)
  │ If fails →
FALLBACK — Return partial output with clear flag:
  "[⚠️ INCOMPLETE — Generation stopped at TC-XXX. Re-run from this point.]"
```

### Rules
- Maximum **3 retry attempts** before falling back
- Each retry logs the failure reason in the Notes field of the last TC generated
- If output is partial, the report template is still generated based on whatever TCs were completed
- User is clearly notified: which section failed, how many TCs were generated successfully, and how to resume

---

## 9. VERSION HISTORY

The skill tracks every generation run so users can compare outputs and roll back to a previous version if needed.

### Version Record Format
Each time a spec is fed and test cases are generated, a version entry is created:

```
## Version Log

| Version | Date | Input Spec | TC Count | Generated By | Notes |
|---|---|---|---|---|---|
| v1.0 | 2025-02-23 | spec_login_v1.md | 14 TCs | SmartQC Skill | Initial generation |
| v1.1 | 2025-02-24 | spec_login_v2.md | 17 TCs | SmartQC Skill | Added OTP flow |
| v1.2 | 2025-02-24 | spec_login_v2.md | 17 TCs | SmartQC Skill | Regenerated after prompt refinement |
```

### Version Naming Convention
| Scenario | Version bump |
|---|---|
| New spec file fed | Minor bump: v1.0 → v1.1 |
| Same spec, skill re-run | Patch bump: v1.1 → v1.1.1 |
| Major spec rewrite | Major bump: v1.x → v2.0 |

### Rollback
- All previous versions are stored as separate files: `test-cases-v1.0.md`, `test-cases-v1.1.md`
- User can explicitly request: *"Roll back to v1.0"* → skill reloads and displays the previous output
- Version files are pushed to GitHub with each generation → full audit trail via commit history

### What is versioned
| ✅ Versioned | ❌ Not versioned |
|---|---|
| Generated test cases | Draft notes |
| Report template | Intermediate prompts |
| Spec file used as input | AI conversation logs |
| TC count & coverage summary | |

---

## 10. SECURITY MASKING

Before feeding a spec into the skill and before outputting test cases, all sensitive data must be detected and masked to prevent accidental exposure in logs, GitHub repos, or shared documents.

### What Counts as Sensitive Data
| Category | Examples |
|---|---|
| Credentials | Passwords, API keys, secret tokens, private keys |
| Personal data (PII) | Real names, email addresses, phone numbers, national IDs |
| Financial data | Real credit card numbers, bank account numbers |
| Internal infrastructure | Internal IP addresses, internal domain names, database connection strings |
| Business-sensitive | Unreleased feature names, internal pricing, client names |

### Masking Rules

**In Input Spec (before processing):**
- Skill scans spec for patterns matching sensitive categories
- Detected values are replaced with safe placeholders before being used in any prompt
- Original spec file is never stored or logged

**In Generated Test Cases (output):**
- Test Data fields must never contain real sensitive values
- Use masked placeholders instead:

| Sensitive Value Type | Masked Placeholder |
|---|---|
| Password | `[TEST_PASSWORD]` or `ValidPass123!` (generic) |
| API Key | `[API_KEY_PLACEHOLDER]` |
| Real email | `test@example.com` or `user_{n}@testdomain.com` |
| Real phone number | `+84-900-000-000` (dummy) |
| Credit card | `4111 1111 1111 1111` (Stripe test card) |
| National ID | `[MASKED_ID]` |
| Internal IP | `192.0.2.x` (documentation range per RFC 5737) |

### Flag & Warn
If sensitive data is detected in the input spec, the skill must:
1. **Mask** the value before processing
2. **Warn** the user at the top of the output:

```
⚠️ SECURITY NOTICE
The following sensitive data patterns were detected in your spec and have been masked:
- Line 12: API key → replaced with [API_KEY_PLACEHOLDER]
- Line 34: Email address → replaced with test@example.com
Please review your spec file and avoid including real credentials or PII.
```

### What the Skill Does NOT Store
- Raw input spec content
- Unmasked test data
- User credentials of any kind
- Conversation history beyond the current session (Claude Project scope)

---

## 11. LIMITATIONS (What the skill cannot do yet)

| Limitation | Explanation | Workaround |
|---|---|---|
| Does not execute tests | Skill only generates test cases, does not run them | QC performs the steps manually |
| No Jira/TestRail integration | Cannot auto-create tickets | Copy-paste output into the tool |
| Does not auto-generate test data | Suggests test data but does not create fake data | QC uses an additional faker tool |
| Cannot test visual/pixel-perfect UI | Does not compare screenshots | Use Percy/Chromatic additionally |
| Vague spec → poor output | Garbage in, garbage out | A good spec is required before feeding |

---

## 12. EXPANSION ROADMAP

| Phase | Feature | Effort |
|---|---|---|
| **v1.1** | Auto-export to `.xlsx` (Jira-compatible) | Low |
| **v1.2** | Accept additional input: Figma link / Postman collection | Medium |
| **v2.0** | Jira API integration → auto-create tickets | High |
| **v2.1** | Accept test results → auto-generate bug report | High |
| **v3.0** | AI agent auto-runs tests on Web via browser automation | Very High |

---

## 13. DEPLOYMENT INFORMATION

| Field | Details |
|---|---|
| **Platform** | Claude Project |
| **How to deploy** | Upload SKILL.md into Claude's Project Instructions |
| **How to use** | Upload spec.md file into a conversation → AI auto-generates |
| **Not required** | Code, server, deployment pipeline |
| **AI tool** | Claude Sonnet (powerful, fast, cost-effective) |

---

*This spec was created using Claude AI | Version 1.0 | Pending Supervisor approval*
