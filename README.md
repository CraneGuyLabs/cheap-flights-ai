# cheap-flights-ai

**AI-powered, comfort-first flight and package deal finder**  
Optimizes for direct routes, premium seating, time efficiency, and real savings — not just the cheapest fare.

---

## Overview

`cheap-flights-ai` is not a traditional “cheap flights” app.

Most flight search tools optimize only for price and hide tradeoffs like poor seats, long layovers, and inconvenient routes. This project takes a different approach:

> **Comfort and time are optimized first. Price is optimized intelligently second.**

The result is fewer bad trips, better seats, fewer stops, and transparent savings.

---

## Core Principles

- **Round-trip first**: Most travelers book round trips — the app is built around that reality.
- **Comfort-first ranking**: Premium cabins are evaluated before economy.
- **Direct over cheap**: Direct routes are always favored unless savings justify connections.
- **AI, not filters**: Results are ranked using a weighted scoring model, not checkbox filtering.
- **Transparency**: No “guaranteed upgrades” or misleading prices.

---

## Key Features

### ✈️ Round-Trip Flights (Default)
- Round-trip is the default mode
- True total cost includes:
  - Cabin class
  - Seat quality
  - Baggage
  - Boarding group
  - Change / cancellation penalties

---

### 🧠 AI-Powered Optimization
Flights are ranked using a weighted AI scoring model that considers:
- Price
- Seat quality
- Route simplicity
- Total travel time
- Upgrade probability
- Included perks

Users control priorities via **sliders**, not filters:
- Comfort ↔ Price
- Speed ↔ Savings

---

### 💺 Quality Seating First
Search order:
1. First Class  
2. Business Class  
3. Premium Economy  
4. Economy  

The AI attempts to **step down in class to reduce cost**, rather than upgrading from economy.

This is a core differentiator.

---

### 🔁 Route Preference Hierarchy
Routes are evaluated in strict order:
1. Direct / Non-stop  
2. 1 stop  
3. 2 stops (last resort)

Each additional stop applies a ranking penalty.

---

### ⏱ Layover Optimization
If stops are unavoidable:
- Minimum safe layover times enforced
- Penalties for:
  - Tight connections
  - Airport changes
  - Overnight layovers (unless allowed)

Users may allow stops **only if savings exceed a defined amount**.

---

### 🌍 Destination-First Discovery
Users can search by:
- City or airport
- Region (e.g. Caribbean)
- Travel intent (e.g. “warm destinations in March”)

Results return **best-value destinations**, ranked by comfort and cost.

---

### 🏷 Airline Preferences
- Prefer or exclude airlines
- Preferences are weighted, not absolute
- AI may override only if savings exceed a user-defined threshold

---

### 🧳 Priority Boarding Awareness
AI favors fares that include:
- Priority boarding
- Early boarding groups
- Overhead bin certainty

Handled via fare-class intelligence.

---

### 🏨 Package Deals
Supports:
- Flight + hotel
- Flight + resort
- All-inclusive packages

Packages surface **only when they provide better value than booking separately**.

---

### 🚀 Business-Class Upgrade Probability
⚠️ **Probability-based only — never guaranteed**

AI evaluates:
- Premium cabin availability
- Airline upgrade behavior
- Discounted business-class inventory

Labeled clearly as:
- High upgrade probability
- Moderate upgrade probability

---

### 💸 Automatic Savings Engine
- Track selected routes
- Alerts when:
  - Prices drop
  - Better cabins become cheaper
  - Direct routes replace connections

Savings are shown clearly:
> “Same trip, better seat — save $213”

---

### 🎛 Trip Type Control
Users choose:
- Round-trip (default)
- Direct-only
- Flexible (AI-optimized)

Direct-only mode suppresses all connecting flights and warns when cost premiums exceed thresholds.

---

## MVP Scope

The initial MVP focuses on:
- Round-trip flights
- AI ranking engine
- Seat-class-first search
- Direct-route prioritization
- Layover penalties
- Destination-first discovery
- Price & seat alerts

Package deals and loyalty-aware routing follow after validation.

---

## Positioning

**cheap-flights-ai** is a:
- Comfort-optimized travel engine
- Subscription-ready product
- Tool for travelers who value time, seats, and transparency

It is intentionally **not** a race-to-the-bottom fare scraper.

---

## Status

- FEATURES.md: **Frozen**
- AI scoring model: **Defined**
- MVP screen flow: **Locked**

Next steps:
- API selection
- Repo structure
- Initial data models

---

## Disclaimer

Upgrade probabilities are estimates based on historical and market data.  
No upgrades or savings are guaranteed.

---

## License

TBD
