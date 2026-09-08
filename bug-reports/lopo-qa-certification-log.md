# Lopo (BigWave) — QA Certification Retrospective

**Author:** Iandra Morais, QA Tester
**Project:** BigWave Automação Digital — Lopo (WhatsApp AI agent)
**Period covered:** April 2026 (pre-formal-QA-training work)
**Document type:** Retrospective test documentation, reconstructed and formalized in September 2026

## 1. Overview

This document formalizes ad-hoc quality assurance work performed on Lopo, an AI-powered
WhatsApp sales/scheduling agent (n8n + WhatsApp Business API integration + LLM), during
active development in April 2026 — before the author had completed any formal QA training.

The original work was not documented using standard QA artifacts at the time. This
retrospective reconstructs it using correct terminology and structure, both as an honest
record of the project's history and as a portfolio piece demonstrating QA aptitude that
predates formal training.

## 2. Test Approach

The testing performed in April 2026 was **exploratory / ad-hoc testing embedded in active
development**, not pre-planned scripted testing. Bugs were identified reactively while
building and adjusting the flow, and a certification checklist was drafted mid-project once
the need for a formal go/no-go gate became clear. This distinction is stated explicitly
because a credible QA report does not overstate its own methodology.

## 3. Scope

### 3.1 In scope (WhatsApp channel)

- BANT-based lead qualification flow
- Appointment scheduling (calendar integration)
- Lead routing (hot / cold leads) to CRM spreadsheet
- Automated re-engagement sequence after lead silence
- Sticker / emoji handling
- Operator controls: pause a conversation, lock a contact, restart command
- Operator notification on lead qualification

### 3.2 Out of scope / not completed

| Item | Reason |
|---|---|
| Image / file reception | Blocked on a media-download integration issue (WhatsApp media URLs are short-lived and authenticated; the workaround via the WhatsApp gateway's dedicated media-retrieval endpoint was not completed) |
| Instagram Direct channel | Separate integration, still under construction at the time (webhook receiving events, but the reply pipeline and agent connection were not finished) |
| CRM backend (dedicated server-side store) | Explicitly deferred by the author to a later development phase |

## 4. Certification Requirements (Acceptance Criteria)

Drafted as a formal go/no-go gate before exposing the agent to a beta client group.

| ID | Requirement | Category | Pass Criteria | Verified Outcome (as of April 2026) |
|---|---|---|---|---|
| REQ-01 | Qualification before pricing | Blocker | Agent never discloses price before completing Budget/Need qualification | Not met — reported as an open defect |
| REQ-02 | Flow stability (core logic node) | Blocker | Executes without error across 5 consecutive, distinct conversations | Pending re-verification |
| REQ-03 | Lead logging to spreadsheet | Blocker → Minor | Lead tag recorded correctly in 3/3 test conversations | Partially met — tagging defect reported |
| REQ-04 | Media reception without breaking the flow | Blocker | Photo and audio received without interrupting the conversation | Partially met — audio passed; image never completed |
| REQ-05 | Operator pause control | Blocker | Operator can pause and resume a conversation without losing context | Designed; execution not confirmed complete |
| REQ-06 | Contact lock | Blocker | A locked contact receives no response from the agent | Designed; execution not confirmed complete |
| REQ-07 | Lead name collected before scheduling | Minor | Documented as known gap; does not block certification | Accepted as technical debt |
| REQ-08 | Graceful error handling | Blocker | Fallback message shown instead of silence or a crash | Not confirmed tested |

**Certification rule (as originally defined):** REQ-01, 02, 04, 05, 06 and 08 must pass at
100% for certification. REQ-03 tolerates one documented failure. REQ-07 is accepted as
technical debt and does not block certification.

**Result:** Full A-to-Z certification was **not completed** in April 2026. This is the gap
that the September 2026 QA cycle (see companion test tracker) exists to close.

## 5. Bug Report Log

| ID | Title | Severity | Steps to Reproduce | Expected | Actual | Root Cause | Status (Apr 2026) |
|---|---|---|---|---|---|---|---|
| BUG-01 | Price disclosed before qualification | Blocker | Lead asks for pricing at the start of the conversation | Agent defers pricing until Budget/Need is established | Agent discloses price immediately | Prompt/flow ordering issue — pricing step not gated behind qualification state | Open |
| BUG-02 | Core logic node instability | Blocker | Run several consecutive real conversations | Node executes without error every time | Node fails intermittently | Not fully diagnosed; flagged for stabilization | Open |
| BUG-03 | Image reception breaks the flow | Blocker | Send a photo to the agent | Flow continues; agent responds normally or with a graceful fallback | Flow fails while attempting to fetch the media file | WhatsApp media URLs are short-lived and require gateway-level authentication; the integration to fetch media through the proper gateway endpoint was not completed | Open — deferred to next session, never closed |
| BUG-04 | Lead tag not always recorded correctly | Minor | Complete a full qualification conversation | Spreadsheet row includes the correct lead-status tag | Tag occasionally missing or incorrect | Not diagnosed | Open |
| BUG-05 | Lead name not always collected before scheduling | Minor | Lead proceeds to scheduling without providing full name earlier in the conversation | Full name collected before the calendar event is created | Scheduling can proceed without it | Flow ordering gap | Accepted as technical debt (REQ-07) |

## 6. Retrospective Note

This body of work was produced entirely by instinct, several months before the author
began formal QA training (LumeStack "Profissão QA" programme, started June 2026, completed
August 2026). Read with hindsight, it already contains recognizable QA practice: a severity
scale, measurable acceptance criteria, dependency-gated test phases, and root-cause-driven
debugging — arrived at without a QA vocabulary to name them.

The gap it also reveals — a certification plan that was designed but never executed to
completion — is precisely what the September 2026 QA cycle on Lopo was structured to close,
this time following a documented test plan, formal test case design, and a recorded go/no-go
decision.

## 7. Related Documents

- `documentation/case-study.md` — project context and QA objectives.
- `test-cases/whatsapp-functional-scenarios.md` — designed test scenarios.
- BigWave QA Tracker (September 2026 cycle) — current test plan, test case execution,
  bug log and go/no-go decision for this round.
