# 🎯 AI Opportunity & Learning Radar (Zero-Cost n8n Engineering Project)

## 1. Problem Statement & Project Goals
Independent developers and automation engineers spend excessive time manually checking disparate job boards, open-source bounty repositories, and technical news aggregators—most of which are filled with noise, region-locked roles, duplicate listings, or unverified claims.

**Project Goal:** Build a self-hosted, fault-tolerant, ₹0-cost automation pipeline in **n8n (v2.35.7)** on Ubuntu Linux that:
1. **Collects** live software bounties, remote technical roles, and AI/automation engineering signals from verified public APIs.
2. **Normalizes & Validates** heterogeneous JSON payloads into a strict internal schema while preserving raw source evidence.
3. **Deduplicates & Scores** items deterministically against a specific developer stack (`Python`, `FastAPI`, `Next.js`, `TypeScript`, `PostgreSQL/Supabase`, `Docker`, `n8n`, `Linux`) with diversity caps so no single organization monopolizes the report.
4. **Delivers** an actionable daily HTML digest via encrypted SMTP containing direct links, verification status disclaimers, and capture instructions.

**Explicit Non-Goals (Honesty Policy):**
* This system does **not** scrape login-walled platforms (e.g., Upwork, LinkedIn) or violate platform Terms of Service.
* Triage scores represent **stack and criteria overlap**, not an objective probability of earning money or being hired.
* All compensation and India-eligibility fields distinguish between source-reported metadata and independently verified facts.

---

## 2. System Architecture Diagram

```text
[Manual Trigger] ──┐     ┌──> [Fetch GitHub Bounties (HTTP GET + Retry/Continue)] ──┐
                   ├────>├──> [Fetch RemoteOK Jobs   (HTTP GET + Retry/Continue)] ──┼──> [Merge (Append, 3 Inputs)]
[Schedule Trigger] ┘     └──> [Fetch HN AI Signal    (HTTP GET + Retry/Continue)] ──┘              │
                                                                                                   ▼
[Gmail Inbox] <── [Send an Email (SMTP SSL:465)] <── [Build Daily Digest & Deduplicate] <── [Normalize Filter & Build Action Plan]
