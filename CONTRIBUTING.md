# Contributing to **Struggle for the British Isles**

Thanks for helping build this CK3 mod! This guide explains how to set up your environment, our coding standards, and the review process so contributions stay consistent and safe.

---

## 1) Quick Start

1. **Clone** the repo and open it in VS Code.
2. Install **CK3Tiger** (VS Code extension) and point it to:

   * Game directory (CK3 install)
   * Mod directory (this repo)
3. Ensure these files exist at repo root:

   * `.editorconfig`, `.gitattributes`, `.gitignore`, `.vscode/`
   * `descriptor.mod`
4. (Optional but recommended) **Symlink** your repo into your Paradox mods folder so changes load in-game without copying.

---

## 2) Environment

* **Editor:** VS Code (workspace settings provided in `.vscode/settings.json`).
* **Linting/Format:**

  * `.editorconfig` enforces UTF-8, LF, spaces=2.
  * `.gitattributes` normalizes line endings and treats binaries correctly.
* **Validation:** Use **CK3Tiger** (syntax, scopes, triggers/effects).

  * Command Palette → *CK3 Tiger: Reload Database* after adding new scripted keys.

---

## 3) Folder Layout (authoritative)

```
common/
  struggles/
  decisions/
  buildings/
  religions/
  culture/
  men_at_arms_types/
  court_positions/
  scripted_effects/
  scripted_triggers/
  scripted_values/
  on_actions/
  modifiers/
  laws/
events/
gfx/interface/{icons,gui}/
localization/english/
defines/
```

> Add stub files if you create new folders so Git tracks them.

---

## 4) Naming & Namespace Rules (HARD)

* **All keys, files, and images MUST be prefixed with `isles_`.**
  Examples:

  * Events: `isles.unity.0001`
  * Decisions: `isles_confederation_form`
  * Modifiers: `isles_unity_of_the_isles`
  * Scripted effects/values: `isles_unity_monthly_update`, `isles_unity_value`
  * Buildings: `isles_building_burh_lvl_1`
  * Men-at-arms: `isles_maa_huscarls`

* **Additive, not replacing:** Do **not** overwrite vanilla files. If you must, discuss in an issue first.

---

## 5) Event ID & File Conventions

* Event IDs: `isles.<domain>.<####>`

  * `isles.unity.0001`, `isles.confed.1005`, `isles.religion.0203`, etc.
* Reserve ranges per domain:

  * `isles.unity.0001–0999` (Unity system)
  * `isles.struggle.1000–1999` (Struggle flow/catalysts)
  * `isles.confed.2000–2999` (Confederation)
  * `isles.culture.3000–3999`
  * `isles.religion.4000–4999`
  * `isles.military.5000–5999`
* One feature per file:

  * `events/isles_unity_events.txt`
  * `common/decisions/00_isles_decisions.txt`, etc.

---

## 6) Localization

* Every script key that’s player-facing **must** have English loc:

  * File: `localization/english/isles_l_english.yml`
* Use UTF-8 (no BOM), LF line endings.
* Provide:

  * `key:0 "Title"`
  * `key_desc:0 "Description"`
  * `key_tt:0 "Tooltip text"` (when applicable)
* Keep placeholders if needed:
  `isles_todo_key:0 "TODO: $KEY$"`

---

## 7) Coding Style

* Indentation: **2 spaces**; no tabs.
* Keep lines <= 120 chars where practical.
* Comment “why”, not “what”:

  ```txt
  # WHY: this buff offsets early Invasion-phase disunity
  add_realm_modifier = { name = isles_unity_fractured_realm duration = 365 }
  ```
* Prefer **scripted_effects** / **scripted_triggers** for reused logic.
* Scope to Britannia where possible for performance.

---

## 8) Features: Common Patterns

### Struggle (skeleton)

* File: `common/struggles/00_isles_struggle.txt`
* Phases: invasion → consolidation → hegemony
* Resolutions: hegemon | confederation + religion + culture paths

### Unity System

* Values: `common/scripted_values/00_isles_values.txt` → `isles_unity_value`
* Effects: `common/scripted_effects/00_isles_effects.txt` → `isles_unity_monthly_update`
* On-action hook: `common/on_actions/zz_isles_unity_on_actions.txt` → `on_monthly_pulse`

### Buildings

* `common/buildings/00_isles_buildings.txt`
* Chains: Burhs / Dúns / Longphorts with culture/terrain gates

### Levies / MaA

* Levies via realm modifiers (or innovations) under `common/modifiers/00_isles_levies.txt`
* MaA: `common/men_at_arms_types/00_isles_maa.txt`

### Decisions

* `common/decisions/00_isles_decisions.txt`
  (Form Hegemon, Form Confederation, Establish networks, Revivals, Syncretic faith, Culture outcomes)

---

## 9) Testing & Validation Checklist

Before opening a PR:

1. **CK3Tiger** shows no errors/squiggles in changed files.
2. All new keys have **English localization**.
3. No vanilla files modified or deleted.
4. New content uses **`isles_`** prefix.
5. Feature loads in-game:

   * Launch CK3 → enable mod in launcher.
   * Smoke test: open relevant UI (Struggle, Decisions, etc.) and confirm no error logs.
6. Performance: no heavy loops or broad `any_*` scans without scope filters.

---

## 10) Branching, Commits, PRs

* Branch off `dev`:

  ```
  git checkout -b feature/isles-<short-name>
  ```
* Commits: concise, imperative, with scope:

  * `feat(unity): add 50/75/100 threshold events`
  * `fix(buildings): correct burh level triggers`
* Open a PR into `dev` with:

  * Summary of changes
  * Screenshots/log snippets (if UI/visible feature)
  * Checklist ticked (below)

**PR Checklist**

* [ ] Namespaced (`isles_`)
* [ ] Loc added
* [ ] CK3Tiger clean
* [ ] In-game smoke test
* [ ] No vanilla overwrites
* [ ] Docs updated (README/design if needed)

We merge `dev → main` for tagged releases.

---

## 11) Compatibility & Performance

* Avoid `replace_path` unless absolutely necessary (discuss first).
* Keep triggers tight (filter to region/culture/faith where possible).
* Prefer **province/character scopes** over global `any_*` where feasible.

---

## 12) Running the Mod (Launcher)

If you want to test in-game without copying:

* Create a symlink from your Paradox mods folder to this repo.
* Add a `.mod` stub:

  ```txt
  name="Struggle for the British Isles"
  path="mod/ck3-struggle-for-the-isles"
  supported_version="1.12.*"
  ```

(We keep a quick script in the issue thread if you need it.)

---

## 13) Issue Reporting

Please include:

* Game version, mod commit hash
* Repro steps (numbered)
* Save file or minimal script snippet
* `error.log` excerpt (if available)

---

## 14) Code of Conduct

Be kind. Debate ideas, not people. No harassment or discriminatory language.

---

### Thank you!

Your contributions help turn this into a DLC-grade experience. If you’re unsure how to structure a new feature, open a **Draft PR** or an **Issue** and we’ll sketch it together.
