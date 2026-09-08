# Test Scenarios — Lopo WhatsApp Flow

Functional and integration test scenarios designed to validate the B2B qualification
workflow managed by n8n and the Evolution API.

**Status:** designed scenarios. Execution against the current build is tracked in the
active September 2026 QA cycle (private test tracker) and in
`bug-reports/lopo-qa-certification-log.md` for the earlier, retrospective cycle. This file
records the scenario design, not a claimed pass rate.

---

## TC-001 — Out-of-Scope Lead Response (Conversation Boundary)

**Description:** Verify how Lopo handles unexpected or hostile responses from a restaurant
owner that fall outside the sales qualification scope.

**Pre-conditions:** The n8n workflow is active, and Lopo has initiated contact with a
verified lead.

**Steps:**
1. Reply to Lopo with an unrelated question (e.g., "What is the weather like today in Cork?").
2. Send a second message with a hostile/rejection tone (e.g., "Stop texting me, this is a scam").

**Expected Result:** Lopo maintains a professional tone, avoids answering out-of-scope
questions, and flags the conversation for human intervention (or stops the automation) if a
rejection-keyword rule is triggered.

---

## TC-002 — Multi-format Input Handling (Robustness)

**Description:** Verify Lopo's stability when a lead sends non-text media (audio, image)
during the qualification process.

**Pre-conditions:** The Evolution API is connected and forwarding webhooks to n8n.

**Steps:**
1. Send a voice note longer than 2 minutes describing a restaurant's problem.
2. Send an image (e.g., a screenshot of a menu) without any text description.

**Expected Result:** The system does not crash or loop. The webhook payload reaches n8n, and
Lopo triggers a fallback response (e.g., a human agent will review the media) rather than
failing silently.

---

## TC-003 — Evolution API Downtime (Integration Failure)

**Description:** Verify system behavior and error handling when the Evolution API service
drops while n8n is processing a workflow step.

**Pre-conditions:** Access to n8n execution history.

**Steps:**
1. Trigger a qualification workflow in n8n.
2. Simulate an API failure (e.g., pause the Evolution API container, or force an invalid API
   key).
3. Observe the n8n execution node.

**Expected Result:** The n8n workflow shows a clear error state (node failed / timeout),
handles the error gracefully without losing the lead's conversation history, and — ideally —
triggers an alert to the operator.
