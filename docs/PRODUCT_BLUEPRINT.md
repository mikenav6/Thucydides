# Thucydides Product Blueprint

## 1) Product Vision
**Thucydides** is a web-based geopolitical strategy simulation designed to teach global affairs through realistic, consequence-driven decision-making.

Players assume leadership of any recognized sovereign state and respond to fast-changing domestic and international events. Every decision updates military readiness, economic stability, social cohesion, diplomatic relationships, and long-term strategic outcomes.

Core goals:
- Deliver a **serious simulation** with game-like engagement.
- Make complex geopolitics approachable through guided education.
- Model short- and long-term consequences with transparent explanations.

---

## 2) Player Experience (High-Level)

### Game Loop
1. Choose country and scenario (e.g., border crisis, sanctions regime, climate emergency).
2. Review briefing dashboard (economy, military, domestic politics, alliances, logistics).
3. Make policy choices under constraints (budget, time, public support, legal obligations).
4. Observe real-time consequences and second-order effects.
5. Receive analytical debrief with “why this happened” educational explanations.

### Win/Loss Framing
Not a binary “world domination” game. Success is measured by:
- Stability and legitimacy of governance.
- Human development and resilience.
- Strategic objectives achieved with acceptable tradeoffs.
- Avoidance of catastrophic outcomes (civil war, collapse, famine, strategic defeat).

---

## 3) Realism Framework

### Simulation Pillars
- **Military realism**: force structure, logistics, readiness, sustainment, deterrence.
- **Economic realism**: GDP composition, debt, inflation, trade dependence, energy security.
- **Political realism**: regime constraints, coalition politics, public sentiment, elite factions.
- **Diplomatic realism**: alliance obligations, sanctions, treaty costs, reputational effects.
- **Social realism**: demographics, education, inequality, migration pressure.

### Consequence Engine (Explainable)
Use a weighted systems model where each action affects multiple linked indicators:
- Immediate effects (hours/days)
- Medium-term effects (weeks/months)
- Long-term effects (years)

Each result should expose:
- Which variables changed
- Why weights applied
- What uncertainty/confidence bounds exist

---

## 4) Country Data Scope

### Coverage
- Include all currently recognized sovereign nations.
- Country profile generated from a normalized data model with versioned snapshots.

### Proposed Source Use
- **CIA World Factbook**: demographic, economic, governance, geography context.
- **Global Firepower**: military capability indicators.

### Compliance Requirement
Before integration, validate each source’s terms for reuse, redistribution, scraping/API access, and attribution. If direct reuse is restricted, implement either:
- licensed/permissioned data access, or
- substitution with open/commercially permitted datasets.

### Country Starting-Standings Baseline
At game start, each country receives a baseline standing derived from normalized indicators across military capacity, economic resilience, demographics, and governance stability.

- CIA World Factbook and Global Firepower are treated as **reference sources** for shaping the metric model during development.
- The game does **not** require direct in-game republication of those sources to launch the experience.
- Baseline metrics should be computed from legally approved, provenance-tracked inputs with the same schema so sources can be swapped without redesigning gameplay logic.

---

## 5) Data Model (v1)

### Core Country Entity
- `country_id`
- `name`, `iso_codes`
- `government_type`, `stability_index`
- `population`, `urbanization`, `median_age`
- `gdp_nominal`, `gdp_ppp`, `inflation`, `debt_to_gdp`
- `energy_import_dependency`, `food_import_dependency`
- `military_personnel_active`, `reserve_strength`
- `air_power_index`, `land_power_index`, `naval_power_index`
- `alliance_graph`, `regional_blocs`
- `strategic_resources`
- `infrastructure_resilience`
- `education_index`, `health_capacity`

### Dynamic State
- `public_support`
- `elite_support`
- `military_readiness`
- `intel_confidence`
- `sanctions_exposure`
- `supply_chain_stress`
- `war_fatigue`
- `diplomatic_trust_by_country`

---

## 6) Scenario & Event System

### Scenario Types
- Interstate conflict escalation
- Economic crisis and debt distress
- Resource shock (energy/food/water)
- Insurgency/civil conflict
- Cyber attacks on critical infrastructure
- Pandemic and climate disasters

### Event Design Rules
- Events chain from player actions and global AI actor responses.
- Include hidden variables and fog-of-war to avoid deterministic play.
- Provide post-event “intel update” to support learning.

---

## 7) AI & Decision Analysis

### NPC Nations
Each non-player country should have:
- Strategic doctrine (risk profile, red lines)
- Domestic constraints (elections, unrest, fiscal limitations)
- Alliance commitments and rivalries

### Decision Evaluation Pipeline
1. Convert decision into policy vector.
2. Simulate first-order effects using country models.
3. Run multi-agent reaction step for external actors.
4. Propagate second-order effects via global dependency graph.
5. Return outcome + confidence interval + explanation.

---

## 8) Web App Architecture (Recommended)

### Frontend
- **Framework**: Next.js (React + TypeScript) or Vue/Nuxt.
- **Views**: world map, country dashboard, cabinet decisions, intelligence briefs, timeline replay.
- **Session mode**: browser-first persistence with autosave and resumable sessions.

### Backend
- **API**: GraphQL or REST.
- **Simulation service**: deterministic core + stochastic event layer.
- **Data pipeline**: scheduled ingestion, validation, normalization, provenance tracking.
- **Telemetry**: decision logs for balancing and learning analytics.

### Storage
- Relational DB for canonical data.
- Time-series/event store for simulation progression.
- Cache layer for country and scenario snapshots.

---

## 9) Educational Layer

### Teaching Mechanics
- “Why this matters” cards tied to each indicator shift.
- Optional glossary and context panels per event.
- Debrief compares player path with plausible alternatives.
- Scenario packs aligned with real-world themes (energy security, deterrence, state capacity).

### Assessment Options
- Knowledge checkpoints before/after scenarios.
- Leadership style profile based on repeated decisions.
- Replay and reflection prompts for classrooms.

---

## 10) MVP Roadmap (90 Days)

### Phase 1: Foundations (Weeks 1-3)
- Finalize legal/data sourcing constraints.
- Implement country schema and ingest pipeline.
- Build static web country profile screens with baseline starting-standings metrics.

### Phase 2: Core Simulation (Weeks 4-7)
- Implement indicator engine and policy vectors.
- Ship one complete scenario family (regional crisis).
- Add explainability layer for outcomes.

### Phase 3: Multiplayer-Ready AI World (Weeks 8-10)
- Add AI behavior model for top 20 influential actors.
- Implement alliance/reaction system.
- Tune balance with simulation telemetry.

### Phase 4: MVP Release Candidate (Weeks 11-13)
- Add onboarding + tutorial.
- Add save/load, replay timeline, debrief reports.
- Conduct realism and educational QA tests in desktop/mobile browsers.

---

## 11) Risks & Mitigations
- **Data licensing risk** → legal review + pluggable data provider architecture.
- **Overcomplexity risk** → progressive disclosure UX and adjustable realism modes.
- **Perceived bias risk** → transparent model assumptions and source citations.
- **Performance risk** → server-side simulation + web-optimized payloads.

---

## 12) Success Metrics
- Day-7 retention
- Average scenario completion rate
- Learning gain (pre/post scenario score delta)
- Replay rate per scenario
- User trust score in explanation clarity

