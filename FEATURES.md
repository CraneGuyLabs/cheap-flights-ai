# Cheap Flights — Features

## 1. Cheap Round-Trip Flights (Default)
- Round-trip is the default search mode.
- AI evaluates true total trip cost, including:
  - Cabin class
  - Seat quality
  - Baggage
  - Boarding group
  - Change / cancellation penalties

---

## 2. AI-Powered Optimization Engine
- Results are ranked using a weighted scoring model, not simple filters.
- Core scoring inputs:
  - Price
  - Seat quality
  - Route simplicity
  - Total travel time
  - Upgrade probability
  - Included perks
- Users control priority sliders (comfort vs price, speed vs savings).

---

## 3. Quality Seating First (Reverse Search Logic)
Search order:
1. First Class
2. Business Class
3. Premium Economy
4. Economy

The AI attempts to reduce cost by stepping down in class rather than upgrading from economy.

---

## 4. Route Preference Hierarchy
For round-trip flights, routes are evaluated in strict order:
1. Direct / Non-stop
2. 1 stop
3. 2 stops (last resort)

Each additional stop applies a ranking penalty.

---

## 5. Layover & Connection Control
If stops are unavoidable:
- Enforce minimum safe layover times.
- Penalize:
  - Tight connections
  - Airport changes
  - Overnight layovers unless explicitly allowed.
- Users may allow stops only if savings exceed a defined dollar threshold.

---

## 6. Destination-First Discovery
Users may search by:
- Specific city or airport
- Region (e.g. Caribbean)
- Travel intent (e.g. “warm destinations in March”)

Results are ranked by comfort and total cost.

---

## 7. Airline Preference Options
- Users may prefer or exclude specific airlines.
- Airline preferences are weighted inputs, not hard filters by default.
- AI may override preferences only if savings exceed a user-defined threshold.

---

## 8. Priority Boarding Preferences
AI favors fares that include:
- Priority boarding
- Early boarding groups
- Overhead bin certainty

Handled via fare-class intelligence.

---

## 9. Package Deals (All-Inclusive & Bundles)
- Supports:
  - Flight + hotel
  - Flight + resort
  - All-inclusive packages
- Packages surface only when they provide superior value compared to booking separately.

---

## 10. Business-Class Upgrade Probability Scoring
- Upgrade scoring is probability-based and never guaranteed.
- AI evaluates:
  - Premium cabin availability
  - Airline upgrade behavior
  - Discounted business-class inventory
- Results are labeled clearly:
  - High upgrade probability
  - Moderate upgrade probability

---

## 11. Discounted & Reduced-Cost Upgrades
- Detects:
  - Cash upgrade offers
  - Discounted business-class fares
  - Bundled upgrade pricing
- Upgrade value is shown transparently.

---

## 12. Automatic Savings Engine
- Tracks selected routes.
- Alerts users when:
  - Prices drop
  - Better cabins become cheaper
  - Direct flights replace connections
- Displays clear savings deltas (e.g., “Same trip, better seat — save $213”).

---

## 13. Trip Type Control
Users explicitly choose:
- Round-trip (default)
- Direct-only
- Flexible (AI-optimized)

Direct-only mode suppresses all connecting flights and warns when price premiums exceed thresholds.
