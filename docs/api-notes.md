# cheap-flights-ai — API Notes & Assumptions

## Purpose
This document records known behaviors, limitations, and assumptions for all external APIs used by **cheap-flights-ai**.

Its goals are to:
- Prevent hidden logic errors
- Avoid overpromising features APIs cannot support
- Ensure consistent interpretation of external data
- Enable future API swaps without architectural changes

---

## Primary Flight Data Provider (MVP)

### Amadeus Self-Service APIs

**Used For**
- Round-trip flight search
- Direct vs connecting route detection
- Cabin class identification
- Fare family and branded fare attributes
- Airline and airport metadata

---

## Data Reliability Assumptions

- Prices returned by Amadeus are **point-in-time estimates**
- Inventory availability can change rapidly
- Fare rules may differ at booking time

**Implication**
> No price or upgrade is considered final until redirected booking completes.

---

## Cabin Class & Fare Family Notes

- Cabin class is reliable at a **high level**:
  - First
  - Business
  - Premium Economy
  - Economy
- Sub-variants (e.g. Economy Light, Basic Economy) must be normalized internally.

**Fare Family Caveats**
- Priority boarding, seat selection, and baggage inclusion vary by airline.
- Branded fare names are **not standardized** across airlines.

**Mitigation**
- Maintain internal airline metadata mapping:
  - Boarding group inclusion
  - Baggage rules
  - Seat selection defaults

---

## Route & Segment Behavior

- Multi-stop itineraries may be returned in multiple permutations.
- Some itineraries include:
  - Self-transfer risks
  - Long layovers disguised as short connections

**Mitigation**
- All itineraries must pass through routing and layover rules before scoring.

---

## Layover Time Caveats

- Minimum connection times (MCT) may be optimistic.
- Airport congestion, customs, and security are not reflected in API data.

**Rules**
- Apply conservative minimum layover thresholds internally.
- Penalize tight connections even if API flags them as valid.

---

## Airport Changes

- Amadeus may return itineraries with airport changes in the same city.
- These are often undesirable for comfort-first travelers.

**Handling**
- Airport changes incur heavy penalties or are excluded if user disallows them.

---

## Upgrade & Fare Class Limitations

- Amadeus does **not** provide:
  - Upgrade inventory
  - Upgrade eligibility guarantees
  - Loyalty status effects

**Implication**
> Upgrade probability must always be inferred, never asserted.

---

## Upgrade Probability Guardrails

Upgrade probability scoring must:
- Be labeled clearly as probability
- Never be marketed as guaranteed
- Never override hard routing constraints
- Never influence booking eligibility

---

## Package Deals (Phase 2)

- Package APIs (e.g. Expedia Rapid) return **bundled pricing only**
- Package pricing may obscure individual component costs

**Rule**
- Package logic must remain isolated from core flight ranking.
- Packages are evaluated in parallel and surfaced only if superior.

---

## Rate Limits & Quotas

- Amadeus Self-Service has:
  - Request rate limits
  - Monthly usage caps

**Mitigation**
- Cache identical searches
- Debounce rapid user input
- Avoid re-querying for alert checks unless necessary

---

## Error Handling Expectations

- API timeouts are expected
- Partial responses may occur

**Required Behavior**
- Fail gracefully
- Never return unscored or unranked results
- Provide clear user-facing fallback messaging

---

## Data Normalization Rules (Non-Negotiable)

- All monetary values normalized to a single currency before scoring
- All times normalized to UTC internally
- All distances and durations computed internally, not trusted blindly from API

---

## Compliance & Legal Notes

- No scraping or reverse engineering
- All API usage must comply with provider TOS
- Affiliate disclosures required where applicable

---

## Explicit Non-Goals

The API layer does NOT:
- Guarantee prices
- Guarantee upgrades
- Bypass airline rules
- Optimize for hidden-city or throwaway ticketing

---

## Status

- API assumptions: **Documented**
- Limitations: **Acknowledged**
- Guardrails: **Enforced**

Any API changes require review and update of this document.
