# BigWave — Lopo QA & Testing

QA portfolio and living test record for **Lopo**, the AI-driven WhatsApp sales/scheduling
agent built by BigWave Automação Digital.

## Overview

Lopo is a B2B conversational agent that qualifies leads (BANT), schedules appointments, and
routes leads to a CRM spreadsheet, over WhatsApp. It is built on n8n workflow automation,
integrated with a WhatsApp Business API gateway (Evolution API) and OpenAI GPT-4o.

This repository documents its Quality Assurance work: both the retrospective formalization
of early, ad-hoc testing, and the structured, ongoing certification cycle that followed
formal QA training.

## Repository Structure

- **`documentation/`** — project context, architecture overview, and QA objectives.
- **`test-cases/`** — designed functional and integration test scenarios for the WhatsApp
  flow.
- **`bug-reports/`** — certification retrospective and defect log, using a standard
  severity/acceptance-criteria format.
- **`test-evidence/`** — execution logs and evidence collected during active test cycles
  (populated as cycles run; not backfilled).

## Status

- **April 2026** — informal, ad-hoc QA work performed during active development, before
  formal QA training. Reconstructed and formalized in `bug-reports/lopo-qa-certification-log.md`.
- **June–August 2026** — formal QA training completed (LumeStack "Profissão QA" programme:
  manual testing, API testing, SQL).
- **September 2026** — structured two-week certification cycle in progress: test plan,
  formal test case execution, defect tracking, and a documented go/no-go decision on whether
  the product is ready for client-facing exposure.

## Tech Stack

n8n · Evolution API (WhatsApp) · OpenAI GPT-4o · Google Sheets · Google Calendar · Redis

## Author

**Iandra Morais** — QA Tester in transition, founder of BigWave Automação Digital.

- LinkedIn: [linkedin.com/in/iandra-morais](https://linkedin.com/in/iandra-morais)
- Live product: [bigwaveautomacaodigital.com](https://bigwaveautomacaodigital.com/)
