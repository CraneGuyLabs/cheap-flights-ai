# cheap-flights-ai — System Architecture

## Purpose
This document defines the system architecture for **cheap-flights-ai**.  
It describes data flow, service boundaries, scoring logic separation, and design constraints to ensure scalability without rework.

This architecture is optimized for:
- AI-driven ranking (not filtering)
- Comfort-first logic
- Incremental feature rollout (packages, upgrades)
- Clear separation of concerns

---

## High-Level Architecture
The backend owns **all intelligence**.  
External APIs are treated strictly as **data sources**, never decision-makers.

---

## Core Components

### 1. Client Layer
**Responsibilities**
- Collect user input
- Display ranked results
- Show AI explanations
- Manage alerts & tracked trips

**Client does NOT**
- Score flights
- Filter routes beyond user intent
- Interpret airline fare logic

All intelligence remains server-side.

---

### 2. API / Backend Layer
Acts as the **orchestrator**.

**Responsibilities**
- Normalize external API data
- Apply routing & layover rules
- Invoke AI scoring engine
- Return ranked, explainable results

**Key Design Rule**
> No external API response is ever returned directly to the client.

---

### 3. Flight Data Layer (External APIs)

#### Primary Provider (MVP)
**Amadeus Self-Service API**

Used for:
- Flight search (round-trip & direct)
- Cabin class data
- Fare family / branded fare attributes
- Airline & airport metadata

**Assumptions**
- Amadeus provides raw availability and pricing
- All comfort logic is computed internally

---

### 4. Normalization Layer

External data is normalized into internal models:

**Canonical Models**
- `Flight`
- `Segment`
- `Fare`

This ensures:
- Provider-agnostic scoring
- Future API swaps without refactors
- Consistent scoring inputs

---

### 5. Routing & Layover Rules Engine

Applies **hard constraints before scoring**:
- Direct → 1 stop → 2 stop hierarchy
- Minimum safe layover times
- Airport-change penalties
- Overnight layover rules

This prevents bad routes from contaminating scoring results.

---

### 6. AI Scoring Engine (Core Intelligence)

Each flight is scored **0–100** using weighted components:

- Price Score
- Seat Quality Score
- Route Simplicity Score
- Time Efficiency Score
- Upgrade Probability Score

**Key Rule**
> Scoring ranks options; it does not filter them out unless a hard constraint is violated.

User sliders dynamically adjust weights, but default weights remain canonical.

---

### 7. Upgrade Probability Engine

There is **no external API** for upgrades.

Upgrade probability is inferred using:
- Fare class eligibility
- Historical premium cabin load heuristics
- Airline-specific upgrade behavior
- Route demand patterns
- Time-to-departure windows

**Output**
- High probability
- Moderate probability

⚠️ Never guarantees outcomes.

---

### 8. Package Deals (Phase 2)

Handled as a **parallel data stream**, not merged into flight logic.

- Flight-only logic remains pure
- Packages are evaluated independently
- Only surfaced if they outperform flight-only options

This avoids corrupting core flight ranking logic.

---

### 9. Automatic Savings & Alerts Engine

Background service responsible for:
- Tracking watched routes
- Periodic price rechecks
- Detecting:
  - Price drops
  - Cabin improvements
  - Route improvements (direct replacing stops)

Alerts are generated **only when objective improvement occurs**.

---

## Data Flow (Step-by-Step)

1. User submits search parameters
2. Backend queries Amadeus
3. Raw results normalized into internal models
4. Routing & layover rules applied
5. AI scoring engine ranks flights
6. Results returned with:
   - Scores
   - Explanations
   - Upgrade probability labels
7. Optional tracking saved for alerts

---

## Non-Goals (Explicit)

This system does NOT:
- Guarantee free upgrades
- Scrape airline websites
- Perform hidden-city or throwaway ticketing
- Optimize solely for cheapest fare

These are intentionally excluded for reliability and trust.

---

## Scalability Considerations

- Provider-agnostic normalization allows multi-API expansion
- Scoring engine is stateless and horizontally scalable
- Alert engine is asynchronous and decoupled
- Package deals do not affect core flight logic

---

## Security & Compliance Notes

- API keys stored server-side only
- No PII stored without explicit user consent
- Pricing and upgrade probabilities are estimates and disclosed as such

---

## Status

- FEATURES.md: Frozen
- README.md: Complete
- Architecture: Defined

Next recommended documents:
- `docs/scoring-model.md`
- `docs/api-notes.md`

---
