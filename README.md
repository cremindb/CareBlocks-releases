# CareBlocks - Healthcare Informatics Automator Toolkit

*Created by [Creative Mind Blocks](mailto:cremindb@gmail.com) · Author: Dr. Somnath V*

> **This is a complete, ready-to-run package.** The download includes the compiled app, a fully
> populated abbreviation workbook, and the full documentation/support suite - extract the zip and
> every feature described below works immediately, with no separate setup, licensing key, or
> content to build yourself.

A Windows desktop tool for informatics specialists documenting in an EHR/Citrix workflow: expands
clinical abbreviations while charting, warns on dangerous/do-not-use terms and disallowed symbols,
blocks copy/cut/paste/print of patient data leaving the EHR window, and injects saved credentials
into login screens with a single hotkey.

Runs entirely on the specialist's own Windows machine, one specialist per Windows login, starting
automatically at sign-in.

## Download

Download the latest release from the [Releases page](https://github.com/cremindb/CareBlocks-releases/releases).

Each release is a single `CareBlocks-vX.Y.Z-win-x64.zip` containing everything needed to run the app -
no installer, no separate .NET runtime download.

## System requirements

- Windows 10 or 11, 64-bit.
- The [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/#download-section)
  (the "Evergreen Bootstrapper" is the right download). This is already installed on most modern
  Windows 10/11 machines with Edge, but isn't guaranteed - if it's missing, the app will show a clear
  message on startup rather than failing silently.
- No administrator rights required to install or run.

## Install & run

1. Download the zip from [Releases](https://github.com/cremindb/CareBlocks-releases/releases) and extract it
   to any folder.
2. Run `CareBlocks.App.exe`.
3. **You will likely see a "Windows protected your PC" SmartScreen warning.** This is expected - the
   exe isn't code-signed yet (see [Known limitations](#known-limitations) below). Click **More info**,
   then **Run anyway**.
4. On first launch you'll see a short welcome popup, then the app runs quietly in the system tray.

## First-run setup

Press **F1** from anywhere to open the Configuration Page - this is where you point the app at your
abbreviation workbook, enter credentials, and adjust hotkeys/guarding. See the in-app Knowledge Base
(also reachable from the Configuration Page) for a full walkthrough of every setting.

A complete, ready-to-use abbreviation workbook, `HIAT_DCW.xlsx`, is included in this download, sitting
alongside `CareBlocks.App.exe`. On the Abbreviation Stacks card, click **Change…** and select it to
get started immediately - no need to build your own workbook before trying the tool.

## Training videos

All 6 videos below are also collected as a real YouTube Course,
["Learn all about CareBlocks Healthcare Automation Toolkit"](https://www.youtube.com/playlist?list=PLbiUc-Je5i7Q).

0. [Course Introduction](https://www.youtube.com/watch?v=y3VcV7ajYkw) - meet the instructor and get
   a roadmap of everything the course covers.
1. [Part 1 — Getting Started](https://youtu.be/D8RopjJQLvU) - install, find CareBlocks in your tray,
   and a tour of all 4 tabs.
2. [Part 2 — Content and Rules](https://youtu.be/Xnk9WB6rj3s) - abbreviation expansion and
   dangerous-term safety.
3. [Part 3 — Access and Guarding](https://youtu.be/D9Jrg826Qws) - credentials and clipboard/print
   protection.
4. [Part 4 — System and Support](https://youtu.be/hMGq2sKx-CE) - Activity Log, metrics, and the
   Knowledge Base.
5. [Part 5 — Dashboard](https://youtu.be/bcgNco9MhAs) - a visual look at everything CareBlocks has
   caught.

## Known limitations

This is a demo-stage release, not a finished commercial product. Worth knowing before relying on it:

- The exe is **not code-signed** - expect a SmartScreen warning on first run, and some corporate
  antivirus/EDR software may flag or quarantine it (a global keyboard hook plus credential handling
  is exactly the shape of behavior AV tools are built to watch for).
- **No auto-update** - checking for and installing a newer version is manual (re-download and
  re-extract).
- The clipboard/print guard only intercepts specific keyboard shortcuts (`Ctrl+C/X/V/P`, Print Screen,
  `Win+Shift+S`) - a menu-triggered copy/paste, or a separately-launched screenshot tool, isn't caught.
- The Activity Log is stored locally as unencrypted SQLite - readable by anything with access to your
  Windows profile.
- No settings backup/versioning beyond what's already in the app.

## Security & privacy

- **No outbound network calls, anywhere in the app.** Everything the app shows (the Configuration
  Page, popups, help content) is loaded from files bundled with the app itself - never a remote
  server. This is a deliberate, standing requirement for a tool that runs directly alongside an EHR.
- Credentials are stored in **Windows Credential Manager**, never written to a settings file or the
  Activity Log.
- The abbreviation workbook, hotkey map, and feature toggles live in a local settings file under
  `%LocalAppData%\CareBlocks\` - never uploaded anywhere.

## Regulatory & clinical-safety alignment

- **Joint Commission / JCI**: the Do Not Use, Dangerous Abbreviation, and Symbols stacks give your
  organization a real-time enforcement mechanism for its own restricted-terminology policy, built to
  support and align with the abbreviation-safety intent behind Joint Commission Standard IM.02.02.01
  and Joint Commission International (JCI) Standard MOI.4.
- **HIPAA**: no outbound network calls, clipboard/print guarding, and Credential Manager-only
  credential storage are technical safeguards that support your organization's HIPAA compliance
  efforts, aligned with the HIPAA Security Rule's technical-safeguard categories (45 CFR § 164.312).
- CareBlocks is not itself HIPAA-certified or JCI-accredited, and using it does not, by itself, make
  your organization compliant with either - that remains your organization's responsibility.
- See [COMPLIANCE.md](COMPLIANCE.md) for the full explanation and reference citations, and
  [LICENSE](LICENSE) for the clinical-use and liability terms.

## Support / feedback

The Configuration Page (`F1`) has a **Feedback** card with a QR code and a "report an issue / suggest
an improvement" form, and a **WhatsApp Group** QR code for quicker back-and-forth. Both are the
fastest way to reach the team.

## License

CareBlocks is proprietary software, free to use for personal/internal purposes but not open-source -
see [LICENSE](LICENSE) for the full terms. In short: you're welcome to install and use it; please
contact [cremindb@gmail.com](mailto:cremindb@gmail.com) before redistributing, modifying, or
republishing it. Neither CareBlocks, Creative Mind Blocks, nor its author, Dr. Somnath V, bears any
legal responsibility for your use of the tool - see [LICENSE](LICENSE) and
[COMPLIANCE.md](COMPLIANCE.md) for the full terms.

---

© 2026 Creative Mind Blocks
