# CareBlocks — Regulatory Alignment, Clinical Use & Liability

This document explains how CareBlocks relates to Joint Commission / Joint Commission International
(JCI) and HIPAA requirements, and states the terms under which the tool is provided. It is referenced
from [README.md](README.md) and [LICENSE](LICENSE) rather than duplicated in full there.

CareBlocks is created by Creative Mind Blocks; the tool's author is Dr. Somnath V.

## CareBlocks is a clinical documentation aid, not a clinical decision-maker

CareBlocks assists a specialist while charting — it does not diagnose, treat, or make care
decisions, and it does not verify the clinical accuracy of anything it expands, blocks, or warns
about beyond matching against the abbreviation list your organization has configured. Every
expansion, warning, and blocked action must be reviewed by the specialist before it becomes part of
the medical record. Final clinical judgment, and full responsibility for the accuracy and
completeness of the resulting documentation, rest entirely with the user.

## Joint Commission / JCI alignment

Ambiguous and error-prone abbreviations are a recognized patient-safety risk. In the United States,
the Joint Commission's "Do Not Use" list of abbreviations was approved in 2002 as part of National
Patient Safety Goal 2 and folded in 2010 into the Information Management chapter as **Standard
IM.02.02.01** (Elements of Performance 2 and 3) — created specifically because terms like "U" for
units, "QD" for daily, or a trailing zero have caused real medication and documentation errors.
Joint Commission International (JCI) carries the same requirement internationally under its own
**Management of Information (MOI) chapter, Standard MOI.4**, which requires a hospital to standardize
and enforce the use of approved symbols, abbreviations, and codes hospital-wide. (JCI's exact
standard numbering has shifted across manual editions — confirm the current citation against your
organization's own JCI standards manual edition; see References below.)

CareBlocks' **Do Not Use**, **Dangerous Abbreviation**, and **Symbols** stacks give your organization
a real-time enforcement mechanism for whatever restricted-terminology policy it has defined: a
specialist typing a listed term is warned and the term is removed before it reaches the note, and
every occurrence is recorded in the Activity Log. This is built to **support and align with** the
abbreviation-safety intent behind these Joint Commission / JCI standards — it is not itself a Joint
Commission or JCI certification, and it does not substitute for your organization's own accreditation
program, clinical governance, or the accuracy of the abbreviation content it's configured with. The
actual list of restricted terms is entirely defined by the workbook your organization supplies and
maintains; CareBlocks enforces whatever that workbook contains.

## HIPAA alignment

The HIPAA Security Rule (45 CFR § 164.312) requires covered entities to implement technical
safeguards across several categories — including access control, transmission security, and audit
controls — to protect electronic PHI. CareBlocks implements specific technical controls that map onto
those categories:

- **No outbound network calls, anywhere in the app.** Every screen CareBlocks shows is loaded from
  files bundled with the app itself. PHI visible in the EHR is never transmitted anywhere by this
  tool — there is no server, no telemetry, and no update-check ping.
- **Clipboard and print/screen-capture guarding.** Configurable blocking of copy/cut/paste
  (`Ctrl+C/X/V`) and print/screen-capture (`Ctrl+P`, Print Screen, `Win+Shift+S`) reduces the ways
  EHR content can leave the screen through this workstation.
- **Credentials never stored in plaintext.** Saved credentials live in Windows Credential Manager,
  never in a settings file or the Activity Log.

These are real, verifiable technical safeguards that **support your organization's HIPAA compliance
efforts** — but HIPAA compliance itself is a property of your organization's complete administrative,
physical, and technical safeguard program (policies, workforce training, risk assessments, Business
Associate Agreements, breach procedures), not something a single piece of software can hold on its
own. CareBlocks is one technical control within that program, not a certification and not a
substitute for it. Note also that the Activity Log itself is stored locally as unencrypted SQLite,
readable by anything with access to the Windows profile it runs under — worth factoring into your
organization's own risk assessment.

## What CareBlocks does not claim

- CareBlocks is not itself HIPAA-certified, JCI-accredited, or FDA-cleared — no such certification
  exists for a tool like this, and none is claimed.
- Installing and using CareBlocks does not, by itself, make your organization compliant with HIPAA,
  Joint Commission/JCI, or any other regulatory or accreditation standard. That responsibility
  remains entirely with your organization.
- CareBlocks does not review, validate, or guarantee the clinical accuracy of the abbreviation
  content your organization configures it with.

## Liability

CareBlocks is provided free of charge, as-is, for personal or internal organizational use — see
[LICENSE](LICENSE) for the full legal terms.

CareBlocks is designed to honor HIPAA data privacy and to reduce documentation errors while charting
— catching dangerous abbreviations, mis-typed terms, and restricted symbols before they reach the
medical record, and guarding against PHI leaving the EHR screen. Any data loss or data alteration is
contrary to the tool's design intent, not an accepted or expected outcome of its normal use.

Notwithstanding that intent, neither CareBlocks, Creative Mind Blocks (its creator), nor Dr. Somnath V
(its author) accepts any legal liability of any kind — including for data loss, data alteration, a
missed or incorrect abbreviation expansion or warning, or any resulting medical-legal complication
(MLC) — arising from use of CareBlocks. The user bears full responsibility for reviewing, verifying,
and accepting anything CareBlocks inserts, corrects, or flags before it becomes part of the medical
record.

## Contact

Questions about this document, or about CareBlocks' regulatory positioning generally: contact
Creative Mind Blocks at cremindb@gmail.com, or use the in-app Feedback card (Configuration Page →
"Content and rules" tab).

## References

- [Do Not Use List / Prohibited Abbreviations — Joint Commission](https://www.jointcommission.org/en-us/knowledge-library/support-center/standards-interpretation/do-not-use-list-of-abbreviations)
- [International Patient Safety Goals — Joint Commission International](https://www.jointcommission.org/en/standards/international-patient-safety-goals)
- [JCI Standards Manuals — Joint Commission International](https://www.jointcommission.org/en/standards/standards-manuals)
- [Summary of the HIPAA Security Rule — U.S. Department of Health and Human Services](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html)
