# Design Document: "Shadows Over The Balkans — New Sun of Liberty"

> **Tag System:** Each phase is tagged with one of: `#starter` `#paused` `#resumed` `#completed`
> Change the tag at the start of each work session. Both AI and human developers reference this document.

---

## Mod Context

| Property | Value |
|---|---|
| Name | Shadows Over The Balkans — New Sun of Liberty |
| Internal name | MacTestMod (descriptor.mod) |
| Version | 1.19.2.0 |
| Tags | Alternative History |
| Steam ID | 3759323492 |
| Namespace | `SOTB` (to be created in Phase 0) |
| Mod path | `/home/oddsoul/Desktop/HOI4Studio/Projects/Mods/Shadows over the Balkans - New Sun of Liberty/` |

**Premise:** Alternative history where Macedonia became its own sovereign nation after the Ilinden Uprising (1903) failed militarily but leadership survived. Successful autonomy negotiations with Young Turks (1903–1908). Solun Uprising (1912) secured the capital. Bulgaria invaded twice (1913, 1915) — both repelled. At game start (1936), President Metodija Čento is interim leader after Goce Delchev's 1934 stroke. Ten paths compete for the republic's future.

**Custom Countries:** MAC (Macedonia), THR (Thrace), ERM (Eastern Rumelia — releasable)

---

## Phase Status Overview

| Phase | Status | Started | Completed |
|---|---|---|---|
| **Pre-Phase: Map Setup** | `#completed` | 2026-07-14 | 2026-07-14 |
| **Phase 0: Foundation** | `#completed` | 2026-07-14 | 2026-07-14 |
| **Phase 1: Political Tree** | `#completed` | 2026-07-14 | 2026-07-14 |
| **Phase 2: Military Tree** | `#starter` | — | — |
| **Phase 3: Economic Tree** | `#starter` | — | — |
| **Phase 4: Diplomatic Tree** | `#starter` | — | — |
| **Phase 5: Cultural Heritage Tree** | `#starter` | — | — |
| **Phase 6: Opium GUI & Events** | `#starter` | — | — |
| **Phase 7: AI & Balance** | `#starter` | — | — |

---

## Pre-Phase: Map Setup — `#completed`

> **Completed:** 2026-07-14

### States Created/Modified

| State | ID | Provinces | Owner | Cores |
|---|---|---|---|---|
| Eastern Rumelia (new) | 1089 | 6967, 9888, 9902, 9919 | BUL | BUL + ERM |
| Edirne (overridden) | 341 | 849, 922, 3879, 3893, 6895, 9833, 11842 | GRE | GRE + THR |
| Istanbul (overridden) | 797 | 11829 | TUR | TUR |
| Burgas (overridden) | 211 | 649, 9769, 9783 | BUL | BUL |
| Plovdiv (modified) | 212 | *(unchanged)* | BUL | BUL + ERM |

### Countries Created

| Tag | Name | Ideology | Color | Status |
|---|---|---|---|---|
| ERM | Eastern Rumelia | Non-Aligned | `rgb { 85 170 170 }` | Releasable from BUL |

### Constantinople Naming

- Province 9833 (European side, GRE-owned): default "Constantinople", TUR/GER override "İstanbul"
- Province 11829 (Asian side, TUR-owned): default "İstanbul", GRE override "Constantinople"

### Files Changed (7 created, 5 modified)

**Created:**
- `history/states/1089-Eastern Rumelia.txt`
- `history/states/341-Edirne.txt`
- `history/states/797-Istanbul.txt`
- `history/states/211-Burgas.txt`
- `common/countries/Eastern Rumelia.txt`
- `history/countries/ERM - Eastern Rumelia.txt`

**Modified:**
- `history/states/212-Plovdiv.txt` (added ERM core)
- `common/country_tags/00_countries.txt` (added ERM)
- `common/countries/colors.txt` (added ERM)
- `localisation/english/state_names_l_english.yml` (STATE_1089, STATE_341, STATE_797)
- `localisation/english/victory_points_l_english.yml` (VP 9833, VP 11829)
- `localisation/english/countries_l_english.yml` (ERM entries)

### Still Needed
- ERM flags (12 .tga files — placeholder acceptable)

---

## Phase 0: Foundation — `#starter`

> **Depends on:** Pre-Phase Map Setup ✅

### Files to Create (7)

| File | Purpose |
|---|---|
| `events/MAC_NewsEvents.txt` | Namespace `SOTB` + hidden event infrastructure |
| `common/ideas/MAC_starting_spirits.txt` | 10 national spirits |
| `common/characters/MAC_characters.txt` | 10 character definitions + 3 monarchist candidates |
| `common/scripted_effects/SOTB_effects.txt` | Reusable effects |
| `common/scripted_triggers/SOTB_triggers.txt` | Reusable triggers |
| `localisation/english/SOTB_ideas_l_english.yml` | Spirit localisation |
| `localisation/english/SOTB_characters_l_english.yml` | Character localisation |

### Namespace
```
add_namespace = SOTB
```

### National Spirits (10)

| Spirit Key | Effect | Starting? | Notes |
|---|---|---|---|
| `MAC_founder_watches` | +10% Stability, −10% PP gain | Yes | Delchev — retired, frail, watching. Removed when succession resolves. |
| `MAC_lion_watches` | +5% War Support, +5% Div Recovery | Yes | Sandanski — alive, retired. |
| `MAC_two_betrayals` | GRE opinion −100, BUL opinion −100 | Yes | 1913 & 1915. |
| `MAC_vergina_star` | +5% Stability, +10% justify wargoal time ON us | Yes | Settled heritage. |
| `MAC_delcevism` | +10% PP, +25% drift defense | Yes | Democratic creed. Removed if fascist/communist. |
| `MAC_solun_arsenal` | +10% Factory Output, +5% Dockyard | Yes | Solun industrial base. |
| `MAC_army_of_the_lion` | +5% Division Org, +0.03 daily army XP | Yes | Sandanski's military legacy. |
| `MAC_old_guard_reform` | −5% Military Research, +0.02 army XP | Yes | Resolved by military tree choice. |
| `MAC_throne_of_ohrid` | +5% Stability, −0.02 daily communist | Yes | Church influence. |
| `MAC_poppy` | −2% Consumer Goods, +5% Trade Opinion | Yes | Expandable via opium branch. |

### Characters (10 + 3 monarchist)

| Character | Ideology | Trait |
|---|---|---|
| Goce Delchev | Democratic | `delchevism_founder` |
| Jane Sandanski | Democratic | `lion_of_solun` |
| Metodija Čento | Democratic | `interim_president` (STARTING LEADER) |
| Dimitar Vlahov | Democratic | `imro_reformer` |
| Gjorche Petrov | Democratic | `imro_progressive` |
| Todor Aleksandrov | Non-Aligned | `pragmatic_soldier` |
| Archbishop Dositej II | Non-Aligned | `the_shepherd` |
| Mihajlo Apostolski | Non-Aligned | `military_reformer` |
| Lazar Koliševski | Communist | `the_firebrand` |
| Ivan Mihailov | Fascist | `the_avenger` |
| Prince Harald | Democratic | `constitutional_monarch` (monarchist candidate) |
| Peter II | Non-Aligned | `exiled_king` (monarchist candidate) |
| Prince Philipp | Fascist | `german_prince` (monarchist candidate) |

### Key Scripted Effects

| Effect | Purpose |
|---|---|
| `SOTB_remove_delchev_watches` | Remove Delchev's spirit when path chosen |
| `SOTB_delchev_returns` | Swap to Delchev leader, apply Delčevism buffs |
| `SOTB_sandanski_path` | Swap to Sandanski leader, apply Lion's Path modifiers |
| `SOTB_aleksandrov_takes_power` | Military shift to Non-Aligned |
| `SOTB_mihailov_coup` | Fascist takeover |
| `SOTB_resolve_old_guard` | Remove Old Guard vs Reform spirit |
| `SOTB_set_opium_dependency_<TAG>_<level>` | Track dependency stages (0–4) |
| `SOTB_calculate_opium_leverage` | Sum dependency across nations |
| `SOTB_albania_submit_check` | Conditions for ALB submitting to MAC |

---

## Phase 1: Political Focus Tree — "The Delchev Succession" — `#starter`

> **Depends on:** Phase 0 ✅

### Structure

```
"The Delchev Succession" (70d) — Čento calls the permanent succession
    │
    ├── "Preserve Democracy" (70d) → Democratic Primary → 5 candidates
    ├── "Embrace the Crown" (70d) → Monarchist → 3 candidates
    ├── "Order Above All" (70d) → Aleksandrov OR Archbishop
    ├── "The People's Army" (70d) → Koliševski (Communist)
    └── "The Iron Guard" (70d) → Mihailov (Fascist)
```

### Democratic Candidates (5 paths, ~20 focuses)

| Leader | Path Name | Focuses | Core Mechanic |
|---|---|---|---|
| Goce Delchev | "The Founder Returns" | 4 | Delčevism fulfilled — armed neutrality, cannot join factions |
| Jane Sandanski | "The Lion's Path" | 4 | Defensive resilience — fortifications, "They Will Not Pass" |
| Metodija Čento | "The Manager's Mandate" | 3 | Institutional stability — construction, research |
| Dimitar Vlahov | "The Reformer's Coalition" | 3 | Western alignment — trade, UK/France guarantees |
| Gjorche Petrov | "The Progressive's Dream" | 4 | Social democracy — land reform, workers' rights, anti-fascist |

### Non-Aligned (2 + Monarchist, ~10 focuses)

| Leader | Path Name | Focuses |
|---|---|---|
| Todor Aleksandrov | "The Soldier's Duty" | 3 |
| Archbishop Dositej II | "The Shepherd's Way" | 3 |
| Monarchist (3 candidates) | "The Crown" | 3 + candidate selection |

### Communist & Fascist (1 each, ~8 focuses)

| Leader | Path Name | Focuses |
|---|---|---|
| Lazar Koliševski | "The People's Army" | 4 |
| Ivan Mihailov | "The Iron Guard" | 4 |

**Total: ~35 focuses**

### Key Events

| Event ID | Description |
|---|---|
| `SOTB.100` | "The Crisis Begins" — Čento calls succession |
| `SOTB.200` | "The Democratic Primary" — Player selects candidate |
| `SOTB.300` | "The Old General's Choice" — Mihailov attempts to sway Aleksandrov |
| `SOTB.400` | "The Lion Roars" — Sandanski's intervention (stability < 40%) |
| `SOTB.401` | Delchev's letter (democratic path losing support) |
| `SOTB.500` | Monarchist surge (crisis > 180 days + stability < 30%) |

---

## Phase 2: Military Focus Tree — "The Army of the Lion" — `#starter`

> **Depends on:** Phase 0 ✅

### Structure

```
SHARED TRUNK (5 focuses):
  "The Army's Future" → "Sandanski's Principles" →
  "The Night of Solun" → "National Conscription" →
  "Vardar Engineering Corps"

MUTUALLY EXCLUSIVE SPLIT:
  ┌─ ALEKSANDROV'S PATH (4 focuses): "The Lion's Way"
  │    Infantry/artillery/fortifications/defensive mastery
  └─ APOSTOLSKI'S PATH (4 focuses): "Apostolski's Vision"
       Armor/aviation/mobility/offensive breakthrough

SHARED CAPSTONE (3 focuses):
  "The Arsenal of Solun" → "Macedonian Steel" → "The Lion's Heirs"
```

**Total: ~18 focuses**

### Key Mechanics
- Mutually exclusive focus choice — only one path per game
- Aleksandrov: removes `MAC_old_guard_reform`, applies defensive spirit
- Apostolski: removes `MAC_old_guard_reform`, applies offensive spirit
- Sandanski endorsement event favors Apostolski but stops short of full backing

---

## Phase 3: Economic Focus Tree — "The Balkan Workshop" — `#starter`

> **Depends on:** Phase 0 ✅

### Structure — 5 branches, ~22 focuses

| Branch | Focuses | Centerpiece | Notes |
|---|---|---|---|
| Military Industry | 5 | Solun Arsenal → Balkan Arsenal | Arms factories, artillery foundry |
| Civilian Industry | 5 | Teteks → Balkan Workshop | **"Macedonian Medicine" focus MUTUALLY EXCLUSIVE with Opium** |
| Infrastructure | 4 | Vardar Railway → Aegean Gateway | Roads, rail, Solun port |
| Tobacco | 4 | TKP (Tutunski Kombinat Prilep) | Real company (1873), premium export |
| Opium | 5 | Alkaloid (real company, 1936) | **Mutually exclusive with "Macedonian Medicine"** |

### Real Companies

| Company | Real? | Founded | Role |
|---|---|---|---|
| TKP (Tutunski Kombinat Prilep) | ✅ | 1873 | Tobacco industrial concern |
| Alkaloid | ✅ | 1936 | Pharmaceutical concern — dual-purpose face of opium |
| Teteks | ✅ (alt-history) | — | Textile industrial concern |
| Kratovo-Zletovo Mining | ✅ (deposits) | — | Mining concern |

### Opium Dependency Mechanic

**Stages (per target nation):**
| Stage | Name | Effect on Target | Cost to MAC |
|---|---|---|---|
| 0 | No dependency | — | — |
| 1 | Casual Use | +10 trade opinion | 50 PP |
| 2 | Officer Addiction | −5% war support, +20 trade opinion | 100 PP, −2% CG |
| 3 | Elite Compromised | −10% stability, −10% war support | 150 PP, −3% CG, timed mission |
| 4 | State Dependency | −15% stability, −10% war support, cannot justify on MAC | 200 PP, −5% CG |

- **Greece:** Predisposed — reduced costs, faster progression. Event chain: "The Salonika Habit" → "The Athenian Dens" → "The Ambassador's Observation"
- **Major Powers (UK, France, Germany):** Stage 0–2 only. Benefit from pharma imports. Can be "tipped off" via intelligence.
- **Balkan neighbours:** Stage 0–3. Neutral-positive trade. They know it's aimed at Greece.
- **Opium Diplomacy:** Repeatable decisions — "Flood the [TAG] market" (PP + CG cost, temporary debuff). 365-day cooldown.
- **Petrov + Archbishop:** Publicly denounce, privately tolerate. Do NOT remove poppy spirit.
- **Domestic effects:** External only at this stage. MAC is the dealer, not the addict.

### Opium GUI (Phase 6 — deferred)

Custom GUI using scripted graphs + parliament diagram:
- Dependency tracker (which nations, what stage)
- Opium leverage aggregate score
- Influence decisions accessible from tracker

---

## Phase 4: Diplomatic Focus Tree — "Macedonia Among Nations" — `#starter`

> **Depends on:** Phase 1 (political tree — irredentism gated behind ideology choice)

### Structure — 3 branches, ~16 focuses

#### Balkan League Path (4 focuses)
```
"Court Albania" → "Liberate Montenegro" → "Woo Romania" → "Balkan Federation"
```
Creates `BALKAN_LEAGUE` faction. ALB, MNT (if exists), ROM invited.

#### Great Power Alignment (4 mutually exclusive)
- "Western Alignment" (UK/France guarantees, democratic drift)
- "German Partnership" (trade, fascist drift)
- "Soviet Embrace" (communist drift, Koliševski influence)
- "Eternal Independence" (drift defense, cannot be puppeted)

#### Irredentism — Per-Ideology Methods

| Ideology | Method | Targets | Mechanic |
|---|---|---|---|
| **Fascist (Mihailov)** | Conquest | BUL (1082), GRE (1086), ALB (1087) | Focus grants wargoals directly |
| **Non-Aligned (Aleksandrov/Archbishop)** | Ultimatum | BUL (1082), GRE (1086) | Demand territory — refuse = wargoal |
| **Democratic (Delčev, Sandanski, Čento, Vlahov)** | Balkan Conference | BUL (1082), GRE (1086) | UK/France mediate. Plebiscites. Accept/Cede/Stall. |
| **Democratic (Gjorche Petrov)** | Balkan Solidarity | None | Locks irredentism. Builds defensive faction instead. |
| **Communist (Koliševski)** | Revolution | BUL, GRE, ALB | Support communist partisans. If target flips communist → joins faction, cedes claims. |

### Albania "Shield" Mechanic

- **Focus: "The Shield of Albania"** (70d) — MAC guarantees ALB. +100 opinion. ALB gets `ALB_macedonian_shield` spirit.
- **Italy reaction:** ITA gets decision "Accelerate Albanian Plans" — race for influence.
- **Event: "The Adriatic Question"** — if ITA pressures ALB, ALB chooses: Turn to Solun / Submit to Rome / Stand Alone.
- **Pogradec (1087):** Diplomatic option if ALB joins MAC faction — "territorial adjustment" cedes 1087 in exchange for guarantees.

---

## Phase 5: Cultural Heritage Focus Tree — "Heirs of Alexander" — `#starter`

> **Depends on:** None (ideologically neutral, accessible to all paths)

### Structure — ~10 focuses

```
"The Vergina Museum" → "Alexander's Library" →
"Festival of the Sun" → "The Philip II Monument" →
"The White Tower Restoration" → "Macedonian Alexander Airways" →
"The Vergina Phalanx" → "Macedonia Eternal"
```

All focuses celebrate already-established heritage. No "discovery" — Macedonia already knows who it is.

---

## Phase 6: Opium GUI & Events — `#starter`

> **Depends on:** Phase 3 (economic tree)

### Scope
- Custom GUI: dependency tracker, leverage score, influence decisions
- Uses scripted graphs (Flaxbeard/hoi4-scripted-graphs) + parliament diagram
- Implement basic mechanics FIRST (variables + decisions + events)
- GUI added as polish pass

---

## Phase 7: AI Strategy & Balance — `#starter`

> **Depends on:** All phases complete

### Files to Create

| File | Purpose |
|---|---|
| `common/ai_strategy/MAC_strategy.txt` | MAC AI behavior |
| `common/ai_strategy/THR_strategy.txt` | THR AI behavior |

### MAC AI Weights
- Historical (default): Democratic — 70% Delčev or Čento
- Alt-history: Fascist 15%, Communist 10%, Non-Aligned 5%
- Military: Aleksandrov defensive 60/40 (20/80 if fascist)
- Diplomatic: Balkan League preferred

### ai_will_do
- Every branch-point focus gets weights
- Historical AI follows democratic path
- Fascist/communist AI follows respective paths

---

## File Manifest (Planned)

| Phase | Files | Approx. Lines |
|---|---|---|
| Pre-Phase: Map | 11 files | ~400 |
| 0: Foundation | 7 files | ~1,200 |
| 1: Political | 3 files | ~2,000 |
| 2: Military | 2 files | ~800 |
| 3: Economic | 3 files | ~1,200 |
| 4: Diplomatic | 2 files | ~600 |
| 5: Cultural | 2 files | ~400 |
| 6: Opium GUI | 4 files | ~600 |
| 7: AI | 2 files | ~400 |
| **Total** | **36 files** | **~7,600 lines** |

---

## Decision Log

| Date | Decision | Rationale |
|---|---|---|
| 2026-07-14 | ERM tag = ERM | Avoids RUM (Romania), ERE not standard |
| 2026-07-14 | State 1089 for Eastern Rumelia | Was reserved as "Tamrash" — repurposed |
| 2026-07-14 | Edirne stays as state 341 | Avoids empty state crashes |
| 2026-07-14 | "Macedonian Medicine" as clean industry focus name | Clear identity vs "Clean Industry" |
| 2026-07-14 | Opium external-only at this stage | MAC is dealer, not addict |
| 2026-07-14 | THR content deferred | Focus on MAC core content first |
| 2026-07-14 | Opium GUI deferred to Phase 6 | Basic mechanics first, polish later |
| 2026-07-14 | Petrov does NOT remove poppy spirit | Public denouncement, private tolerance |
| 2026-07-14 | Irredentism gated behind ideology choice | Internal consolidation before territorial ambition |

---

## Open Questions

1. **ERM flags** — need placeholder or actual assets
2. **Delčevism localisation** — "Kemalism + Finnish Sisu" framing — final wording?
3. **Apostolski's political dimension** — should certain factions favor his reforms?
4. **Gjorche Petrov age (71)** — succession mechanic or not a gameplay factor?
5. **Democratic ecosystem depth** — cooperation events between democratic leaders?
