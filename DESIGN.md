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

**Premise:** Alternative history where Macedonia became its own sovereign nation after the Ilinden Uprising (1903) failed militarily but leadership survived. Successful autonomy negotiations with Young Turks (1903–1908). Solun Uprising (1912) secured the capital. Bulgaria invaded twice (1913, 1915) — both repelled.

**Leadership Timeline (1913–1936):**
| Leader | Term | Notes |
|---|---|---|
| Goce Delchev | 1913–1928 | Founding President. Resigned via democratic elections, retired but alive and watching. |
| Nikola Karev | 1928–1936 | Hero of Kruševo Republic. Presidency started stable, grew chaotic in later years. |
| Metodija Čento | 1936 (interim) | Caretaker President at game start. Parliament deadlocked — a party won but cannot form government. Repeated failed elections. |

**At game start (1936):** Čento presides over a parliamentary crisis. Fourteen possible leaders across five ideological columns compete to break the deadlock and define Macedonia's future.

**Custom Countries:** MAC (Macedonia), THR (Thrace), ERM (Eastern Rumelia — releasable)

---

## Phase Status Overview

| Phase | Status | Started | Completed |
|---|---|---|---|
| **Pre-Phase: Map Setup** | `#completed` | 2026-07-14 | 2026-07-14 |
| **Phase 0: Foundation** | `#completed` | 2026-07-14 | 2026-07-14 |
| **Phase 1: Political Tree** | `#completed` | 2026-07-14 | 2026-07-16 |
| **Phase 2: Military Tree** | `#completed` | 2026-07-15 | 2026-07-16 |
| **Phase 2b: Icon Audit** | `#completed` | 2026-07-16 | 2026-07-16 |
| **Phase 3: Economic Tree** | `#resumed` | 2026-07-17 | — |
| **Phase 4: Diplomatic Tree** | `#paused` | — | — |
| **Phase 5: Cultural Heritage Tree** | `#paused` | — | — |
| **Phase 5b: Rakija Spirits** | `#paused` | — | — |
| **Phase 5c: Science/Research Tree** | `#paused` | — | — |
| **Phase 6: Opium GUI & Events** | `#paused` | — | — |
| **Phase 7: AI Strategy & Balance** | `#paused` | — | — |
| **Phase 5b: Rakija Spirits** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 6: Opium GUI & Events** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 6b: Scripted GUI** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 6c: Parliament + Pie Chart** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 7: AI & Balance** | `#resumed` | 2026-07-15 | — |

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
| `MAC_founder_watches` | +10% Stability, −10% PP gain | Yes | Delchev — retired since 1928, alive and watching. Removed when succession resolves. |
| `MAC_lion_watches` | +5% War Support, +5% Div Recovery | Yes | Sandanski — alive, retired. |
| `MAC_two_betrayals` | GRE opinion −100, BUL opinion −100 | Yes | 1913 & 1915. |
| `MAC_vergina_star` | +5% Stability, +10% justify wargoal time ON us | Yes | Settled heritage. |
| `MAC_delcevism` | +10% PP, +25% drift defense | Yes | Democratic creed. Removed if fascist/communist. |
| `MAC_solun_arsenal` | +10% Factory Output, +5% Dockyard | Yes | Solun industrial base. |
| `MAC_army_of_the_lion` | +5% Division Org, +0.03 daily army XP | Yes | Sandanski's military legacy. |
| `MAC_old_guard_reform` | −5% Military Research, +0.02 army XP | Yes | Resolved by military tree choice. |
| `MAC_throne_of_ohrid` | +5% Stability, −0.02 daily communist | Yes | Church influence. |
| `MAC_poppy` | −2% Consumer Goods, +5% Trade Opinion | Yes | Expandable via opium branch. |

### Characters (15 total)

| Character | Ideology | Trait | Role |
|---|---|---|---|
| Goce Delchev | Democratic | `delchevism_founder` | Retired founder, alive. Recallable via "Goce's Ideas" path. |
| Jane Sandanski | Democratic | `lion_of_solun` | Military hero, alive and retired. Leads "Sandanski" path. |
| Metodija Čento | Democratic | `interim_president` | **STARTING LEADER (interim).** Also permanent leader via "Republican" path. |
| Nikola Karev | Democratic | `ilinden_veteran` | Former President (1928–1936). Hero of Kruševo Republic. Leads "Ilinden" path. |
| Dimitar Vlahov | Democratic | `imro_reformer` | Advisor/minister. Pro-Western reformer. |
| Gjorche Petrov | Democratic | `imro_progressive` | Advisor/minister. Old IMRO progressive, social democrat. |
| Todor Aleksandrov | Non-Aligned | `pragmatic_soldier` | Military strongman. Leads non-aligned "The Soldier" path. |
| Archbishop Dositej II | Non-Aligned | `the_shepherd` | Head of Orthodox Church. Leads non-aligned "The Shepherd" path. |
| Mihajlo Apostolski | Non-Aligned | `military_reformer` | Military advisor. Leads military tree's offensive branch. |
| Metodi Shatorov | Communist | `bulgarian_comrade` | Pro-Bulgarian Macedonian communist. Leads "Shatorov" communist sub-path. |
| Lazar Koliševski | Communist | `the_firebrand` | Pro-Yugoslav/Comintern communist. Leads "Kolishevski" communist sub-path. |
| Ivan Mihailov | Fascist | `the_avenger` | Ultranationalist revanchist. Leads fascist path. |
| Prince Harald | Democratic | `constitutional_monarch` | Danish prince. Monarchist candidate — constitutional monarchy. |
| Peter II | Non-Aligned | `exiled_king` | Exiled Yugoslav king. Monarchist candidate — Yugoslav alignment. |
| Prince Philipp | Fascist | `german_prince` | German prince (Hesse). Monarchist candidate — Axis alignment. |

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

## Phase 1: Political Focus Tree — "The Parliamentary Crisis" — `#completed`

> **Completed:** 2026-07-16. Kone's ideology path draft integrated. Full tree with 14 leader endpoints across democratic (4), non-aligned (3), monarchist (3), communist (3), and fascist (2) columns.

> **Depends on:** Phase 0 ✅
> **Architecture:** Model B — layered pairwise mutually exclusive forks (vanilla Bulgaria pattern).
> **Last revised:** 2026-07-16 — Kone's ideology path draft integrated.

### Design Philosophy

The tree uses **layered pairwise mutually exclusive (MEX) forks** rather than a flat N-way MEX. Each fork is a meaningful narrative beat. The engine supports flat N-way MEX, but layered 2/3-way forks produce cleaner UI and better AI navigation — exactly as Paradox uses in Bulgaria (BftB), Finland (AAT), and the Netherlands (MtG).

**Parallel event-driven switching:** Hidden events fire based on thresholds (stability, faction popularity, war support, world tension) allowing mid-game ideology/leader changes even after a path is chosen. See "Event-Driven Ideology Switching" below.

### Full Tree Structure

```
                         MAC_parliamentary_crisis (70d)
                        "The Parliamentary Deadlock"
                                  │
                ┌─────────────────┴─────────────────┐
                │                                   │
          MAC_defend_democracy              MAC_restore_order
       "Preserve the Republic"          "Democracy Has Failed"
           (Democratic)                   (Authoritarian)
                │                                   │
                │                       ┌───────────┴───────────┐
                │                       │                       │
                │              MAC_national_salvation    MAC_break_the_system
                │            "A Strong Hand" (Non-Aligned)  "Sweep It Away" (Radical)
                │                       │                       │
                │           ┌───────────┼───────────┐   ┌──────┴──────┐
                │           │           │           │   │             │
                │     MAC_aleksandrov  MAC_church  MAC_crown  MAC_peoples_army  MAC_iron_guard
                │     "The Soldier"  "The Shepherd" "The Crown"  (Communist)    (Fascist)
                │           │           │       │                   │             │
                │           │           │   ┌───┼───┐       ┌──────┼──────┐  ┌───┴───┐
                │           │           │  Harald Peter Philipp  │      │   Direct  Axis
                │           │           │                      Shatorov Kolishevski  War   Align
                │           │           │                          │      │
                │           │           │                          └──KPM─┘
                │           │           │
                │   ┌───────┼───────┐   │
                │   │       │       │   │
                │  Goce  Sandanski Ilinden Republican
                │  (Delchev)       (Karev)  (Čento)
```

### MEX Layers

| Layer | Fork | Type | Options |
|---|---|---|---|
| 1 | `MAC_defend_democracy` vs `MAC_restore_order` | 2-way MEX | Democratic vs Authoritarian |
| 2a | Democratic sub-fork | 4-way MEX | Goce's Ideas / Sandanski / Ilinden / Republican |
| 2b | Authoritarian sub-fork: `MAC_national_salvation` vs `MAC_break_the_system` | 2-way MEX | Non-Aligned vs Radical |
| 3b | Non-Aligned sub-fork | 3-way MEX | Aleksandrov / Archbishop / Monarchist |
| 3c | Radical sub-fork: `MAC_peoples_army` vs `MAC_iron_guard` | 2-way MEX | Communist vs Fascist |
| 4b | Monarchist sub-fork | 3-way MEX | Harald / Peter II / Philipp |
| 4c | Communist sub-fork | 3-way MEX | Shatorov / Kolishevski / KPM |
| 4d | Fascist sub-fork | 2-way MEX | Direct War vs Axis Alignment |

**Total unique endpoints:** 4 (dem) + 1 (Aleks) + 1 (Archbp) + 3 (monarch) + 3 (comm) + 2 (fasc) = **14 possible leaders**

---

### Democratic Column — 4 Leaders (~16 focuses)

> Accessed via `MAC_defend_democracy` → `MAC_democratic_convention` (event SOTB.200 fires, player selects candidate)

| Leader | Path Name | Focuses | Signature Buff | Signature Debuff | Core Mechanic |
|---|---|---|---|---|---|
| Goce Delchev | "Recall the Founder" | 4 | +10% stability, +25% drift defense | −15% PP gain | Delčevism fulfilled. Armed neutrality, cannot join factions. Reluctant founder returns. |
| Jane Sandanski | "The Lion's Path" | 4 | +0.03 daily army XP, +5% division recovery | −10% construction speed | Defensive resilience. Fortifications, "They Will Not Pass." |
| Nikola Karev | "Ilinden Spirit" | 4 | +5% manpower, +5% war support | −10% trade opinion, −5% stability (conservative opposition) | Revolutionary republicanism. Mobilizes the people, alienates old guard. |
| Metodija Čento | "Republican Stewardship" | 4 | +10% PP gain, +5% construction speed | −5% war support | Institutional stability. Čento steps aside peacefully if not chosen. |

**Čento-specific spirits (removed if he leaves office):**
- `MAC_cento_caretaker`: +5% stability, +5% PP (active only while interim)
- `MAC_cento_stewardship`: +10% construction speed (removed if not Republican leader)

**Vlahov & Gjorche Petrov:** Demoted to advisor/minister roles. Available as political advisors under any democratic path.

---

### Non-Aligned Column — 3 Leaders + Monarchist Sub-Branch (~12 focuses)

> Accessed via `MAC_restore_order` → `MAC_national_salvation`

| Leader | Path Name | Focuses | Signature Buff | Signature Debuff |
|---|---|---|---|---|
| Todor Aleksandrov | "The Soldier's Duty" | 3 | +5% division org, +0.02 daily army XP | −10% democratic popularity |
| Archbishop Dositej II | "The Shepherd's Way" | 3 | +10% stability, +5% manpower from church loyalty | −10% war support, −10% research speed |
| Monarchist (3 candidates) | "The Crown" | 4 per candidate | Varies by candidate | Varies by candidate |

---

### Monarchist Sub-Branch — 3 Candidates (4 focuses each)

| Candidate | Focus 1 | Focus 2 | Focus 3 | Capstone |
|---|---|---|---|---|
| **Harald** (Danish/Constitutional) | "The Danish Connection" — +ENG/DEN opinion, trade bonuses | "Constitutional Charter" — +stability, +PP | "The Northern Model" — +research, +construction speed | "The Copenhagen Accord" — +democratic drift, faction with Denmark/Norway if they exist |
| **Peter II** (Yugoslav) | "The Exiled King" — unlock Peter II as advisor, +YUG opinion, spirit `MAC_yugoslav_connection` | "Yugoslav Sympathy" — unlock volunteer/equipment decisions for YUG, +war support | "The Belgrade Compact" — if YUG exists: faction + shared bonuses. If not: claims on South Serbia/Vardar | "The Crown of the South Slavs" — MAC cosmetic name "Macedonian Yugoslavia" (tag stays MAC). +stability. Decisions to core held YUG states. |
| **Philipp** (German/Hessian) | "The Hessian Prince" — +GER opinion, +fascism popularity | "German Patronage" — military advisors, −consumer goods | "The Kaiser's Shadow" — +factory output, +war support | "The Hessian Crown" — join Axis, German equipment licenses |

**Peter II shared-focus hooks (future sub-mod):** If Peter II completes capstone and MAC has Balkan puppets, unlock placeholder decisions (`is_triggered_only = yes`) for shared army commands — activated by the future Yugoslav reunification sub-mod.

**Monarchist narrative:** The parliamentary deadlock makes "return to order via the crown" attractive. Aleksandrov or the Archbishop may propose it, or an external power may back a candidate.

---

### Communist Column — 3 Leaders (~12 focuses)

> Accessed via `MAC_restore_order` → `MAC_break_the_system` → `MAC_peoples_army`

| Leader | Path Name | Focuses | Signature Buff | Signature Debuff | Foreign Patron |
|---|---|---|---|---|---|
| Metodi Shatorov | "The Bulgarian Comrade" | 4 | +10% communist popularity, +0.02 daily communist | −50 YUG opinion, −50 SOV opinion | Bulgaria — autonomous Macedonian communist, anti-Yugoslav |
| Lazar Koliševski | "The Firebrand" | 4 | +0.03 daily army XP (partisan), +5% division recovery | −50 BUL opinion, +10% consumer goods | Yugoslavia / USSR — Comintern loyalist, Tito-aligned |
| KPM | "Party Above All" | 4 | +15% drift defense, +5% stability | −10% PP gain | Independent — collective leadership, party orthodoxy |

**Communist fracture narrative:** The Macedonian communist movement is split three ways — pro-Bulgarian (Shatorov), pro-Yugoslav/Comintern (Kolishevski), and independent party-institutional (KPM). Choosing one purges or sidelines the other two. The USSR may back one faction depending on its own strategic interests.

---

### Fascist Column — 1 Leader, 2 Sub-Paths (~8 focuses)

> Accessed via `MAC_restore_order` → `MAC_break_the_system` → `MAC_iron_guard`

| Sub-Path | Focuses | Signature Buff | Signature Debuff | Foreign Alignment |
|---|---|---|---|---|
| **Direct War** | 4 | +10% war support, −25% justify wargoal time | −15% stability, −30 trade opinion with all neighbours | None — reckless revanchism |
| **Axis Alignment** | 4 | +50 GER opinion, +50 ITA opinion, +10% factory output | −20% stability, −100 BUL opinion | Germany/Italy patronage |

**Mihailov narrative:** Ivan Mihailov leads a fascist ultranationalist movement claiming IMRO's militant legacy. His faction must choose between immediate revenge on Bulgaria or patient alignment with the Axis powers.

---

### Event-Driven Ideology Switching

Parallel to the focus tree, hidden events fire based on threshold checks. These allow mid-game ideology/leader changes even after a focus path is chosen.

| Trigger | Event ID | Effect |
|---|---|---|
| Stability < 25% + war support < 30% + democratic path | `SOTB.600` "The Republic Crumbles" | Option to switch to Aleksandrov (non-aligned) or hold emergency elections |
| Communist popularity > 50% + non-communist path | `SOTB.610` "The Red Surge" | Option to flip to KPM (moderate) or suppress (stability hit, popularity drop) |
| Fascist popularity > 50% + non-fascist path | `SOTB.620` "The Blackshirts March" | Option to flip to Mihailov or call on Sandanski's veterans to resist |
| World tension > 50% + democratic path + stability < 40% | `SOTB.630` "The Founder's Letter" | Delchev writes to the nation — option to recall him even if another democratic faction was chosen |
| Monarchist sub-path + stability < 20% | `SOTB.640` "The King or Chaos" | Archbishop brokers compromise — switch to Church path or double down on monarchy |

### Key Narrative Events

| Event ID | Description |
|---|---|
| `SOTB.100` | "The Parliamentary Deadlock" — Čento addresses the nation. Crisis begins. |
| `SOTB.101` | Hidden event: sets crisis timer, initial stability hit |
| `SOTB.200` | "The Democratic Convention" — Player selects democratic candidate (4 options) |
| `SOTB.300` | "The Old General's Choice" — Mihailov attempts to sway Aleksandrov |
| `SOTB.400` | "The Lion Roars" — Sandanski's intervention when stability < 40% |
| `SOTB.401` | "The Founder's Letter" — Delchev writes to the nation (see SOTB.630 trigger) |
| `SOTB.500` | "The Crown or the Cross" — Monarchist vs Archbishop decision point |
| `SOTB.600` | "The Republic Crumbles" — Emergency event (see threshold table) |
| `SOTB.610` | "The Red Surge" — Communist uprising event |
| `SOTB.620` | "The Blackshirts March" — Fascist coup event |
| `SOTB.630` | "The Founder's Letter" — Delchev recall event |
| `SOTB.640` | "The King or Chaos" — Monarchist crisis event |

### Focus Count Estimate

| Column | Sub-branches | Approx. Focuses |
|---|---|---|
| Democratic | 4 leaders × 4 focuses | ~18 (incl. shared trunk) |
| Non-Aligned | Aleksandrov (3) + Archbishop (3) | ~8 (incl. shared trunk) |
| Monarchist | 3 candidates × 4 focuses | ~14 (incl. shared trunk) |
| Communist | 3 leaders × 4 focuses | ~14 (incl. shared trunk) |
| Fascist | 1 leader × 2 sub-paths × 4 focuses | ~10 (incl. shared trunk) |
| Shared trunk + crisis | 3 focuses | ~3 |
| **Total** | | **~67 focuses** |

---

## Phase 2: Military Focus Tree — "The Army of the Lion" — `#completed`

> **Completed:** 2026-07-16. Full 27-focus tree with shared trunk, Aleksandrov vs Apostolski MEX split, and mountain/air/naval sub-branches. Hidden paths use `allow_branch` gating.

### Structure (27 focuses)

```
SHARED TRUNK (5) — always visible, y=7→11
  "The Army's Future" → "Sandanski's Principles" → "Night of Solun"
    → "National Conscription" → "Vardar Engineering Corps"
                    |
        [GATE: SOTB_succession_resolved]
                    |
    ┌───────────────┴────────────────┐
ALEKSANDROV (5) — defensive      APOSTOLSKI (5) — offensive
  "The Lion's Way"                  "Apostolski's Vision"
    → Fortress Macedonia              → Armored Vanguard
    → Artillery Foundry               → Breakthrough Doctrine
    → They Will Not Pass              → Modern Officer Corps
    → Old Guard's Vindication         → New Model Army
         |                                   |
    [GATE: has doctrine spirit]     [GATE: has doctrine spirit]
         |                                   |
    ┌────┴────────────┬────────────┐
MOUNTAIN (4)       AIR (4)      NAVY (4) — all accessible from either doctrine
```

### Manpower & Equipment
- **+45% recruitable pop factor** across 4 key focuses (+20% Conscription, +15% capstone, +10% Peaks)
- **+22,500 flat manpower**, +500/week from Conscription Act spirit
- **Equipment:** 13,000 infantry eq, 50 artillery, 40 light tanks, 80 fighters, 50 CAS, destroyers, submarines, 80 convoys
- **12 tech bonuses** across infantry, artillery, armor, engineers, mountaineers, fighters, CAS, destroyers, submarines

### Hidden Path Mechanics
- `allow_branch = { has_country_flag = SOTB_succession_resolved }` on doctrine entry focuses
- `allow_branch = { OR = { has_idea = MAC_lions_way has_idea = MAC_apostolski_vision } }` on mountain/air/naval entry focuses
- Children inherit hidden status through prerequisite chain — no repeated `allow_branch` needed

## Phase 2b: Icon Audit — `#completed`

> **Completed:** 2026-07-16. All 84 focus icons + 67 spirit icons replaced with verified vanilla DDS files.
> **Focus icons:** 55 unique, all cross-referenced against `gfx/interface/goals/` DDS files.
> **Spirit icons:** 55 unique, 3 bookmark preview spirits fixed with `GFX_` prefix. 64 remaining spirits have `picture =` values set but may need `GFX_` prefix pass.

---

## Phase 3: Economic Focus Tree — "The Balkan Workshop" — `#resumed`

> **Started:** 2026-07-17. Full 56-focus tree with shared trunk, 5 main branches, opium vs medicine MEX, and ideology-gated industry sub-branches.
> **Depends on:** Phase 0 ✅, Phase 1 ✅ (ideology flags for gating)

### Design Parameters

| Parameter | Value |
|---|---|
| Entry focus | `MAC_balkan_workshop` at x=18, y=0 |
| Entry tone | Hopeful — "Macedonia's hands built Solun. Now they will build an economic miracle." |
| Total focuses | 56 |
| Spelling | Australian English throughout |
| Companies | TKP (1873), Alkaloid (1936), Vardarski Železnici, Pivarnica Skopje (1924), Rudnici Kratovo-Zletovo |
| Gating | Shared trunk always visible. Ideology sub-branches gated by political flags from Phase 1. Opium/Medicine MEX mid-tree. |
| Positioning | Anchor-based: all economic focuses use `relative_position_id = MAC_balkan_workshop` |

### Tree Structure

```
SHARED TRUNK (4) — always visible, x=18, y=0→3
  "The Balkan Workshop" → "Solun Industrial Commission" → "Survey the Vardar" → "The Solun Polytechnic"
                                    │
          ┌─────────┬─────────┬─────┴─────┬─────────┬─────────┐
          │         │         │           │         │         │
    MIL IND (7)  CIV IND (8) INFRA (6)  MINING (6) TOBACCO (6)
    x=15→10     x=21→26    x=27→30     x=31→34   x=35→38
    y=4→10      y=4→11     y=4→9       y=4→9     y=4→9
          │         │
          │         └──[IDEOLOGY GATES at y=12→13]
          │               DEM | NA | MON | COM | FAS
          │               (2)  (2)  (2)   (2)   (1)
          │
          └──[IDEOLOGY MIL GATES at y=12→13]
                                                  │
                                          [OPIUM vs MEDICINE MEX]
                                          x=40→47, y=8→13
                                          Poppy (5) | Medicine (5)
```

### Focus Detail

#### Shared Trunk (4)

| Focus ID | Name | Pos (x,y) | Cost | Key Effects |
|---|---|---|---|---|
| `MAC_balkan_workshop` | "The Balkan Workshop" | 18,0 | 70d | +1 civ 731, +1 infra 731, spirit `MAC_balkan_workshop_spirit` |
| `MAC_solun_industrial_commission` | "The Solun Industrial Commission" | 18,1 | 70d | +2 civ +1 mil 731, upgrades `MAC_solun_arsenal` |
| `MAC_survey_the_vardar` | "Survey the Vardar" | 18,2 | 70d | +100% industry + construction tech, +1 infra 106,1084 |
| `MAC_solun_polytechnic` | "The Solun Polytechnic" | 18,3 | 70d | +1 research slot, +100% synthetic/fuel refining, spirit |

#### Military Industry (7) — x=15→10, y=4→10

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_arms_of_the_republic` | "Arms of the Republic" | +2 mil 731, +1 mil 106, +20 army XP |
| `MAC_solun_arsenal_expansion` | "Expand the Solun Arsenal" | +2 mil 731, +100% infantry/support weapons, +3000 inf eq |
| `MAC_artillery_foundry` | "The Skopje Artillery Foundry" | +1 mil 106, +100% artillery (2 uses), +40 artillery eq |
| `MAC_macedonian_motorisation` | "Macedonian Motorisation" | +100% motorised/mechanised, +1 mil 1084, +100 motorised eq |
| `MAC_armour_initiative` | "The Armour Initiative" | +100% armour (2 uses), +1 mil 731, +30 light tanks |
| `MAC_war_machine` | "The Macedonian War Machine" | +5% mil construction, +10% eq conversion, spirit `MAC_war_machine` |
| `MAC_balkan_arsenal` | "The Balkan Arsenal" | +3 mil (731/106/970), spirit `MAC_balkan_arsenal`, +30 army XP |

#### Civilian Industry (8) — x=21→26, y=4→11

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_textile_mills` | "The Solun Textile Mills" | +2 civ 731, −3% CG |
| `MAC_break_the_ciftlik` | "Break the Çiftlik" | +5% recruitable pop, +5% stability, +1 civ 970 |
| `MAC_reform_tax_code` | "Reform the Tax Code" | +10% PP, +5% stability, +1 civ 106 |
| `MAC_new_guilds` | "The New Guilds" | +10% factory output, +5% construction speed, +100% industry tech |
| `MAC_pivarnica_skopje` | "Pivarnica Skopje" | +1 civ 106, −2% CG, +5% trade opinion, spirit |
| `MAC_consumer_cooperatives` | "Consumer Cooperatives" | −5% CG, +5% stability, +10% trade opinion |
| `MAC_solun_trade_houses` | "The Solun Trade Houses" | +15% trade opinion, +10% PP, +2 civ 731 |
| `MAC_balkan_workshop_fulfilled` | "The Balkan Workshop Fulfilled" | +1 research slot, +5% construction, +5% factory output, spirit |

#### Infrastructure (6) — x=27→30, y=4→9

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_vardar_railways` | "Vardarski Železnici" | +1 infra 106/1084/731, +100% construction tech, spirit |
| `MAC_connect_the_east` | "Connect the East" | +1 infra 1083/1084/1085, +1 civ 1083 |
| `MAC_highland_roads` | "Highland Roads" | +1 infra 970/1086, +1 civ 970, 970 pastoral→rural |
| `MAC_modernise_port_solun` | "Modernise the Port of Solun" | +2 dockyards 731, +1 infra 731, +30 convoys, +2 naval base 731, UK/GRE −10 opinion |
| `MAC_kavala_port` | "The Kavala Port Expansion" | +1 infra 1083, +2 naval base 1083, +1 dockyard 1083, +15 convoys |
| `MAC_aegean_gateway` | "The Aegean Gateway" | +5% dockyard output, +10% trade power, +50 convoys, spirit |

#### Mining & Resources (6) — x=31→34, y=4→9

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_survey_the_mountains` | "Survey the Mountains" | +100% excavation (2 uses), unlock prospecting decisions |
| `MAC_kratovo_zletovo` | "Rudnici Kratovo-Zletovo" | +1 civ 106, +8 steel 106, spirit |
| `MAC_radusa_chromium` | "The Raduša Mines" | +6 chromium 106, +1 civ 106 |
| `MAC_bitola_coal` | "The Bitola Coal Basin" | +8 coal 970, +1 infra 970, +1 civ 970 |
| `MAC_aegean_oil_survey` | "Survey the Aegean Shelf" | +100% synthetic/fuel refining, unlock Prinos prospecting decision (70% chance +8 oil 1083) |
| `MAC_mineral_wealth` | "The Mineral Wealth of Macedonia" | +10% resource gain, +5% factory output, spirit |

#### Tobacco — TKP (6) — x=35→38, y=4→9

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_revive_tkp` | "Revive TKP" | +2 civ 970, spirit `MAC_tkp_monopoly`, unlock tobacco partner decision |
| `MAC_oriental_standard` | "The Oriental Standard" | +10% trade opinion, +5% PP, upgrade spirit to Tier 2 |
| `MAC_prilep_gold` | "Prilep Gold" | +15% trade opinion, +1 civ 970, upgrade spirit to Tier 3 |
| `MAC_tobacco_auction_houses` | "Tobacco Auction Houses" | +1 civ 731, +1 civ 106, +10% trade opinion, +50 PP |
| `MAC_global_tobacco_markets` | "Global Tobacco Markets" | +15% trade opinion, full major power trade, upgrade spirit |
| `MAC_tobacco_barons` | "The Tobacco Barons" | +5% stability, +100 PP, capstone spirit |

#### Opium vs Medicine MEX (12 total)

**Fork point:** `MAC_the_alkaloid_decision` (x=40, y=8) — fires SOTB.800 with MEX choice.

**Poppy Path (5)** — x=41→43, y=9→13:

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_poppy_path` | "The Poppy Path" | MEX with medicine. Upgrade poppy spirit. Unlock opium partner decision. −5% stability, −10 UK/FRA opinion |
| `MAC_expand_poppy_plantations` | "Expand the Poppy Plantations" | +2 civ (970/1084), +5% trade opinion, dependency cap to Stage 3 |
| `MAC_the_powder_trail` | "The Powder Trail" | Event SOTB.801, covert trade routes, −5 stability, +50 PP |
| `MAC_opium_underworld` | "The Opium Underworld" | Upgrade spirit, Stage 4 dependency, −15 UK/FRA/USA opinion, intel bonus on partners |
| `MAC_balkan_opium_empire` | "The Balkan Opium Empire" | Capstone spirit, Stage 5 dependency, unlock "Demand faction join" and "Demand release subject" in trade tracker |

**Medicine Path (5)** — x=45→47, y=9→13:

| Focus ID | Name | Key Effects |
|---|---|---|
| `MAC_medicine_path` | "Macedonian Medicine" | MEX with poppy. Remove poppy spirit. Add `MAC_alkaloid_pharma`. Unlock pharma partner. +10 UK/FRA opinion, +5% stability |
| `MAC_public_health_service` | "The Public Health Service" | +5% stability, +5% recruitable pop, +500 weekly manpower, upgrade spirit |
| `MAC_balkan_pharmacy` | "The Balkan Pharmacy" | +15% trade opinion, +1 civ 106, Tier 2 pharma deals, +10 Balkan opinion. Event: Balkan Health Conference |
| `MAC_medical_diplomacy` | "Medical Diplomacy" | Upgrade spirit, "Send Medical Mission" decision, +5% diplomatic weight |
| `MAC_healers_of_the_balkans` | "The Healers of the Balkans" | +1 research slot, capstone spirit, "Offer Medical Alliance" and "Medical Aid Programme" in trade tracker |

#### Ideology-Gated Industry (9)

**Democratic (2)** — gate: `SOTB_democratic_path`:
- `MAC_cooperative_commonwealth` → `MAC_credit_unions`

**Non-Aligned (2)** — gate: `SOTB_non_aligned_path`:
- `MAC_state_industrial_direction` → `MAC_national_industrial_council`

**Monarchist (2)** — gate: `SOTB_monarchist_path`:
- `MAC_royal_charters` → `MAC_crown_corporations`

**Communist (2)** — gate: `SOTB_communist_path`:
- `MAC_five_year_plan` → `MAC_collectivised_industry`

**Fascist (1)** — gate: `SOTB_fascist_path`:
- `MAC_war_economy`

### New Spirits (22)

| Spirit | Source | Key Modifiers |
|---|---|---|
| `MAC_balkan_workshop_spirit` | Shared trunk | +5% construction speed, +5% factory output |
| `MAC_solun_arsenal_expanded` | Shared trunk | +15% factory output, +10% dockyard output |
| `MAC_polytechnic_spirit` | Shared trunk | +5% research speed |
| `MAC_war_machine` | Mil industry | +10% mil factory output, −5% CG |
| `MAC_balkan_arsenal` | Mil industry capstone | +15% mil factory output, +10% eq conversion, −5% CG |
| `MAC_balkan_workshop_fulfilled` | Civ industry capstone | +10% factory output, +10% construction speed, −5% CG |
| `MAC_pivarnica_skopje` | Civ industry | +5% stability, −2% CG, +5% trade opinion |
| `MAC_vardar_railways_spirit` | Infrastructure | +5% construction speed, +5% supply throughput |
| `MAC_aegean_gateway` | Infrastructure capstone | +10% dockyard output, +10% naval base construction, +5% trade opinion |
| `MAC_kratovo_zletovo_mines` | Mining | +5% resource gain efficiency |
| `MAC_mineral_wealth` | Mining capstone | +15% resource gain efficiency, −5% resource import cost |
| `MAC_tkp_monopoly` → `MAC_tkp_oriental_standard` → `MAC_prilep_gold` → `MAC_tobacco_barons` → `MAC_tobacco_barons_capstone` | Tobacco chain | Trade opinion, CG reduction, PP gain (escalating) |
| `MAC_poppy_cultivation` → `MAC_opium_underworld` → `MAC_opium_empire_capstone` | Poppy path | CG reduction, trade opinion, PP gain (escalating) |
| `MAC_alkaloid_pharma` → `MAC_public_health` → `MAC_medical_diplomacy` → `MAC_healers_capstone` | Medicine path | Research speed, trade opinion, stability, manpower (escalating) |
| `MAC_cooperative_commonwealth` → `MAC_credit_union_capstone` | Democratic | PP gain, stability, CG reduction |
| `MAC_state_direction` → `MAC_industrial_council_capstone` | Non-aligned | Factory output, construction speed |
| `MAC_royal_charters` → `MAC_crown_corporations_capstone` | Monarchist | Trade opinion, PP, CG reduction, stability |
| `MAC_five_year_plan` → `MAC_collectivised_capstone` | Communist | Construction speed, factory output, CG reduction (−stability) |
| `MAC_war_economy_capstone` | Fascist | Mil construction, factory output, CG reduction, war support |

### New/Updated Events

| Event | Purpose |
|---|---|
| `SOTB.800` (update) | Alkaloid Founded — now includes MEX choice between poppy/medicine |
| `SOTB.801` (update) | The Powder Trail Opens — updated for dependency mechanic |
| `SOTB.802` (new) | The Balkan Health Conference — medicine path mid-point |
| `SOTB.803` (new) | The Macedonian Demand — opium Stage 5: demand faction join |
| `SOTB.804` (new) | The Macedonian Demand — opium Stage 5: demand release subject |
| `SOTB.805` (new) | The Macedonian Embrace — target accepts faction join demand |
| `SOTB.806` (new) | The Macedonian Hand — released subject gratitude event |
| `SOTB.807` (new) | Trade Collapse — target refuses demand, gets severe debuff |
| `SOTB.808` (new) | The British Note — UK protests port modernisation (mild) |
| `SOTB.809` (new) | Name Your Alliance — player names new faction |

### Decision Log (Phase 3)

| Date | Decision | Rationale |
|---|---|---|
| 2026-07-17 | Economic tree entry: "The Balkan Workshop" at x=18, y=0 | Far right, parallel to political tree. Hopeful tone — vision, not crisis. |
| 2026-07-17 | Australian English for entire mod | Per instruction: modernise, colour, defence, labour, centre, programme. |
| 2026-07-17 | Companies: TKP, Alkaloid, Vardarski Železnici, Pivarnica Skopje, Rudnici Kratovo-Zletovo | Macedonian names only. No French/Franco names. Teteks removed (founded 1951). |
| 2026-07-17 | Port focus: "Modernise the Port of Solun" with mild UK/GRE penalty (−10) | Frustration, not hostility. Modernisation, not reclamation. |
| 2026-07-17 | Opium vs Medicine MEX as central economic fork | Poppy = criminal influence + leverage. Medicine = legitimate soft power + research. Both end at Stage 5 trade tracker actions. |
| 2026-07-17 | Fascist industry: 1 focus | Fascists get efficiency, not breadth. The war economy IS the point. |
| 2026-07-17 | Monarchist industry: separate from non-aligned | 5 ideology paths, not 4. Monarchists get Royal Charters flavour. |
| 2026-07-17 | Infrastructure: on-map building + state category upgrades | Player sees Macedonia physically develop. Pastoral → rural via event. |
| 2026-07-17 | Aegean oil: late-game prospecting decision with 70% success | Plausible ahistorical. Real Prinos field off Thasos. Risk/reward. |
| 2026-07-17 | Anchor-based positioning for all economic focuses | Avoids the compounding offset issue (LR-0019). `MAC_balkan_workshop` is the anchor. |

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
- Historical (default): Democratic — 40% Goce's Ideas, 30% Republican (Čento), 15% Sandanski, 15% Ilinden (Karev)
- Alt-history: Fascist 15%, Communist 10%, Non-Aligned 5%, Monarchist 5%
- Military: Aleksandrov defensive 60/40 (20/80 if fascist)
- Diplomatic: Balkan League preferred
- Communist AI: 50% KPM (moderate), 30% Kolishevski (Comintern), 20% Shatorov (independent)

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
| 1: Political | 3 files | ~3,500 |
| 2: Military | 2 files | ~800 |
| 3: Economic | 3 files | ~1,200 |
| 4: Diplomatic | 2 files | ~600 |
| 5: Cultural | 2 files | ~400 |
| 6: Opium GUI | 4 files | ~600 |
| 7: AI | 2 files | ~400 |
| **Total** | **36 files** | **~9,100 lines** |

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
| 2026-07-16 | Leadership timeline revised: Delchev 1913–1928 → Karev 1928–1936 → Čento 1936 | Kone's design: Delchev resigned democratically, Karev bridges founding era to crisis |
| 2026-07-16 | Opening crisis changed to parliamentary deadlock | More realistic than personal health crisis. Produces factional + ideological deadlock layers. |
| 2026-07-16 | Tree architecture: Model B layered pairwise MEX (vanilla Bulgaria pattern) | Cleaner UI, better AI navigation than flat N-way MEX. 14 leader endpoints across 5 columns. |
| 2026-07-16 | Kone's ideology draft adopted: Goce's Ideas / Sandanski / Ilinden / Republican (democratic), Shatorov/Kolishevski/KPM (communist) | Replaces old 5-candidate democratic + single communist design. Vlahov & Petrov demoted to advisors. |
| 2026-07-16 | Archbishop Dositej II restored as non-aligned alternative | "The Shepherd's Way" — clerical path. Church as political force. |
| 2026-07-16 | Monarchist path: 3 candidates, 4 focuses each, fifth column under non-aligned | Harald (Danish/constitutional), Peter II (Yugoslav/MAC-only, no tag switch), Philipp (German/Axis) |
| 2026-07-16 | Shatorov added as communist figure | Historically grounded — real Macedonian communist, pro-Bulgarian, anti-Yugoslav. Creates communist 3-way split. |
| 2026-07-16 | Peter II path scoped to MAC-only | Yugoslav reunification deferred to future sub-mod. MAC gets Yugoslav-themed spirits/decisions without tag switch. |
| 2026-07-16 | Event-driven ideology switching via thresholds | Parallel system. Stability, faction popularity, war support, world tension gates. Finland-vanilla pattern. |
| 2026-07-16 | Phase 1 focus count: ~67 (up from ~35) | Reflects 14 leaders × 4 focuses each + shared trunks + crisis events. |
| 2026-07-16 | Military tree: full rework, 27 focuses | Shared trunk (5) always visible. Aleksandrov vs Apostolski MEX split (5 each) gated behind `SOTB_succession_resolved` via `allow_branch`. Mountain/Air/Naval branches (4 each) accessible from either doctrine path. +45% recruitable pop factor, 12 tech bonuses. |
| 2026-07-16 | Icon audit: 84 focus + 67 spirit icons replaced | All verified against vanilla DDS files. 55 unique focus icons, 55 unique spirit pictures. 3 bookmark preview spirits fixed with `GFX_` prefix. 4 broken GFX names discovered and replaced (`GFX_goal_generic_navy` etc don't exist). |
| 2026-07-16 | `major = yes` added to MAC country history | MAC now appears in major powers row on country selection screen instead of "Other countries". |
| 2026-07-16 | Bookmark: desc condensed, crown focus removed, `MAC_the_crown` dropped | `MAC_SOTB_BOOKMARK_DESC` from 20 lines → 4. Preview focuses reduced to 3 (parliamentary crisis + democratic + authoritarian). |

---

## Open Questions

1. **ERM flags** — need placeholder or actual assets
2. **Delčevism localisation** — "Kemalism + Finnish Sisu" framing — final wording?
3. **Apostolski's political dimension** — should certain factions favor his military reforms?
4. **Gjorche Petrov age (71)** — advisor role only, or any active political involvement?
5. **Democratic ecosystem depth** — cooperation events between democratic leaders?
6. **Shatorov localisation** — flesh out his ideological line vs Kolishevski
7. **KPM collective leadership** — who are the named figures on the KPM central committee?
8. **Harald & Philipp paths** — currently placeholders. Flesh out when sub-mod scope defined.
9. **Monarchist narrative hook** — who proposes the crown? Aleksandrov? Archbishop? External power?
10. **Shared-focus sub-mod hooks** — placeholder decisions for Peter II's Yugoslav path deferred.
