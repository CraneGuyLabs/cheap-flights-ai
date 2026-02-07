# cheap-flights-ai — Scoring Model

## Purpose
This document defines the authoritative AI scoring model used to rank flights in **cheap-flights-ai**.

The scoring model:
- Ranks results (does not merely filter)
- Prioritizes comfort and time before price
- Is explainable and deterministic
- Supports user-adjustable priorities without breaking core logic

All flight results are scored on a **0–100 scale**.

---

## High-Level Formula (Canonical)
⚠️ These weights are the **default canonical weights**.  
User sliders may reweight them dynamically, but the base structure is fixed.

---

## Scoring Order of Operations

1. Apply hard routing constraints
2. Normalize all viable flights
3. Compute individual component scores
4. Apply weighted aggregation
5. Rank descending by final score

No score is computed for routes that violate hard constraints.

---

## Component Scores

### 1. Price Score (0–100)

**Definition**
Measures how cost-effective a flight is relative to other viable options.

**Inputs**
- Total round-trip price
- Includes:
  - Base fare
  - Taxes & fees
  - Mandatory baggage
  - Seat selection fees (if required)

**Normalization**
- Cheapest viable option = 100
- More expensive options scale downward
- No negative scores

---

### 2. Seat Quality Score (Fixed Values)

Seat class is treated as a **first-class signal**, not a soft preference.

| Cabin Class        | Score |
|-------------------|-------|
| First Class        | 100   |
| Business Class     | 85    |
| Premium Economy    | 65    |
| Economy            | 40    |

⚠️ Seat quality is evaluated **before** price optimization.

---

### 3. Route Simplicity Score (0–100)

Measures route complexity and traveler burden.

**Base Values**
- Direct / Non-stop: 100
- 1 stop: 70
- 2 stops: 40

**Penalties**
- Airport change: −15
- Overnight layover (if allowed): −20
- Border re-clearance: −10

Minimum score floor: **0**

---

### 4. Time Efficiency Score (0–100)

Measures total trip duration efficiency.

**Inputs**
- Door-to-door flight time
- Layover durations

**Normalization**
**Penalties**
- Layovers > 3 hours: −10
- Layovers > 6 hours: −20
- Red-eye with long connection: −10

---

### 5. Upgrade Probability Score (0–100)

⚠️ **Probability-based only. Never guaranteed.**

**Inputs**
- Fare class eligibility
- Airline-specific upgrade behavior
- Historical premium cabin load patterns
- Route demand
- Time to departure

**Heuristic Bands**
- High probability: 80–100
- Moderate probability: 40–79
- Low probability: 0–39

Upgrade probability **never overrides hard constraints**.

---

## Hard Constraints (Non-Negotiable)

Flights are **excluded before scoring** if they violate:

- User-selected direct-only mode
- Maximum stops allowed
- Minimum safe layover thresholds
- Airport change disallowed by user
- Overnight layovers disallowed by user

These are binary gates, not scoring penalties.

---

## User Priority Sliders (Dynamic Reweighting)

Users may adjust:
- Comfort ↔ Price
- Speed ↔ Savings

**Rules**
- Sliders adjust weights proportionally
- No component weight may exceed 40%
- Seat Quality weight may not drop below 15%
- Route Simplicity weight may not drop below 10%

This prevents pathological rankings.

---

## Tie-Breakers (If Final Scores Match)

1. Fewer stops
2. Better seat class
3. Lower price
4. Shorter total travel time

---

## Explainability Requirement

Each ranked result must be able to answer:
- Why it ranked where it did
- Which factors helped or hurt it
- What tradeoffs exist vs alternatives

This is mandatory for user trust.

---

## Explicit Non-Goals

The scoring model does NOT:
- Guarantee upgrades
- Optimize solely for cheapest fare
- Perform hidden-city or throwaway ticketing
- Use scraped or unofficial airline data

---

## Status

- Scoring model: **Frozen**
- Weighting logic: **Locked**
- Slider constraints: **Enforced**

Any changes to this file require an explicit version bump and documentation update.
