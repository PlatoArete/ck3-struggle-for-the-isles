# Struggle for the British Isles — Design & Technical Outline

## 0) Mod Scope (MVP)

**Playable focus:** 867 start, the British Isles (Britannia + Isle of Man + Orkney/Hebrides).
**Core pillars:** Struggle system, Religion paths (incl. syncretic & revivals), Culture paths, Military/Levies, Buildings (Burhs/Dúns/Longphorts), Retainers/Court roles, Unity/Legitimacy bar, Confederation endgame.

---

## 1) Struggle Definition

**Path:** `common/struggles/00_british_isles_struggle.txt`

**Phases & flavor**

* **Invasion** → **Consolidation** → **Hegemony**
* Momentum sources (hostile/defensive/conciliatory) tied to your buildings, retainers, and decisions.

**Resolutions (mix & match)**

* Political: *Hegemon of the Isles* (empire) **or** *Confederation of the Isles* (peaceful).
* Religious: *Roman Dominance* / *Insular Resurgence* / *Norse Victorious* / *Old Gods Stir (Goidelic/Brythonic/Hellenic)* / *Syncretic Faith*.
* Cultural: *Melting Pot Culture* **or** *Hegemon’s Divergence*.

**Tech notes**

* Use `possible_resolutions`, `resolution_blockers`, `on_resolution` effects to apply realm modifiers, unlock titles/decisions, and fire capstone events.

---

## 2) Unity of the Isles (Legitimacy–Unity System + UI)

**Scripted value:** `isles_unity_value` (0–100)

**Where**

* Logic: `common/scripted_values/isles_unity_values.txt`
* Monthly updates: `common/scripted_effects/isles_unity_monthly_effects.txt` invoked via on_action.
* On-action: `common/on_actions/zz_isles_unity_on_actions.txt` → `on_monthly_pulse`.

**Bands & effects (realm modifiers)**

* 0–24: `unity_fractured_realm`
* 25–49: `unity_contested_authority`
* 50–74: `unity_recognized_sovereignty`
* 75–100: `unity_of_the_isles`

**Gain/Loss sources (examples)**

* * Unity: phase = Consolidation/Hegemony, great councils, high cultural acceptance, peace streaks, building networks present, religious harmony.
* − Unity: civil wars, excommunication, multi-faith hostility, large culture suppression, raids on Isles realms.

**UI**

* Bar widget reusing struggle/fervor patterns:

  * `gui/isles_unity_bar.gui`
  * `gfx/interface/isles_unity_icons/` (crown/torc/helm/diadem icons)
* Tooltip lists current deltas (scripted loc).

---

## 3) Political Outcomes

### A) Hegemon of the Isles (Empire)

**Files**

* Title: `common/landed_titles/e_hegemon_of_the_isles.txt`
* Decision: `common/decisions/isles_hegemon_decisions.txt` → `proclaim_hegemon_of_the_isles`
* Artifact: `common/artifacts/isles_hegemon_artifacts.txt` (e.g., *Crown of the Eagle*)

**Requirements (typical)**

* Unity ≥ 60, hold ≥ 70% de jure Britannia, Hegemony phase or Struggle resolved.

**Effects**

* Empire creation, realm modifier (+prestige, +control), coronation event.

### B) Confederation of the Isles (High King of High Kings)

**Files**

* Decision: `common/decisions/isles_confederation_decisions.txt` → `form_confederation_of_the_isles`
* System logic: `common/scripted_effects/isles_confederation_effects.txt`
* Membership rules & stability: `common/scripted_triggers/isles_confederation_triggers.txt`
* Events & councils: `events/isles_confederation_events.txt`

**Mechanics**

* Overlord: *High King of High Kings* (prestige/legitimacy gain, weak suzerainty).
* Members: diplomatic obligations, limited internal wars (council votes).
* Stability score; collapse conditions (low unity, war, succession).

---

## 4) Religion Systems

### A) Paths (resolution-gated)

* **Roman Dominance** (Catholic): Papal opinion, church tax/upkeep buffs.
* **Insular Resurgence**: new head (Patriarchate of the Isles), holy order of St. Columba.
* **Norse Victorious**: raiding economy buffs; optional “Sea-Kings’ Syncretism.”
* **Old Gods Stir** (Goidelic / Brythonic / Hellenic): faith definitions + holy sites.
* **Syncretic Faith — “Faith of the Isles”**: tolerant doctrines, ancestor veneration + communion-like tenet, council head (optional).

**Files**

* Faiths: `common/religions/faiths/isles_faiths.txt`
* Doctrines/Tenets (custom): `common/religions/doctrines/00_isles_doctrines.txt`
* Decisions: `common/decisions/isles_faith_decisions.txt`
* Events: `events/isles_religion_events.txt`

**Key decision examples**

* `revive_old_gods_goidelic`
* `revive_old_gods_brythonic`
* `revive_hellenism_insular`
* `forge_new_path_of_faith` (syncretic)

---

## 5) Culture Systems

### A) Cultural Resolutions

* **Melting Pot Culture** (`culture_isles_unified`): ethos: *communal*, pillars mixed; traditions: *maritime commerce*, *cross-cultural court*.
* **Hegemon’s Culture** (divergence): `hegemon_english` / `hegemon_norse` / `hegemon_gaelic` with administrative/imperial tradition.

**Files**

* Cultures & traditions: `common/culture/cultures/isles_cultures.txt`
* Events (hybrid/divergence flavor): `events/isles_culture_events.txt`
* Decisions: `common/decisions/isles_culture_decisions.txt`

---

## 6) Buildings (regional systems)

### A) Burh System (Anglo-Saxon/English)

* Chain: *Timber Burh* → *Stone Burh* → *Royal Burh*
* Adjacent county +fort aura (scripted province modifier)

### B) Dún / Monastic Fort System (Celtic)

* *Hill Dún* → *Stone Dún* → *Royal Dún* (or “Fortified Monastery” variant for Insular/Syncretic)

### C) Longphort System (Norse)

* *Longphort* → *Fortified Longphort* → *Sea-King’s Haven*

**Files**

* `common/buildings/00_isles_buildings.txt`
* Province setup hints: add unique specials (Winchester, Jorvik, Clonmacnoise, Dublin).

**Realm decisions**

* `establish_burghal_system`
* `establish_dun_network`
* `establish_longphort_network`

---

## 7) Troops & Levies

### A) Levy systems (replace base levies via realm modifiers/innovations)

* **Fyrd** (Anglo-Saxon): −levy size, +morale, +reinforcement, home defense.
* **Ceithernn** (Gaelic/Brythonic): −morale, +damage, +pursuit, terrain buffs.
* **Leidang** (Norse): −size, +movement, +siege, +raid loot capacity.

### B) Men-at-Arms

* **Huscarls** (AS/EN): heavy inf; bonus in forts/plains.
* **Gallóglaigh** (Gaelic hybrid/late): heavy shock; rough terrain buffs.
* **Hersir’s Huscarls** (Norse): heavy inf; coastal/river assault buffs.
* **Warriors of the Isles** (melting pot) / **Imperial Guard** (hegemon).

**Files**

* MaA: `common/men_at_arms_types/00_isles_maa.txt`
* Innovations (unlock gates): `common/culture/innovations/00_isles_innovations.txt`
* Modifiers for levy replacements: `common/modifiers/00_isles_levy_modifiers.txt`

---

## 8) Retainers & Court Positions

**Roles**

* **High Reeve** (control + taxes; Burh synergy)
* **Thegn** minor title (levy reinforcement; events)
* **Ollamh / Court Bard** (prestige; acceptance gain)
* **Abbot-Marshal / High Druid** (piety/control for Dúns or Old Gods)
* **Hersir** (raid income; longphort synergy)
* **Law-Speaker** (realm stability, tyranny reduction)
* **Sea-Marshal** (naval speed, raid efficiency)

**Files**

* Court positions: `common/court_positions/00_isles_positions.txt`
* Minor titles via traits/modifiers: `common/traits/00_isles_minor_titles.txt` or `common/minor_titles/…` (if you use a custom system)
* Events: `events/isles_court_events.txt`

---

## 9) Decisions, CBs, & Laws

**Decisions (key)**

* Establish the three building networks
* Form/Proclaim Hegemon / Confederation
* Forge Syncretic Faith / Revive Old Faiths
* Forge Melting-Pot Culture / Impose Hegemon’s Culture
* Council of Unity (remove post-war unrest)

**CBs**

* *Unite the Isles* (Consolidation phase vassalization/conquest CB, prestige-heavy)
* *Hegemon’s Claim* (final phase CB with big legitimacy swing)
* *War of Faiths* (hostile phase religious CB variant)

**Laws**

* *Shire Law* / *Brehon Law* / *Thing Law* → optional merge into *Law of the Isles* on unification.

**Files**

* `common/decisions/…` (grouped by theme)
* `common/casus_belli/00_isles_cb.txt`
* `common/laws/00_isles_laws.txt`

---

## 10) Artifacts & Holy Orders

**Artifacts**

* *Sword of the Isles*, *Crown of Tara*, *Banner of Woden*, *Gospel of St. Columba*, *Stone Crown*, *Seal of the Council*.

**Holy Orders**

* *Order of St. Columba* (Insular)
* *Guardians of the Stones* (Pagan/Syncretic)
* *Companions of the Cross and Hammer* (Syncretic)

**Files**

* `common/artifacts/00_isles_artifacts.txt`
* `common/holy_orders/00_isles_holy_orders.txt`

---

## 11) Events & Flavor

**Packs**

* `events/isles_struggle_events.txt` — phase transitions, catalysts
* `events/isles_unity_events.txt` — thresholds 25/50/75/100
* `events/isles_religion_events.txt` — revivals, synods, syncretic council
* `events/isles_culture_events.txt` — marriages, markets, hybridization
* `events/isles_court_events.txt` — retainers: skald vs. ollamh, reeve corruption, law-speaker debates
* `events/isles_confederation_events.txt` — formation, councils, crises, permanence

---

## 12) Localization & Icons

* Loc: `localization/english/isles_l_english.yml` (keep keys stable)
* Icons: building chains, unity bar states, decisions, artifacts

  * `gfx/interface/icons/isles_*`
  * `gfx/models/*` (optional unique building art later)

---

## 13) Balance & AI

* **AI weights** for each resolution path by culture/faith situation.
* **Unity pacing** tuned so passive play doesn’t auto-win; councils/decisions matter.
* **MaA** balanced against vanilla equivalents (start with −5% to −10% vs. top-tier vanilla to avoid power creep; add synergies situationally).

---

## 14) Compatibility & Performance

* Namespaces prefixed (`isles_*`) to avoid conflicts.
* Avoid overwriting vanilla files; use additive patterns.
* Use on_actions sparingly; batch Unity updates monthly.
* Scope filters to Britannia for triggers to keep costs down.

---

## 15) QA Checklist (quick)

* Start 867 as: Wessex / Dublin / Alba / Gwynedd / Jorvik; verify phase triggers.
* Build 3× Burhs/Dúns/Longphorts: check catalysts and bonuses.
* Form each religious path once; verify doctrines/holy sites/applicable orders.
* Culture: create melting-pot, create hegemon divergence; check innovations.
* Confederation: form with 3+ kings, run 25 years peace, test collapse path.
* Unity: verify bands, tooltips, threshold events, and resolution gating.

---

## 16) Roadmap

### MVP (2–3 features deep)

* Struggle skeleton + phase modifiers
* One political resolution (Hegemon)
* One building chain (Burhs)
* One levy/maa pair (Fyrd/Huscarls)
* Unity value (no custom UI yet; event-only feedback)
* 10–12 core events

### v1.0

* All three building chains + levy/maa systems
* All religious paths (incl. Syncretic + 1 Old Gods variant)
* Cultural resolutions (melting-pot + one hegemon divergence)
* Unity UI bar + thresholds
* Confederation system + councils
* ~40–60 events total

### v2.0 (flavor & polish)

* Remaining Old Gods variants + holy orders
* More artifacts + special buildings (Winchester, Jorvik, Tara)
* Law trees & hybrid government polish
* Custom 2D art for UI/icons; optional building models
* Achievements/scenario bookmarks (optional)

---

## 17) Tiny Sample Snippets (style guide)

**Struggle (header)**

```txt
british_isles_struggle = {
    picture = isles_struggle_bg
    start_date = 867.1.1
    phases = { invasion consolidation hegemony }
    # momentum sources, catalysts, resolutions…
}
```

**Monthly Unity Update (scripted effect)**

```txt
isles_unity_monthly_update = {
    add_to_variable = { name = isles_unity_value value = isles_unity_gain_this_month }
    clamp_variable = { name = isles_unity_value min = 0 max = 100 }
    if = { limit = { check_variable = { isles_unity_value >= 75 } }
      add_realm_modifier = { name = unity_of_the_isles duration = 365 }
    }
}
```

**Decision (sketch)**

```txt
proclaim_hegemon_of_the_isles = {
  picture = decision_isles_hegemon
  desc = proclaim_hegemon_of_the_isles_desc
  is_shown = { has_struggle = british_isles_struggle }
  is_valid = { isles_unity_value >= 60 has_landed_title = k_england OR = { … } }
  effect = { create_title = e_hegemon_of_the_isles hidden_effect = { end_struggle = british_isles_struggle } }
  ai_will_do = { base = 1 modifier = { factor = 3 has_trait = ambitious } }
}
```

---
