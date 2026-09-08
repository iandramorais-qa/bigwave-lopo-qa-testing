# QA Case Study — Lopo (BigWave)

## Project Focus

**Lopo** is a B2B AI Sales Development Representative (SDR): an AI-driven agent that
qualifies leads and engages restaurant owners in Portugal over WhatsApp, on behalf of BigWave
Automação Digital.

The architecture combines **n8n** for workflow automation, hosted via Easypanel, integrated
with the **Evolution API** for WhatsApp messaging, and **OpenAI GPT-4o** for conversation.

## QA Objectives

Validate Lopo's conversational workflow, integration stability (n8n ↔ Evolution API ↔
GPT-4o), and business logic (BANT qualification, scheduling, CRM handoff), through structured
manual and exploratory testing — ensuring the automated qualification funnel correctly
handles edge cases before human handover or client-facing exposure.

## In Scope

- BANT-based lead qualification
- Appointment scheduling (calendar integration)
- Lead routing (hot / cold) to the CRM spreadsheet
- Automated re-engagement after lead silence
- Operator controls (pause a conversation, lock a contact)
- Sticker / emoji handling

## Out of Scope (current cycle)

- Image / file reception (unresolved integration issue — see `bug-reports/`)
- Instagram Direct channel (separate, still under construction)
- Dedicated CRM backend (deferred to a later development phase)

## Methodology

Two distinct phases make up this project's QA history:

1. **Ad-hoc / exploratory testing (April 2026)** — testing embedded reactively in active
   development, before the author had completed formal QA training. See
   `bug-reports/lopo-qa-certification-log.md` for the reconstructed, formalized record.
2. **Structured certification cycle (September 2026)** — a planned two-week cycle following
   a documented test plan: test case design, manual functional execution, API/webhook
   testing, defect tracking, and a recorded go/no-go decision.

## Note

This project is part of a career transition into Software QA, combining hands-on product
development with rigorous software testing methodology.
