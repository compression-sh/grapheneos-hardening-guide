# GrapheneOS Guides

Two practical guides for [GrapheneOS](https://grapheneos.org/) on supported Pixel devices, each available in English and German. The two languages are maintained in parallel and kept technically identical.

> **Not affiliated with the GrapheneOS project.** Where a statement comes from official GrapheneOS documentation it is tagged as such. Everything else is this repository's judgment, comes from a named external source, or is flagged `[Verify]`.
>
> **Security and privacy are not anonymity.** Neither guide makes a phone anonymous or unbreakable. They reduce attack surface, data exposure and identity correlation. The cryptophone guide ends each major section with its remaining risks; the daily-driver guide states its limits in the introduction and in the advanced-hardening, anonymity and common-mistakes sections.

## Which guide do you need?

| | **Daily-driver guide** | **Cryptophone guide** |
|---|---|---|
| **For** | A practical privacy-focused phone for everyday use | A single-purpose, maximum-hardening phone for sensitive communication and research |
| **Threat model** | Casual users, privacy-focused users, and a first look at high-risk use | Opportunistic thieves, malware, network observers and carriers, with higher-risk travel; a well-resourced targeted attacker is only partly considered |
| **Approach** | Balanced: usable day to day, with optional stricter settings | Strict: tiny app list, strict device policy, separate identity, incident planning |
| **Covers** | Installation, first boot, hardening, profiles, app sources, Sandboxed Google Play, realistic OPSEC, checklists | Threat model, hard device policy, per-setting trade-offs, compartments, communication and network OPSEC, behavioral OPSEC (SIM/eSIM discipline, when to power off, daily habits, identity separation), travel and seizure, incident response, useful websites, anti-patterns, verification status |
| **English** | [daily-driver-guide-en.md](daily-driver-guide-en.md) | [cryptophone-guide-en.md](cryptophone-guide-en.md) |
| **German** | [daily-driver-guide-de.md](daily-driver-guide-de.md) | [cryptophone-guide-de.md](cryptophone-guide-de.md) |

**Start with the daily-driver guide** unless your threat model already demands the stricter setup. The cryptophone guide builds on it and does not replace it. If you follow the cryptophone guide, treat a separate device, separate SIM or eSIM, and a separate network usage pattern as the realistic boundary. Profile separation alone is compartmentalization, not a complete boundary.

## Threat models

- **Daily-driver guide:** protects against common risks such as theft, opportunistic malware, tracking by apps and ad networks, and data exposure. It stays practical, with optional stricter settings, and treats high-risk use only as a first look.
- **Cryptophone guide:** assumes a higher-risk, single-purpose device used for sensitive communication and research. It adds a strict device policy, a tiny app list, SIM/eSIM and behavioral discipline, travel and seizure planning, and incident response. A well-resourced targeted attacker is only partly considered.
- Both guides reduce risk. Neither makes a phone anonymous or unbreakable.

## What the guides cover

Both guides:

- Official installation with the web installer or the command line, including **locking the bootloader only after a successful flash** and what to do when flashing or verification fails
- Screen lock, auto-reboot, USB-C port control, permissions, Network and Sensors permissions, Storage Scopes and Contact Scopes
- Profiles and their limits, Sandboxed Google Play and its trade-offs
- App sources, a comparison of the app stores (GrapheneOS App Store, Accrescent, F-Droid, Aurora Store, Obtainium, manual APK) and sideloading risks
- VPN, Tor, Private DNS, SIM and eSIM, carrier metadata, and why they do not add up to anonymity
- Checklists

Daily-driver guide only: supported devices and why verified boot matters, first-boot setup, update channels, common mistakes, quick-reference tables, and a change log from an earlier draft (sections 14 and 15).

Cryptophone guide only: behavioral OPSEC, incident response, anti-patterns, and a useful-websites list.

## How to read the tags

| Tag (English) | Tag (German) | Meaning |
|---|---|---|
| **[Official]** | **[Offiziell]** | GrapheneOS provenance: primary documentation or GrapheneOS project source; distinguish documentation from code, pin revisions where possible, no distributed-APK test implied |
| **[External]** | **[Extern]** | Named non-GrapheneOS provenance in either guide: own project documentation/code is primary for its own claims; third-party guides are secondary, not automatically GOS-Official |
| **[Advice]** | **[Empfehlung]** | This repository's judgment or general security practice |
| **[Verify]** | **[Prüfen]** | Unconfirmed claim: direct topic link with a reason. Meta references to this notation instead point to the tag legend, not to an unresolved claim |

Provenance and evidence are separate axes: `Official`/`External` identify whose source it is; primary documentation, project source, secondary source and unconfirmed describe evidence. Signal, Android and Accrescent own documentation is external AND primary. privacygear.nl is a secondary source for the NFC path. A source tag is not a practical test or security guarantee.

Each guide has a Tag legend section with the definitions and links to the open `[Verify]` topics: [daily-driver (EN)](daily-driver-guide-en.md#tag-legend), [daily-driver (DE)](daily-driver-guide-de.md#tag-legend), [cryptophone (EN)](cryptophone-guide-en.md#tag-legend), [cryptophone (DE)](cryptophone-guide-de.md#tag-legend).

## Important warnings

- **Installing GrapheneOS erases the phone.** Unlocking the bootloader wipes it, and locking it wipes it again. Back up first.
- **Use only the official installers** at <https://grapheneos.org/install/>. Third-party guides and "installers" are often outdated or unsafe.
- **Never lock the bootloader over a failed, incomplete or unverified flash.** Leave it unlocked and re-flash. Locking over an invalid OS can leave the device unrecoverable.
- **The Duress PIN/password is an irreversible wipe.** It is not a general anti-seizure control and has legal implications that depend on your jurisdiction.
- **Legal statements are general and jurisdiction-dependent.** Nothing here is legal advice.

## Verification status

The guides reference GrapheneOS primary documentation (install, usage, features, FAQ, releases, app repository), pinned GrapheneOS project source and external project documentation/source, with third-party guides identified separately as secondary. Local editorial review R01–R17 has been applied; overall acceptance remains a separate gate. Source reading and static document checks do not test distributed apps, devices, networking or practical security.

Open verification **categories, not individual claims: 3 in Daily, 6 in Crypto**, per language. Count occurrences as exactly linked `Verify`/`Prüfen` labels, bold or plain, excluding verbs and inline-code mentions; topics are unique `verify-*` base anchors, excluding `tag-verify`. Current per-language occurrences: **Daily 10 (6 direct-topic + 4 meta), Crypto 29 (26 direct-topic + 3 meta)**. Meta links lead to `#tag-verify`; direct links lead to the applicable category reason. Ten body/end-matter meta references already had the correct legend destination; this is not ten newly resolved claims.

Still unconfirmed and marked `[Verify]` / `[Prüfen]` in the text:

- The GrapheneOS project's stance on Tor VPN (its stance on Orbot appears only in a 2020 issue-tracker comment)
- Release-dependent menu paths and untested build behavior: NFC auto-off restoration, captive-portal login with VPN blocking, Sentry compatibility, Tor Android window behavior and the Accrescent licensing documentation/source discrepancy (grouped under `verify-menu-paths`; not positively confirmed or practically tested)
- Carrier and SIM details: virtual-number reassignment and country-specific carrier/KYC rules under SIM rules; eSIM/data-eSIM account, ID and payment requirements under eSIM; SIM-less equipment-identifier exposure in emergency calls remains network-dependent
- Country-specific legal, border and compelled-unlock rules. Check the rules of every country you enter or transit; obtain qualified local advice where needed. / Prüfe die Regeln jedes Landes, das du betrittst oder durchreist; hole bei Bedarf qualifizierten lokalen Rat ein. No legal advice is provided here.

## Sources

- GrapheneOS: <https://grapheneos.org/>, [install](https://grapheneos.org/install/), [usage](https://grapheneos.org/usage), [features](https://grapheneos.org/features), [FAQ](https://grapheneos.org/faq), [releases](https://grapheneos.org/releases)
- EFF Surveillance Self-Defense: <https://ssd.eff.org/>
- Freedom of the Press Foundation: <https://freedom.press/digisec/>
- Reporters Without Borders: [Digital Security Lab](https://rsf.org/en/digital-security-lab), [Digital Security and Spyware Guide](https://resources.rsf.org/digital-security-and-spyware-guide/)
- Tor Project: <https://www.torproject.org/>
- Obtainium: <https://github.com/ImranR98/Obtainium>
- privacygear.nl GrapheneOS hardening guide (secondary source, not official GrapheneOS documentation): <https://privacygear.nl/en/guides/grapheneos-hardening-guide/>
- Accrescent: <https://accrescent.app/>
- Google Android Help, Lockdown (external reference, not GrapheneOS documentation): <https://support.google.com/android/answer/9075927?hl=en>
- Cryptomator Android documentation: <https://docs.cryptomator.org/android/setup/>
- CBP, Border Search of Electronic Devices (Directive No. 3340-049B): <https://www.cbp.gov/document/directives/cbp-directive-no-3340-049b-border-search-electronic-devices>
- Signal: <https://signal.org/>, [Signal PIN and Registration Lock](https://support.signal.org/hc/en-us/articles/360007059792-Signal-PIN), [re-registering with the Signal PIN](https://support.signal.org/hc/en-us/articles/5440120029082-Re-registering-using-your-Signal-PIN), [APK download and verification](https://signal.org/android/apk/)

Each guide contains its own language-specific source list: Daily section 13 [EN](daily-driver-guide-en.md#13-sources) / [DE](daily-driver-guide-de.md#13-quellen); Crypto section 12 [EN](cryptophone-guide-en.md#12-useful-websites) / [DE](cryptophone-guide-de.md#12-useful-websites--nützliche-webseiten).
