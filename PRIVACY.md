# CareBlocks — Privacy Policy

**Revision 1 — 10 September 2026**
Applies to: CareBlocks — Healthcare Informatics Automator Toolkit, all versions from 1.1.0.
Published by Dr. Somnath V (Creative Mind Blocks). Contact: **cremindb@gmail.com**

---

## In one paragraph

CareBlocks runs entirely on the machine it is installed on. In a default installation it makes **no
outbound network calls at all** — nothing you type, nothing it stores, and nothing about your
organisation leaves the device. Two optional reporting channels exist, both switched off unless you
deliberately turn one on, and neither can carry note content, patient identifiers, or credentials.
This policy states precisely what the software touches, what it keeps, and what the exceptions are —
including the ones that are easy to leave unsaid.

## 1. Who controls the data

**In a default installation, we hold no data about you and cannot.** There is no account, no sign-in,
no server, and no telemetry. Everything CareBlocks records stays in your own user profile on your own
machine, under your organisation's control, not ours.

We become a data controller **only** for the optional usage reports described in §4, and only if you
switch them on or press the button that sends them.

## 2. CareBlocks reads your keystrokes — stated plainly

CareBlocks installs a **global low-level Windows keyboard hook** (`WH_KEYBOARD_LL`). At the Windows
API level this is the same mechanism a keylogger uses, and endpoint-protection software may flag it
on that basis. We state it here rather than let a security team discover it, because what separates
the two is not the mechanism but what is *retained*:

- Characters accumulate in **two rolling buffers, each capped at 80 characters**. One holds the word
  currently being typed and is cleared on Space. The other holds recent typing since the last trigger
  key, and is deliberately **not** cleared on Space — prohibited terms such as "PRE OP" contain a
  space and must still be caught — so it can hold up to 80 characters spanning several words. Both
  are cleared on Tab, Enter, Escape, Delete and the navigation keys.
- **Both exist only in memory.** Neither is ever written to disk. No code path in the application
  writes either of them anywhere.
- Their contents are compared against your organisation's abbreviation workbook. **If nothing
  matches, nothing is recorded** and the characters are discarded.

The hook is necessarily global — it must see typing inside a Citrix-published EHR window. Individual
features can be configured to *act* only while the EHR is in front; that setting controls where
CareBlocks acts, not what the hook observes. We draw that distinction rather than blur it.

## 3. What is stored on your machine, and where

Everything below lives in `%LOCALAPPDATA%\CareBlocks\` in your Windows user profile, except stored
credentials.

| What | Where | Notes |
|---|---|---|
| Settings | `settings.json` | Your configuration. No credentials. |
| Activity Log | `activitylog.db` (SQLite) | See below. |
| Abbreviation workbook | `HIAT_DCW.xlsx` | Your organisation's clinical content. |
| EHR credentials | **Windows Credential Manager** | Never in settings or logs — see §5. |

**The Activity Log records matched abbreviation events, not documentation.** Per event it holds:

| Event | Recorded |
|---|---|
| Restricted term blocked | the matched workbook term, and the workbook's own warning text |
| Abbreviation expanded or misspelling corrected | the matched workbook term, and its workbook replacement |
| Copy, cut, paste or screen capture blocked | the action only — no typed text at all |
| Abbreviation workbook fails to load | the error message returned by the load |

**The property that follows**: every value the log holds *about typing* originates in the
organisation-curated workbook, not in what was typed. It can therefore only ever contain strings that
already exist in that workbook, plus timestamps. Free-text note content and patient identifiers have
no path into it, because an unmatched buffer is never stored.

Text you define privately as a **custom shortcut is deliberately never logged at all.**

**One exception, named rather than left to be found:** the fourth row is not workbook-derived. A
file-load error message typically contains a file path, and a path under a user profile contains the
Windows username. No patient data is involved, but it is the one place the log can hold a string that
did not come from the workbook.

## 4. What can leave your device — both optional, both off by default

| Channel | How it is enabled | What it sends |
|---|---|---|
| **Usage counts** | A setting you switch on. **Off by default.** At most one report per day. | A random installation id, the app version, the Windows version, a date, and eleven totals (abbreviations expanded, warnings raised, copy/paste blocks). **No text of any kind** — the data structure has no field capable of holding text. |
| **Activity Log** | Not a setting. A button you press, confirming **each time**, having been shown what it contains. | The Activity Log as described in §3 — matched terms and their expansions or warning text, plus timestamps. |

**The installation id** is a random value generated once per installation. It is deliberately *not*
derived from your machine name, Windows username, or any hardware identifier. It distinguishes one
installation from another and says nothing about who is using it.

**Processor.** Reports are received by a Google Apps Script web application operated by us, and are
stored in a Google Sheet in our Google Workspace account. Google acts as our processor for that
storage. Nothing is sold, shared with advertisers, or used for profiling.

**If your organisation's position is that none of this may leave your estate**, the default
configuration already satisfies that, and both controls can be verified as off on any machine.

## 5. Credentials

If you choose to store EHR credentials for one-key sign-in, they are held in **Windows Credential
Manager** under the target `CareBlocks:StoredCredential`, using the operating system's own protected
storage. CareBlocks implements no encryption of its own and stores no credential material in its
settings file, its Activity Log, or any report. Credentials are never transmitted anywhere, and can
be removed from inside the app (see §6).

## 6. Retention, and how to delete everything

**We apply no retention period, because we hold nothing to retain.** On your machine, the Activity
Log grows without an **automatic** purge — there is no age-based expiry — so it retains matched
events until you clear it.

You can delete everything at any time, without our involvement:

- **From inside the app** — the Configuration Page's reset control restores factory settings, with
  two separate opt-in switches: *"Also clear stored credentials"* and *"Also clear activity
  history"*. Both are off unless you turn them on, so a reset does not silently destroy either.
- **By hand** — delete the `%LOCALAPPDATA%\CareBlocks\` folder for settings and the Activity Log, and
  remove `CareBlocks:StoredCredential` from Windows Credential Manager.
- **Uninstalling does not remove these** by design, so reinstalling preserves your configuration and
  your organisation's workbook. Delete them explicitly if that is what you want.

Step-by-step instructions are in the *How to Revert to Factory Settings* guide shipped with the
product.

**For usage reports you have already sent us**, tell us your installation id and we will delete the
corresponding rows. The id is not displayed in the app's interface; it is the `InstallId` value in
`%LOCALAPPDATA%\CareBlocks\settings.json`. We ask for it because the data is pseudonymous — we have
no way to link it to you without it, which is the same property that makes it low-risk.

## 7. What CareBlocks never does

- No patient data is transmitted anywhere, under any configuration.
- No advertising, no analytics SDKs, no third-party trackers, no profiling.
- No account, no sign-in, no cloud sync.
- No sale or sharing of data with third parties.
- No automatic update checks or "phone home" beyond the two optional channels in §4.

## 8. Children

CareBlocks is a professional clinical documentation tool. It is not directed at children and we do
not knowingly collect data from anyone under 18.

## 9. Your rights

Because a default installation stores everything locally under your own control, most data-protection
rights — access, rectification, erasure, portability — are exercised directly on your own machine
without needing us. Where we do hold data (§4), contact us at **cremindb@gmail.com** and we will act
on requests under applicable law, including the UAE Personal Data Protection Law, the UK GDPR and the
EU GDPR where they apply.

CareBlocks is a documentation aid, not a decision-maker, and makes no automated decisions producing
legal or similarly significant effects.

## 10. Changes to this policy

Material changes will be published here with a new revision number and date. The revision at the top
of this document is authoritative. If a future version of CareBlocks changes what it collects, this
policy will be updated **before** that version is released.

## 11. Contact

**Dr. Somnath V — Creative Mind Blocks**
Email: **cremindb@gmail.com**

For a fuller technical treatment intended for security and information-governance teams — including
architecture, threat surface, and a candid list of what has *not* yet been done (no code-signing
certificate on the zip build, no SOC 2 or ISO 27001, no formal penetration test) — see the *CareBlocks
Security & Data Handling Brief*, available on request.
