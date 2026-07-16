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
| **Phase 1: Political Tree** | `#resumed` | 2026-07-14 | — |
| **Phase 2: Military Tree** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 3: Economic Tree** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 4: Diplomatic Tree** | `#paused` | 2026-07-15 | 2026-07-15 |
| **Phase 5: Cultural Heritage Tree** | `#paused` | 2026-07-15 | 2026-07-15 |
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

## Phase 1: Political Focus Tree — "The Parliamentary Crisis" — `#resumed`

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
