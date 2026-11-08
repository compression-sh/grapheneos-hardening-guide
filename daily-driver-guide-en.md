# GrapheneOS Guide (English)

> **Status:** written 2026-11-05 and checked against the official GrapheneOS pages (features, usage, FAQ, web/CLI installer, releases). Menu names and device lists change between releases. Where something may differ on your device or version, the text says so. For anything marked [**Verify**](#tag-verify): *Check the relevant current primary documentation or project source.*
>
> **Legend:** [**Official**](#tag-official) = GrapheneOS documentation, project source or attributed project statements. [**External**](#tag-external) = a named non-GrapheneOS source, primary or secondary as specified. [**Advice**](#tag-advice) = this guide's recommendation, not an official GrapheneOS statement.

German version: [daily-driver-guide-de.md](daily-driver-guide-de.md) · For a stricter single-purpose setup see [cryptophone-guide-en.md](cryptophone-guide-en.md)

## Table of contents

1. [Introduction](#1-introduction)
2. [Supported devices and preparation](#2-supported-devices-and-preparation)
3. [Installation](#3-installation)
4. [First-boot setup](#4-first-boot-setup)
5. [Basic hardening](#5-basic-hardening)
6. [Advanced hardening](#6-advanced-hardening)
7. [Apps: safe installation and selection](#7-apps-safe-installation-and-selection)
8. [Sandboxed Google Play](#8-sandboxed-google-play)
9. [Anonymity: realistic OPSEC](#9-anonymity-realistic-opsec)
10. [Daily-use checklists](#10-daily-use-checklists)
11. [Common mistakes](#11-common-mistakes)
12. [Quick-reference tables](#12-quick-reference-tables)
13. [Sources](#13-sources)

[Tag legend](#tag-legend)

---

<a id="tag-legend"></a>
## Tag legend

Tags distinguish provenance (GrapheneOS or external) from evidence kind (primary documentation, project source, dated project statement, secondary source, or unconfirmed). Source and advice tags link to the legend; for unresolved claims, verification tags link to the relevant topic.

| Tag | Meaning |
|---|---|
| <a id="tag-official"></a>**[Official]** | GrapheneOS provenance: primary documentation, project source or attributed statements by project accounts or maintainers. Identify the source type; date statements and pin code revisions where possible. A source tag is not a practical test or a guarantee of current behavior. |
| <a id="tag-advice"></a>**[Advice]** | This guide's recommendation or general security practice; not a hard fact and not an official GrapheneOS statement. |
| <a id="tag-external"></a>**[External]** | Non-GrapheneOS provenance, not an evidence rank: a project's own documentation/code is primary for its own claims; a third-party guide is secondary. Name the source and evidence kind; External can therefore also be primary. |
| <a id="tag-verify"></a>**[Verify]** | Unconfirmed claim; follow the link for details and limitations. |

**Open verification topics** (categories, not individual claims; links lead to their reasons):
- [Release-dependent paths and untested build behavior](#verify-menu-paths)
- [Legal, border and compelled-unlock rules by country](#verify-legal)
- [eSIM/data-eSIM activation: account, ID or payment requirements](#verify-esim)

---

## 1. Introduction

### What GrapheneOS is and is not

GrapheneOS is a hardened, open-source Android-based operating system for supported Pixel devices. It starts from the Android Open Source Project (AOSP) and adds exploit mitigations (for example hardened memory allocator, hardware memory tagging on Pixel 8 and newer), a stricter permission model, and privacy features. [**Official**](#tag-official)

It is **not**:

- an anonymity tool. It does not hide your phone number, SIM, carrier, IP address or accounts;
- a replacement for good habits. A weak PIN, an unlocked bootloader or a pile of untrusted apps undo much of its protection;
- protection against everything. A powerful, targeted adversary with physical access, a device in an unlocked state, or a flaw in firmware can still succeed. GrapheneOS aims to raise the cost, not to guarantee safety.

### Security vs. privacy vs. anonymity

| Concept | Question it answers | Example measure |
|---|---|---|
| **Security** | Can someone break into the device or its apps? | Updates, strong passcode, locked bootloader, app sandbox |
| **Privacy** | Who gets to see which data about me? | Permission control, fewer trackers, no Google account |
| **Anonymity** | Can my actions be linked to *me*? | Separate identities, no linkable accounts, network-level care. Very hard on a phone |

You can have strong security with little anonymity (a well-protected phone registered under your name).

### Who this guide is for

Owners of a supported Pixel who want a clear, step-by-step path from installation to daily use. It is written for beginners but stays technically precise.

### Threat-model examples

| Profile | Typical worries | Realistic goal |
|---|---|---|
| **Casual user** | Theft, malware, ad tracking | Updates, strong PIN, few apps, no unnecessary permissions |
| **Privacy-focused user** | Data brokers, app telemetry, account profiling | All of the above plus profile separation, no/limited Google, reduced network exposure |
| **Journalist / activist-style high-risk user** | Device seizure, targeted surveillance, source protection | All of the above plus a long passphrase, short auto-reboot, USB lockdown, strict identity separation, travel discipline, and professional advice |

### What this guide will and will not protect against

**Helps with:** opportunistic theft, much common malware, the impact of many exploit classes, casual physical access to a locked device, bulk app tracking.

**Does not solve:** carrier and cell-tower location data, your own behavior and correlation across accounts, a compromised app you chose to trust, coercion, or a well-resourced targeted attacker. Use it to **reduce exposure**, not to expect perfection.

This guide covers lawful privacy and personal security. It does not help evade lawful investigations.

---

## 2. Supported devices and preparation

### Supported devices [**Official**](#tag-official)

At the time of writing, the FAQ lists official production support for: Pixel 6, 6 Pro, 6a, 7, 7 Pro, 7a, Fold, Tablet, 8, 8 Pro, 8a, 9, 9 Pro, 9 Pro XL, 9 Pro Fold, 9a, 10, 10 Pro, 10 Pro XL, 10 Pro Fold and 10a. The FAQ lists the Pixel 6 and 6 Pro with an OEM minimum support end of October 2026, so treat them as at or past end of support (official updates typically end shortly after). Older models had a 5-year minimum. Do not buy a Pixel 6 or 6 Pro anymore. [**Official**](#tag-official)

GrapheneOS strongly recommends Pixel 8 or newer (8, 8 Pro, 8a, 9 series, 10 series) because the OEM provides at least seven years of support from each model's launch and these devices support hardware memory tagging. Check the current supported-devices list before buying; that minimum does not guarantee seven remaining years at the purchase date. Older listed devices are on shorter or extended support; treat them as stop-gaps. The list above matches the FAQ as fetched on 2026-11-05; check <https://grapheneos.org/faq#supported-devices> again before buying, as it changes.

Carrier-locked variants (mainly some US carrier models) may not allow bootloader unlocking. Buy an unlocked device or confirm it can be unlocked.

### Why official support and verified boot matter [**Official**](#tag-official)

- Official devices receive full firmware, kernel and vendor security updates. An out-of-support device cannot be secured by the OS alone.
- Verified boot checks the operating system at every start and detects tampering. It only works fully when the bootloader is **locked** after installation, and GrapheneOS installs its own signing key so that this protection applies to GrapheneOS, not stock Android.
- The project gives no support for devices running with an unlocked bootloader, as that is an incomplete installation.

### Required equipment

- a supported Pixel (see above) and its USB-C cable, or a high-quality standards-compliant USB-C cable;
- a computer with at least 2 GB free memory and 32 GB free storage, running a supported OS on bare metal (a virtual machine is not recommended). The web installer can also run from an Android phone or tablet;
- a supported browser: Chromium (not Ubuntu's Snap package), Vanadium, Google Chrome, Microsoft Edge, or Brave with Brave Shields disabled [**Official**](#tag-official);
- internet access (the installer downloads the release);
- a **backup** of everything you want to keep.

> ⚠️ **Warning: installation wipes the device.** Unlocking the bootloader and locking it again each erase all data. Back up before you start, and do not rely on the old device state afterwards.

### Buying and setup considerations

- The official recommendation is to buy a supported Pixel and install GrapheneOS yourself. The project is not affiliated with and does not endorse companies selling preinstalled devices. [**Official**](#tag-official)
- If you buy a preinstalled device anyway, verify the verified-boot key hash after receiving it (see [3.6](#36-verify-the-installation)) and check the support lifetime.
- Buying from a shop, with cash or without an account, can reduce *some* purchase records. It does **not** make the device anonymous: the device identifiers, your SIM, and later behavior still link to you. Retailers may also retain records such as CCTV footage, inventory/IMEI data or payment metadata that can link even a cash purchase to a person. Do not rely on purchase tricks.

---

## 3. Installation

> ⚠️ Use **only** the official installers at <https://grapheneos.org/install/>. Never use unofficial images, "GrapheneOS installer" downloads, mirrors you cannot verify, or third-party guides that tell you to skip steps. The project states that third-party guides are often outdated and contain misguided advice. [**Official**](#tag-official)

### 3.1 Method A: web installer (recommended for most users)

Page: <https://grapheneos.org/install/web>

**Preparation**

1. Boot the stock Android and complete setup, connect to the internet.
2. Update the stock Android. On the **Pixel 6a**, OEM unlocking does not work with the factory stock Android: update to the June 2022 release or newer via OTA, **then factory reset** the device. [**Official**](#tag-official)
3. Enable developer options: **Settings → About phone** and tap **Build number** repeatedly.
4. Open **Settings → System → Developer options** and enable **OEM unlocking**. On carrier-sold variants this needs internet access so the stock Android can check whether the device was sold locked.

**Unlock** (wipes the device)

5. On the computer, open the install page in a supported browser. On traditional Linux distributions you need udev rules for non-root USB access (Arch: `android-udev`; Debian/Ubuntu: `android-sdk-platform-tools-common`). Use a direct port and a good cable, not a hub, and connect the phone. [**Official**](#tag-official)
6. Boot the phone into the bootloader (hold the volume-down button while the phone boots, as in the CLI guide; the web page also explains it), then click **Unlock bootloader** on the page.
7. Confirm on the phone with the volume buttons and power button.

**Flash**

8. Use the page's release download and **Flash release** controls. The installer flashes firmware, reboots into the bootloader interface and flashes the OS by itself. Do not unplug the cable or interact with the phone until it finishes. [**Official**](#tag-official)

**Lock**

9. **Lock the bootloader only after the official installer/flasher reports successful flashing.** Then use **Lock bootloader** on the page and confirm on the phone with the volume and power buttons. If flashing failed, was interrupted or is incomplete, do not lock: leave the bootloader unlocked and re-flash. Locking with a missing, incomplete or invalid OS can leave the device unrecoverable, because OEM unlocking can only be re-enabled from a booting OS. **Locking wipes all data again**, which is why it must happen before you put any data on the device. [**Official**](#tag-official) for the lock step and wipe; the failure warning is [**Advice**](#tag-advice)

> ⚠️ **Do not skip locking.** The installation is not complete until the bootloader has been locked after a successful, verified flash. Locking enables full verified boot and blocks fastboot flashing, formatting and erasing of partitions. [**Official**](#tag-official)

10. Reboot into GrapheneOS and complete setup (see [section 4](#4-first-boot-setup)).

### 3.2 Method B: command-line installation (advanced)

Page: <https://grapheneos.org/install/cli>

This method lets you install without trusting the project's web infrastructure: you download the factory image, **verify its signature with OpenSSH**, and flash with `fastboot`. It needs a supported OS with a current `fastboot` and OpenSSH, and enough understanding not to follow instructions blindly. The project's advice is to follow the guide **to the letter, without skipping, reordering or adding steps**. [**Official**](#tag-official)

Outline (the live page has the exact commands, versions and checksums; those change):

1. **Get `fastboot`.** The standalone Google platform-tools release is recommended for most users; the page gives download and SHA-256 verification commands per OS and requires adding it to `PATH`. Check `fastboot --version` before continuing.
2. **Enable OEM unlocking** in the stock Android (same as 3.1, steps 1-4, including the Pixel 6a note).
3. **Boot into the bootloader interface:** hold the volume-down button while the device boots until it shows the red warning triangle and "Fastboot Mode". Do not press the power button to select "Start". Connect the device.
4. **Unlock:** `fastboot flashing unlock`, then confirm on the device with the volume and power buttons. This wipes all data.
5. **Obtain and verify the factory images:** download `allowed_signers`, the `DEVICE_NAME-install-VERSION.zip` and its `.zip.sig`, then verify the signature with `ssh-keygen -Y verify` exactly as the page shows. Compare the signing key with the other locations the page lists. Never flash an image that fails verification. **If verification fails, or flashing fails or is incomplete, do not lock the bootloader.** Leave it unlocked and re-flash; the device may not boot until a verified GrapheneOS image has been flashed successfully and the bootloader has then been locked. Locking with a missing, incomplete or invalid OS can leave the device unrecoverable, because OEM unlocking can only be re-enabled from a booting OS. [**Advice**](#tag-advice) Re-download the image, re-verify it and retry the installation, or ask in the official GrapheneOS support channels (linked on the install page).
6. **Flash:** extract the zip (`bsdtar xvf` on Linux, `tar xvf` on macOS/Windows), enter the directory and run `bash flash-all.sh` (Linux/macOS) or `./flash-all.bat` (Windows). The script flashes firmware, reboots to the bootloader and flashes the OS. Do not interact with the device until it finishes.
7. **Lock:** only after successful flashing and verification (the flash script finished without errors and the image signature was verified), run `fastboot flashing lock` and confirm on the device. Never lock after a failed, incomplete or unverified flash; it can leave the device unrecoverable (see step 5). **Locking wipes all data again**; do it before using the device.
8. Boot GrapheneOS, finish setup, and keep the OEM-unlocking toggle on the last setup screen checked.

> ⚠️ Verify the signature before flashing. An unverified image defeats the purpose of the CLI method.

### 3.3 Disabling OEM unlocking

During first setup on the final screen a toggle for OEM unlocking is **checked by default**; this disables OEM unlocking, which is recommended. You can change it later in **Settings → System → Developer options**. [**Official**](#tag-official)

Leaving OEM unlocking disabled means the bootloader cannot be unlocked without access to the OS, which removes a way for an attacker to flash a modified system.

### 3.4 Turn off USB and wireless debugging

After installation, turn off USB debugging and wireless debugging unless you actively need them. [**Advice**](#tag-advice)

### 3.5 Common mistakes and troubleshooting

| Problem | Likely cause | What to do |
|---|---|---|
| Phone not detected | Bad cable/hub, VM, missing drivers on Windows | Use the original cable, a direct rear port, bare-metal OS; follow the install page's OS notes |
| "OEM unlocking" greyed out | No internet on carrier SKU; Pixel 6a not updated to June 2022+ or not factory reset afterward | Connect to the internet; update the stock Android; on the Pixel 6a factory reset after the OTA update |
| Flash fails midway | Cable/hub/browser issue | **Do not lock the bootloader.** Retry with another cable/port and restart the process from the bootloader; lock only after a complete, successful flash. Locking over a failed, incomplete or unverified flash can leave the device unrecoverable, because OEM unlocking can only be re-enabled from a booting OS |
| Setup shows "bootloader not locked" warning | Locking step skipped | Only if the original flash completed successfully: use "Reboot to bootloader" from the welcome screen and lock it via the install page. Do this before putting data on the phone [**Official**](#tag-official) (FAQ) |
| Yellow boot screen | Expected: shows the GrapheneOS key hash | See 3.6 |
| Stuck or in doubt | | Ask in the official chat (linked on the install page) |

### 3.6 Verify the installation

1. On boot you should see a **yellow** notice that an alternate OS is loaded, with an ID derived from the SHA-256 of the verified-boot public key. The full hash is shown, and you can compare it against the list on the install page. [**Official**](#tag-official) This check is useful, but verified boot works without you doing it manually. Compare the key hash on a separate, trusted device, not on the computer used to flash, because that computer could display anything.
2. During setup there must be no warning about an unlocked bootloader. If you see one, the installation is incomplete (see the troubleshooting table).
3. For stronger assurance use the **Auditor** app with a second Android device (hardware-based attestation) [**Official**](#tag-official). Pair soon after installation, before the device leaves your control, to establish continuity for later checks [**Advice**](#tag-advice). A later first verification still checks supported hardware, firmware and OS properties, but has no prior pairing baseline and retains the initial trust-bootstrap limits: leaked attestation keys or a suitable proxy device can defeat that first check [**Official**](#tag-official) (<https://grapheneos.org/install/web#verifying-installation>; <https://attestation.app/about>). It does not verify every installed app.

---

## 4. First-boot setup

Menu names and build behavior change between releases. <a id="verify-menu-paths"></a>[**Verify**](#verify-menu-paths) This category groups release-dependent paths and untested behavior: NFC auto-off availability, captive-portal behavior with VPN blocking and, where discussed, Sentry compatibility, Tor Android windows and Accrescent licensing. Specific uncertainties are stated beside their markers.

### 4.1 Initial setup choices

- Choose a language, and leave the "disable OEM unlocking" toggle on the final screen checked (default).
- Skip or decline any account sign-in. GrapheneOS does not need a Google account. [**Official**](#tag-official)
- Do not enable usage reporting you don't need. GrapheneOS contacts its own servers for updates, connectivity checks, time and similar; see the FAQ "default connections" entry for the full list. [**Official**](#tag-official)

### 4.2 Wi-Fi, mobile data, SIM and eSIM

- Update the OS first on a network you trust. For a higher-risk setup you may prefer setting a strong passcode before connecting.
- A SIM or eSIM links the phone to a carrier account and a location trail. See [section 9](#9-anonymity-realistic-opsec).
- eSIM is not more anonymous than a physical SIM. [**Advice**](#tag-advice) The EID identifies the device’s eUICC hardware, rather than an individual downloaded eSIM profile. [**External**](#tag-external) (<https://source.android.com/docs/core/connect/esim-euicc-api>) A Duress wipe also removes installed eSIM profiles [**Official**](#tag-official); that does not cancel the contract with the carrier. [**Advice**](#tag-advice)
- LTE-only mode (Settings → Network & internet → SIMs → your SIM → Preferred network type) reduces remote exploitation of legacy radio code; the project says it is not a confidentiality feature. [**Official**](#tag-official) It only helps if your carrier works reliably in LTE-only. [**Advice**](#tag-advice)
- If you do not need cellular, you can use the phone Wi-Fi-only (no SIM inserted or used). This avoids the SIM-based link to a carrier, not Wi-Fi/IP exposure. Airplane mode is not proof of untrackability, and powering off is stronger (see [cryptophone-guide-en.md, section 9.1](cryptophone-guide-en.md#91-mobile-network)). [**Advice**](#tag-advice)

### 4.3 Screen lock

Path: **Settings → Security & privacy → Device unlock**. [**Official**](#tag-official)

- Use a **random PIN of at least 6 digits**, or better a **passphrase** (several random words / long alphanumeric). Avoid birthdays and reused codes. [**Advice**](#tag-advice) GrapheneOS supports passwords of up to 128 characters, including diceware passphrases. [**Official**](#tag-official)
- Enable **PIN scrambling** (randomizes the keypad layout; applies to the lock screen and SIM PIN). [**Official**](#tag-official) It makes shoulder-surfing and inferences from smudge marks harder, but costs speed.
- Biometrics are a convenience, not your main secret. GrapheneOS offers **two-factor fingerprint unlock** (fingerprint plus a PIN), allowing a strong passphrase as the primary method. [**Official**](#tag-official) It also permits only 5 total fingerprint attempts (stock Android allows 20 with delays), which also lets you disable fingerprint unlock by deliberately failing 5 times with a different finger. [**Official**](#tag-official) Disable biometrics if you expect to be compelled to unlock.
- Use **Lockdown** to disable biometric unlock quickly: press Power + Volume Up, then tap Lockdown. Android can also show Lockdown in the power menu after enabling Settings → Display → Advanced → Lock screen display → Show lockdown option. Until the next unlock, it disables lock-screen notifications, fingerprint/face unlocking and Extend Unlock (Google Android Help: <https://support.google.com/android/answer/9075927?hl=en>). Lockdown is not the same as powering off or returning the device to BFU; power off or reboot for that. [**Advice**](#tag-advice)

### 4.4 Auto-reboot, USB-C and other security settings

BFU (Before First Unlock) refers to the state before the first unlock after a reboot; AFU (After First Unlock) refers to the state afterwards.

- **Auto-reboot:** each lock starts a countdown; a successful unlock of any profile cancels it. Expiry reboots the locked device to put data at rest (BFU). It does not run while already in BFU, so it does not repeatedly reboot there. Default is **18 hours**; range 10 minutes to 72 hours, or off [**Official**](#tag-official) (<https://grapheneos.org/features#auto-reboot>). A shorter timeout trades a smaller locked AFU window for more disruption [**Advice**](#tag-advice).
- **USB-C port** (**Settings → Security → Exploit protection**; the official usage page also writes "Security & privacy" for the parent menu, so the label may vary [**Official**](#tag-official)) has five modes: Off, Charging-only, **Charging-only when locked** (default), Charging-only when locked except before first unlock, On. [**Official**](#tag-official) If USB data are never needed, choose Charging-only or Off according to the required usability trade-off [**Advice**](#tag-advice). Off disables charging as well as data while the OS is booted. The feature does not apply while powered off, in firmware fastboot, or in charging, recovery and fastbootd modes [**Official**](#tag-official) (<https://grapheneos.org/features#usb-c-port-and-pogo-pins-control>).
- Wi-Fi and Bluetooth auto-turn-off settings exist (labels "Turn off Wi-Fi automatically" and "Turn off Bluetooth automatically" in the GrapheneOS Settings source) [**Official**](#tag-official); an NFC auto-turn-off setting was added in 2025 and later temporarily removed because of rare system/NFC HAL crash risks [**Official**](#tag-official) (release notes). Whether it is available in the current release is uncertain: no reliable confirmation of its restoration was found [**Verify**](#verify-menu-paths). Path: Settings → Security & privacy → Exploit protection (some GrapheneOS sections shorten the parent to Security) exposes Turn off Wi-Fi automatically and Turn off Bluetooth automatically [**Official**](#tag-official) (GrapheneOS Settings source: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/exploit_protection_settings.xml>).

### 4.5 Updates and update channels

- The System Updater checks about every six hours and installs signed updates over the air. Keep it enabled. [**Official**](#tag-official)
- Channels: **Stable**, **Beta**, **Alpha**. Releases move Alpha → Beta → Stable. Downgrades generally are not possible, so use **Stable** unless you accept temporary issues. [**Official**](#tag-official)
- Updating is one of the most valuable habits. Reboot when asked to finish an update.

---

## 5. Basic hardening

| Area | What to do | Notes |
|---|---|---|
| **Updates** | Keep auto-updates on, stay on Stable | Support ends when the vendor stops firmware updates |
| **Screen lock quality** | 6+ digit random PIN or passphrase, PIN scrambling | The secure element limits guesses (20 total attempts with escalating delays) [**Official**](#tag-official) |
| **Auto-lock timeout** | Short screen timeout; lock immediately on power button | Convenience vs. exposure [**Advice**](#tag-advice) |
| **Auto-reboot** | 18 h default; shorter for higher risk | Each lock starts the timer; a successful unlock of any profile cancels it. Expiry returns data to BFU; no repeated reboot in BFU |
| **USB accessories** | Keep "Charging-only when locked" (or stricter) | Accept new USB peripherals only when unlocked and trusted |
| **Bluetooth / Wi-Fi** | Off when not needed; use auto-turn-off; Wi-Fi uses per-connection MAC randomization by default [**Official**](#tag-official) | Scanning toggles under **Settings → Location → Location services** are off by default |
| **Location** | Deny, or "while in use"; prefer approximate location | GrapheneOS routes SUPL via its own proxy by default and offers a toggle [**Official**](#tag-official) |
| **Camera / microphone** | Grant per use ("only this time"/"while using") | Use the global quick toggles if available |
| **Clipboard** | Don't copy secrets into shared clipboards | Clipboard sharing to/from the parent profile can be blocked for Private Space on recent releases (release notes, 2025-05) [**Official**](#tag-official): Settings → Security & privacy → Private Space → System → Cross-profile shared clipboard → Disallowed (GrapheneOS Settings source: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/private_space_settings.xml>). Avoid copying secrets into the standard clipboard. Under standard clipboard rules, only the currently focused app and the configured default keyboard can read clipboard content [**Official**](#tag-official) (<https://grapheneos.org/faq#clipboard>). Secure Paste adds a per-app restriction with a global default and per-app overrides: when enabled for an app, it blocks reads of content set by other apps, while content the app set itself remains readable. Review per-app compatibility [**Official**](#tag-official) (<https://grapheneos.org/features#secure-paste>) |
| **Lock-screen notifications** | Hide sensitive content | Settings → Notifications (label varies) |
| **App permissions** | Review in Permission manager and Privacy dashboard | Remove unused apps entirely |
| **Sensors / features** | Use the **Sensors** permission (denied apps get zeroed data) and global toggles | Can be denied by default for new apps [**Official**](#tag-official) |

### Browser

Use **Vanadium**, the built-in hardened Chromium, which also provides the system WebView. [**Official**](#tag-official) Chromium-based browsers have the strongest sandbox and site isolation of the browser families, according to the project. [**Official**](#tag-official) Don't expect Vanadium alone to prevent fingerprinting or IP tracking: hiding the IP address requires an intermediary such as a VPN or Tor. [**Advice**](#tag-advice) JavaScript JIT is off by default in Vanadium, with a per-site toggle, and extension support is not planned. [**Official**](#tag-official) Extra browsers add attack surface; install them only for a reason.

### DNS and what it actually changes

- Private DNS (DNS-over-TLS) only encrypts DNS lookups. The destination IP is still visible and domain names still leak through TLS SNI. It is "recommended, but not an alternative to Tor or a VPN". [**Official**](#tag-official)
- **Default (Automatic):** keep it for normal use. In Automatic mode Android uses DNS-over-TLS opportunistically when the network's DNS servers support it. That protects against a passive listener only, because an active attacker can force a fallback to unencrypted DNS. [**Official**](#tag-official)
- **Custom server:** entering a hostname in **Settings → Network & internet → Private DNS** forces authenticated DNS-over-TLS with no fallback. Private DNS takes precedence over DNS provided by a VPN app. Websites can detect your DNS server and use it for fingerprinting. [**Official**](#tag-official)
- **Private DNS is global; VPN configurations are per profile.** Avoid a configured Private DNS hostname alongside a VPN. If any secondary profile uses a VPN, turn Private DNS fully Off globally, as GrapheneOS strongly recommends until this interaction is overhauled. A named server forces authenticated DNS-over-TLS; Automatic uses opportunistic DNS-over-TLS. If filtering is needed with a VPN, use a VPN app able to do both, such as RethinkDNS [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). This guide additionally recommends Off with any VPN as a stricter author policy, not a broader official requirement [**Advice**](#tag-advice).
- Choosing a DNS provider moves trust to that provider. It does not make you anonymous.

---

## 6. Advanced hardening

### 6.1 User profiles and when to use them

Profiles each have their own encrypted storage, app data, and keys. The **Owner** profile is special: it stores sensitive system-wide data, must be unlocked after reboot first, and cannot see other profiles' data. [**Official**](#tag-official)

Suggested layout [**Advice**](#tag-advice):

| Profile | Purpose |
|---|---|
| Owner | Administration, updates, app store, trusted core apps. Keep minimal |
| Daily/Personal | Normal apps if you do not want everything in Owner |
| Google/untrusted | Sandboxed Google Play and Google-dependent apps |
| Sensitive identity | Only for a separate role (see [section 9](#9-anonymity-realistic-opsec)) |

- Use **End session** (power menu or user switcher) when done. It fully purges that profile's keys from memory and puts it back at rest. Not possible for Owner without reboot. [**Official**](#tag-official)
- Secondary profiles can be set not to run in the background. Android's **Private Space** and **work profile** are also supported; GrapheneOS adds settings such as clipboard blocking and non-delayed locking for Private Space on recent releases. [**Official**](#tag-official) (release notes)
- Profiles separate app data and keys, not necessarily identities. They share underlying hardware and network access; per-profile VPNs are possible, so egress IP addresses may differ [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Shared habits or reused phone numbers, emails, names, contacts, files and writing styles can still correlate identities. Treat profiles as data compartments, not an anonymity guarantee [**Advice**](#tag-advice).

### 6.2 App isolation

Apps are sandboxed from each other by default. Most hardening here is about **choosing fewer apps**, putting risky ones in a separate profile, and using the scoping permissions below.

### 6.3 Storage Scopes and Contact Scopes [**Official**](#tag-official)

- **Storage Scopes**: an app that wants broad file access sees only the files/folders you pick, instead of all storage.
- **Contact Scopes**: an app sees only the contacts you choose.

Use them whenever an app requests storage/contacts access.

### 6.4 Network permission and Sensors permission [**Official**](#tag-official)

- The **Network** permission blocks direct and indirect network access per app (and per profile); the app sees "network down". Block it for offline tools (calculator, notes, offline PDF viewer). You can toggle it during app installation. Enabled by default for compatibility.
- The **Sensors** permission covers accelerometer, gyroscope, compass and other sensors not covered by Android permissions; denied apps get zeroed data. It can be disabled by default for newly installed apps in **Settings → Security & privacy → More security & privacy**.

### 6.5 PIN scrambling, Duress, and device seizure

- Enable **PIN scrambling** (see 4.3).
- **Duress PIN/password** [**Official**](#tag-official): entering the duress PIN/password as a device credential on the lock screen or in an OS device-credential prompt irreversibly wipes the device, including installed eSIMs. The duress PIN also works as the two-factor fingerprint unlock PIN, but currently not as the SIM PIN. A matching real unlock credential takes precedence and does not wipe. Set under **Settings → Security & privacy → Device unlock → Duress Password** in the Owner profile. A PIN and a password must both be set. It is not a remote wipe.

> ⚠️ **Danger:** Duress wipe is irreversible. Make an encrypted backup first, never test it casually, and don't make it identical to your real credentials (the real one takes precedence, so no wipe would occur). Whether to use it at all is a legal and personal-risk decision; destroying data during an investigation can be unlawful or criminally relevant depending on jurisdiction. Wiping data during a compelled unlock can be treated as obstruction in some jurisdictions. Deleting data after a legal demand, or in anticipation of a search, is the highest-risk action. Refusing to provide a passcode can itself be an offence in some jurisdictions. Get local legal advice before relying on Duress, auto-wipe, or refusal strategies. [**Advice**](#tag-advice) <a id="verify-legal"></a>[**Verify**](#verify-legal) the rules in your country: no country-specific legal statement is made here.

- Disk encryption: data is encrypted with keys tied to your credential and secure hardware. **After a reboot (BFU), data is at its most protected**; after first unlock (AFU) more is in memory. Short auto-reboot and powering off before border crossings or when handing over a device reduce exposure, but only if the passphrase is strong. They do not defeat seizure, coercion or lawful access. [**Advice**](#tag-advice)
- A weak PIN is the main weakness against forensic tools; use a long passphrase for high risk, which also stays strong against an attacker who defeats the secure element's rate limit. [**Advice**](#tag-advice)

### 6.6 Physical security and travel

- Prefer powering the phone off (or rebooting) before situations where you may lose control of it.
- Power the phone off before checkpoints; disable biometrics (Lockdown) when approaching them or when compelled-unlock risk exists. Disabling biometrics is a security setting, not a way to refuse a lawful demand. Know the local rules on compelled unlocking first; refusing may itself be an offence in some jurisdictions. [**Verify**](#verify-legal)
- Consider a travel device or minimal data on the phone when traveling to high-risk places or regions.
- Avoid public USB charging; use your own charger/cable.
- If the device was out of your control, use Auditor with an existing pairing to check continuity. Without a prior pairing, a first verification still checks supported properties, but cannot compare with a pre-loss baseline and retains the initial trust-bootstrap limits described above [**Official**](#tag-official). Establish an early pairing for future checks [**Advice**](#tag-advice).

### 6.7 Backups without creating a privacy hole

- GrapheneOS includes **Seedvault** for encrypted backups to local storage or a storage-provider app. The project says it plans a replacement because Seedvault's upstream was taken over by a group not sharing its goals, so treat it as the best available option for now. [**Official**](#tag-official)
- Keep backups **encrypted**, with the key not stored on the same device. Test restoring. Avoid unencrypted cloud backups. Don't back up the Duress setup or 2FA seeds somewhere less protected than the phone. [**Advice**](#tag-advice)

---

## 7. Apps: safe installation and selection

### 7.1 Sources, in order of preference [**Advice**](#tag-advice) unless stated

1. **GrapheneOS App Store**: installs GrapheneOS-built apps and Sandboxed Google Play, distributes further apps from its repository (including Accrescent and the PDF Viewer), and updates them automatically. [**Official**](#tag-official)
2. **Official developer releases** (for example the project's GitHub release) with **signature/hash verification**. Use the app’s own updater when available; otherwise track updates yourself.
3. **Accrescent**: a separate app store aimed at security and privacy. Its own primary site describes it as alpha [**External**](#tag-external) (<https://accrescent.app/>); GrapheneOS repository metadata separately lists an Accrescent mirror [**Official**](#tag-official) (project source: <https://github.com/GrapheneOS/apps.grapheneos.org/blob/c8e2b3fb21c420db7d4bab32ce3dd7e42afe7ea9/apps/packages/app.accrescent.client/common-props.toml>). It is ranked below verified developer releases here because of its alpha status [**Advice**](#tag-advice).
4. **F-Droid**: all-open-source apps. Apps with reproducible builds are published with the developer's signature after F-Droid verifies the build, other apps are signed with F-Droid's own keys, and F-Droid builds on its own timeline, so updates can lag (see 7.5). Prefer the developer's own channel when available. Use it for apps not available elsewhere, and keep only those you need.
5. **Aurora Store**: an alternative Play frontend. It still needs a Google account but fetches shared credentials from Aurora's service by default. [**Official**](#tag-official) (usage guide) Play apps are mostly closed source [**Advice**](#tag-advice) (general inference), so use it only as a last resort. [**Advice**](#tag-advice) Play services/Store updates are only accepted from the GrapheneOS App Store or the Play Store itself. [**Official**](#tag-official) (release notes)
6. **Manual APK**: only when necessary. Verify the developer's published signing certificate fingerprint (for example with `apksigner verify --print-certs file.apk`) or checksum from a channel separate from the download. For initial installation, grant "Install unknown apps" to one chosen file manager, not the browser, and revoke it afterward. Review any app-owned updater's installation prompts and permissions separately; Signal's website build manages its own update checks and downloads (see the source-backed [APK source comparison](#75-app-store-comparison)) [**Advice**](#tag-advice).

> ⚠️ **Warning:** avoid random APK sites and modified or cracked apps because of supply-chain and update risks. Installing an ordinary app or app store does not itself disable Verified Boot or the app sandbox; sandboxed Play also runs as regular apps on GrapheneOS [**Official**](#tag-official) (<https://grapheneos.org/features#sandboxed-google-play>). Root (Magisk), LSPosed/Xposed and modified system software are a separate class of intervention that can undermine OS integrity or sandbox boundaries; do not use them under this guide [**Advice**](#tag-advice).

### 7.2 Evaluating an app before installing [**Advice**](#tag-advice)

- Who publishes it? Open source? Recent updates? Independent audit?
- What does it request? Does it need network/contacts/location at all?
- Does the function need an account? Prefer apps that work offline.
- How does it make money (ads, analytics SDKs)?
- Does it need Google Play services? Can a web version or alternative do the job?
- After install: deny everything not needed, block Network if not needed, then test.

### 7.3 Minimum-permission mindset

Fewer apps, fewer permissions, fewer accounts. Avoid bloated, closed-source, telemetry-heavy apps when a simple alternative exists. Don't install "privacy" apps just because of the name.

### 7.4 Example choices (not official endorsements, unless noted) [**Advice**](#tag-advice)

| Category | Suggested option | Alternative | Notes |
|---|---|---|---|
| Browser | **Vanadium** (built-in) | Tor Browser for specific use | Tor Browser provides weaker exploit protection than Vanadium; see section 9. Don't add many browsers |
| Messaging | **Signal** | Other audited E2EE messengers | End-to-end encrypted. Signal registration requires a phone number. Usernames can hide your phone number from other users, but they do not remove the phone-number requirement or eliminate all metadata exposure. Signal is not in the GrapheneOS app repository [**Official**](#tag-official). Signal is not listed in Accrescent's repository catalogue checked on 6 November 2026 (catalogue timestamp 25 February 2026; availability can change; <https://repo.accrescent.app/repodata.1.json>). Use Signal's website APK, Google Play or another explicitly verified source instead (see 7.5). Recheck the repository if availability changes. |
| 2FA/authenticator | **Aegis** (open source) | Hardware security key (FIDO2) | Back up the vault encrypted; keep recovery codes offline |
| Password manager | **KeePassDX** or Bitwarden | KeePassXC on computer | Local database avoids a cloud account |
| VPN client | **Mullvad** or **WireGuard** official apps | RethinkDNS (VPN + filtering) | GrapheneOS's FAQ recommends the official WireGuard app and the official Mullvad app. VPN choice depends on trust, jurisdiction, logging policy, payment method and threat model [**Official**](#tag-official). Choose and pay for the VPN so it is not tied to your real identity: an account paid with your personal card or registered with your main email address can tie the VPN to you. [**Advice**](#tag-advice) According to the GrapheneOS FAQ, Mullvad's app is tested on GrapheneOS with hardware memory tagging, while the official WireGuard app has invalid memory accesses detected when MTE is enabled [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). With MTE enabled by default, prefer Mullvad. If WireGuard is essential, check current compatibility and use only a necessary per-app exception; never disable MTE globally [**Advice**](#tag-advice). |
| Maps/navigation | **Organic Maps** or OsmAnd | Web maps in the browser | Offline maps need no network |
| Email | **Proton Mail** or similar E2E-capable provider | Self-hosted | Email is metadata-rich; does not give anonymity. Proton's privacy policy says it keeps no permanent IP logs by default, may keep IP logs temporarily to combat abuse, and discloses limited data only if legally obligated; other providers differ |
| Cloud/storage | **Cryptomator** over a storage you choose | Local-only | Encrypt before upload |
| Notes | **Standard Notes**, Joplin, or a local notes app | Block Network for offline notes | Standard Notes is still maintained (open source, end-to-end encrypted; partnered with Proton since 2024) |
| Camera/gallery | **GrapheneOS Camera** (built-in) | | Check EXIF/location settings before sharing |
| PDF/office | Built-in **PDF Viewer** | Offline office suite with Network blocked | Documents can carry metadata |

Do not claim an app is anonymous unless it technically is. "No logs" VPN claims, "private" email and "encrypted" notes address specific risks only.

### 7.5 App store comparison

Every store below installs apps into the normal app sandbox. The differences are whether an account is needed, how updates arrive and whom you have to trust. Facts about third-party stores come from each project's own documentation (see the sources); the recommendations are this guide's judgment.

| Store | Account required? | Google dependency | Update mechanism | App selection (size, quality) | Security model | Recommendation: daily driver / cryptophone |
|---|---|---|---|---|---|---|
| **GrapheneOS App Store** | No account is mentioned as a requirement in the GrapheneOS documentation [**Official**](#tag-official) | None for the store itself; it can also install Sandboxed Google Play, which is optional [**Official**](#tag-official) | Updates the apps from its repository in the background, including the Sandboxed Google Play components [**Official**](#tag-official) | Small: GrapheneOS's own apps (for example Camera, PDF Viewer, Auditor, Vanadium), the Sandboxed Google Play components and a few others such as the Accrescent client [**Official**](#tag-official) | First-party app repository and client maintained by the GrapheneOS project and integrated into the OS [**Official**](#tag-official) | Daily driver: first choice. Cryptophone: first choice; install Sandboxed Google Play only if a required app cannot work otherwise ([Crypto section 6](cryptophone-guide-en.md#6-sandboxed-google-play)) [**Advice**](#tag-advice) |
| **Accrescent** | No account required | None stated by the project | Automatic, unattended, unprivileged updates on Android 12 and later | Small curated catalogue; the project is in alpha | App signing key pinning for first-time installs, signed repository metadata, and no remote APK signing, so developers keep control of their signing keys | Daily driver: use it for the apps it carries. Cryptophone: the same. Install the client from the GrapheneOS App Store, as Accrescent's own site recommends for GrapheneOS users. In the source order of 7.1 it ranks below verified developer releases only because of its alpha status [**Advice**](#tag-advice) |
| **F-Droid** | No account needed; F-Droid says it does not track what you install | No Google dependency stated; an independent repository of free and open-source apps | Through the F-Droid client; speed depends on the app, because F-Droid builds on its own timeline and some apps are outdated or lag behind the developer [**Advice**](#tag-advice) | Large catalogue of free and open-source apps; quality and update speed vary by app and repository [**Advice**](#tag-advice) | Apps are checked for security problems before they are added. For apps with reproducible builds F-Droid publishes the developer's signature after verifying the build; other apps are signed with F-Droid's own keys | Daily driver: fallback for apps the stores above do not carry; check that the app is maintained. Cryptophone: fallback only (rule in 7.1) [**Advice**](#tag-advice) |
| **Aurora Store** | Yes, a Google account is needed. By default it fetches shared account credentials from Aurora Store's service (shared dummy accounts handed out through token dispensers); you can also sign in with your personal Google account [**Official**](#tag-official) | Full: it is an alternative frontend to the Google Play Store [**Official**](#tag-official) | Updates the Play apps it installed. GrapheneOS accepts updates of Google Play services, the Google Services Framework and the Play Store only from its own App Store or the Play Store itself, so do not use Aurora for those [**Official**](#tag-official) | The Play catalogue exposed for the selected account and device, including compatibility and distribution restrictions; most listed apps are closed source [**Advice**](#tag-advice) | Developer-signed Play apps, but installs run through Google under a shared or a personal account. Shared dummy accounts are not anonymity: you rely on the dispenser service, the account is shared with many other users, and Google can still correlate device information and installs; a personal account ties installs to you [**Advice**](#tag-advice) | Daily driver: last resort, only in a separate profile and never with your main Google account. Cryptophone: do not use [**Advice**](#tag-advice) |
| **Obtainium** | No store account; Obtainium can track configured release sources. Some supported sources are developer-controlled (for example a developer's GitHub or GitLab release); others are mirrors or aggregators. Evaluate each configured source separately and prefer developer-controlled URLs under this guide's trust model | None, unless the app itself needs Google | Checks the release pages you configured, notifies you of new releases and installs them; it is not a store with its own review | Whatever apps publish APKs on supported release pages; you choose and configure each source yourself. It also supports aggregator and mirror sites (for example APKPure, Aptoide, Uptodown, and APKMirror as track-only) and third-party F-Droid repositories; APKs from those are hosted or repackaged by third parties, so check the signing certificate against the developer's [**Advice**](#tag-advice) | Only as strong as your trust in each source and your verification: it does not make an unsigned or compromised release safe. Obtainium itself publishes a signing-certificate fingerprint and a PGP key for verification (Obtainium README, section "Installation"); its source is on GitHub (<https://github.com/ImranR98/Obtainium>) | Daily driver: optional helper for apps that are only distributed as APKs and that the stores above do not carry. Cryptophone: not by default; it adds an app with the "Install unknown apps" permission and network access, so use it only for a documented need and verify each source. Do not configure aggregator or mirror sources (APKPure, Aptoide, Uptodown). The "Install unknown apps" permission stays granted to Obtainium and is not revoked after each install [**Advice**](#tag-advice) |
| **Manual APK download** | No store account; the developer's site decides | None, unless the app itself needs Google | Signal's website build checks for and downloads its own updates. Follow installation prompts and review the updater's permissions separately; do not assume silent, unattended installation. At the cited project-source revision, `shouldAutoUpdate()` returns `false` in the installer (update job: <https://github.com/signalapp/Signal-Android/blob/a74583b01e260944f699c4da03ba4e8ce04de32b/app/src/main/java/org/thoughtcrime/securesms/jobs/ApkUpdateJob.kt>; installer: <https://github.com/signalapp/Signal-Android/blob/a74583b01e260944f699c4da03ba4e8ce04de32b/app/src/main/java/org/thoughtcrime/securesms/apkupdate/ApkUpdateInstaller.kt>). This is source evidence, not a test of a distributed APK. Signal's own APK documentation (primary source) publishes the signing-certificate fingerprint for initial verification (<https://signal.org/android/apk/>). Other developer APKs without their own updater may require manual update tracking and downloads. | Whatever the developer publishes; not every app offers an APK | For initial installation, verify the signing-certificate fingerprint or checksum through a channel separate from the download; grant "Install unknown apps" only to the chosen file manager, not the browser, and revoke it after installation. This initial-installation permission is separate from any permission needed by the app's own updater; review the updater's installation prompts and permissions separately [**Advice**](#tag-advice) | Daily driver: use a verified developer APK when a necessary app is unavailable in the chosen store or another documented source requirement justifies it. Cryptophone: a verified developer APK may be required by the no-Play policy even when a Play version exists, for example Signal. For Signal, follow its updater rather than tracking every download by hand [**Advice**](#tag-advice) |

**Remaining risk:** the store you choose changes who learns which apps you install and how quickly fixes reach you. It does not make an app trustworthy, and no login mode of any Google-based store makes you anonymous.

---

## 8. Sandboxed Google Play

### What it is [**Official**](#tag-official)

A compatibility layer that lets you install the **official** Google Play services and Play Store as **ordinary sandboxed apps**. Both get no special privileges, no system-level access, and can only reach what you grant them like any app. GrapheneOS does not use Play services for OS functions even when installed. Apps in a profile can use them only if they are installed in that profile and the app chooses to.

### It is optional

Most users can run many apps without it. Prefer to use as much as possible without Google Play, and treat it as the exception. [**Official**](#tag-official)

### When it makes sense / when to avoid

| Install it when | Avoid it when |
|---|---|
| A required app (banking, transport, work) refuses to work without it | You can run your apps without it |
| You need push notifications from Google-dependent apps | Your threat model excludes Google involvement |
| You want to keep them away from your main profile | You would sign in with your main Google account in a profile with sensitive data |

### Installation [**Official**](#tag-official)/[**Advice**](#tag-advice)

1. Open the **App Store** and select **Google Play services**. This installs Google Play services and Play Store together (they depend on each other). Do not remove Google Services Framework if it exists from a pre-Android-15 install.
2. Choose where to install it. **Owner profile:** the simplest approach (the official guide calls it that), but less isolated; acceptable if you accept Google software in your main environment. [**Advice**](#tag-advice) **Separate user or work profile:** **recommended for privacy-focused and higher-risk users**, because only the apps in that profile can use it and the Owner profile (which holds system-wide sensitive data) stays free of Google software. [**Advice**](#tag-advice) The cryptophone guide is stricter and allows only the separate-profile option.
3. Give **Google Play services** a **battery-optimization exception** if you need reliable push notifications (not needed for the Play Store app).
4. Optional configuration at **Settings → Apps → Sandboxed Google Play**.

### Permission minimization [**Official**](#tag-official)/[**Advice**](#tag-advice)

- By default, Google Play location requests are rerouted to the OS location service, so you don't need to grant Play services location. Keep it that way.
- Deny contacts, SMS, phone, camera, microphone unless an app needs it. Don't grant "Allow all the time" location to Play services.
- Disable the advertising ID where offered.

### Risks and tradeoffs

- A Google account is **not anonymous**. Signing in links the profile to an identity at Google. Signing in is optional unless you want Play Store installs, in-app purchases or account-dependent app features. [**Official**](#tag-official) Google may also see which apps you install and information about the device; treat that as likely. [**Advice**](#tag-advice)
- Creating a Google account often requests phone verification. [**Advice**](#tag-advice)
- A separate profile limits data access, but it does not prevent Google from correlating the account through IP address, device characteristics, timing, or account activity. [**Advice**](#tag-advice)
- Compatibility is high but not complete. A few privileged features are unavailable. [**Official**](#tag-official)
- Profile isolation: put Google-dependent apps in one profile, keep sensitive data and identities in another, and don't share clipboard/files between them.
- Updates come through the GrapheneOS App Store.

---

## 9. Anonymity: realistic OPSEC

### Why a phone alone cannot make you anonymous

A phone is a bundle of identifiers and a location sensor. Software hardening does not change what the network, carrier or services you use can see.

How you obtain and set up a tool matters as much as which one you pick: a VPN paid with your real card or an account registered with your real number can link a new identity back to you. [**Advice**](#tag-advice)

| Factor | What it reveals / links |
|---|---|
| **SIM/eSIM, IMSI, phone number** | Identify you to the carrier. Carriers log which cell towers you use (location). The EID identifies the device’s eUICC hardware, rather than an individual downloaded eSIM profile. [**External**](#tag-external) (<https://source.android.com/docs/core/connect/esim-euicc-api>) Activation requirements depend on the carrier and country <a id="verify-esim"></a>[**Verify**](#verify-esim) (no universal primary source found for account, ID or payment requirements). Registration rules vary by country |
| **IMEI** | Device hardware identifier seen by the network; changing SIMs does not change it. Carriers can log IMSI/IMEI pairs, so a new SIM in the same phone, or an old SIM in a new phone, can link identities; EFF: the network observes SIM and device together |
| **Mobile-network metadata** | Call/SMS/data records, tower connections, timing. A VPN does not hide that your phone connects to the network. Calls, SMS and VoLTE are carrier services and are not covered by a VPN |
| **IP address** | Seen by every server you contact; hidden only by VPN/Tor (shifting trust) |
| **Accounts, email, phone number for sign-ups** | Link activity across services |
| **Payment methods, delivery addresses** | Strong real-world links |
| **Bluetooth/Wi-Fi/location** | Nearby-device and place correlation |
| **App telemetry, device fingerprints** | Cross-app and cross-session correlation |

### Public Wi-Fi, VPN and Tor

| Tool | Helps with | Does not help with |
|---|---|---|
| **Public Wi-Fi** | Avoids tying traffic to your home IP | Account logins, payments, the cellular network, the Wi-Fi operator seeing traffic. Captive portals may request a phone number or email address, and CCTV, payment records and location patterns can still link a person to a place. GrapheneOS randomizes MAC per connection by default [**Official**](#tag-official) |
| **VPN** | Hides destinations and content from your local network/ISP (they can still see that a VPN is in use); hides your IP from sites | Moves trust to the VPN provider; doesn't hide cellular location, accounts, or behavior; leaks if misconfigured. Use the **Always-on VPN + "Block connections without VPN"** settings [**Official**](#tag-official). Captive-portal login behavior with blocking enabled is unverified here [**Verify**](#verify-menu-paths). If login requires temporarily lifting the block, do so only if the exposure is acceptable and re-enable it immediately, or avoid that network [**Advice**](#tag-advice). |
| **Tor** | Hides your IP from sites through multi-hop routing | Doesn't hide what you reveal by logging in or by content; makes traffic stand out; slow; exit nodes can see unencrypted traffic |

- **When a VPN helps:** untrusted networks, hiding from the local ISP or a site, or appearing from a stable IP region. **When it doesn't:** you log into accounts tied to you, or the threat is the carrier or the VPN provider.
- **Tor on mobile:** the project notes Tor Browser's security is weak compared to Vanadium and that Tor itself can make you more of a target. [**Official**](#tag-official) If you need strong Tor-based anonymity, a dedicated setup, meaning a separate device or a separate operating system and not merely a separate app, is more appropriate than a daily-use phone. App routing through Orbot or Tor VPN is not a substitute for Tor Browser's usage rules, and the Tor Project says the Tor VPN beta should not be used for sensitive activities. In a [dated issue-tracker comment from 1 May 2020](https://github.com/GrapheneOS/os-issue-tracker/issues/210#issuecomment-622457418), GrapheneOS maintainer thestinger described Orbot as poorly implemented and maintained and rejected forking or bundling it. [**Official**](#tag-official) This dated comment does not establish the project’s current assessment of Orbot or Tor VPN.
- Android allows one VPN per profile; don't stack VPN apps blindly.
- Use a Wi-Fi network your private phone never joins, and do not use both devices at the same times and places. [**Advice**](#tag-advice)

### Separate identities instead of just tools

For a legitimately separate role (for example a professional or advocacy identity):

1. Use a **separate profile** with no contacts, files, accounts or backups from your personal identity.
2. Use separate email/accounts that you create in that profile and never use elsewhere. Create new accounts on the device itself, with a new email address that is not tied to your personal recovery email or number. If a service demands a phone number, that number can link the accounts to each other and to you (see [Setting up a separate line](cryptophone-guide-en.md#setting-up-a-separate-line)). [**Advice**](#tag-advice)
3. Never log into personal accounts there; never reuse usernames, avatars, writing style, or schedules.
4. Don't cross-share files, clipboard or notifications between profiles.
5. Be aware that the same SIM, device, home Wi-Fi, location and timing still link profiles to each other and to you.
6. Strip metadata (EXIF, document properties) before sharing.

A separate number: a prepaid SIM bought without adding records beyond your country's registration rules, or an eSIM activated with a separate email address, avoids reusing your main number. Virtual number services are not anonymous and their numbers can be recycled. Details: [cryptophone guide, "Setting up a separate line"](cryptophone-guide-en.md#setting-up-a-separate-line). [**Advice**](#tag-advice)

**For a high-risk threat model, a separate device, separate SIM/eSIM, and separate network usage pattern are the realistic boundary. Profile separation alone is compartmentalization, not a complete boundary.**

This reduces unnecessary data exposure and limits correlation. It does not create anonymity, and it must stay within the law. This guide does not help evade lawful investigations.

---

## 10. Daily-use checklists

### Setup day
- [ ] Supported Pixel with remaining support checked
- [ ] Installed via official installer; **bootloader locked**
- [ ] Verified boot key hash checked (or Auditor used)
- [ ] OEM unlocking disabled; USB debugging off
- [ ] Updates installed; channel Stable
- [ ] Strong PIN/passphrase; PIN scrambling on
- [ ] Auto-reboot set; USB-C "Charging-only when locked" or stricter
- [ ] Location, camera, mic, contacts, storage reviewed
- [ ] Profiles created if needed; backups configured and tested

### Weekly / monthly
- [ ] Updates installed and rebooted
- [ ] Review Privacy dashboard and permissions
- [ ] Remove unused apps and profiles
- [ ] Check VPN kill-switch behavior if used
- [ ] Test that backup restores

### Before travel
- [ ] Update and reboot; back up; remove unneeded data
- [ ] Set short auto-reboot; consider a stronger passphrase
- [ ] Decide on biometrics (disable/Lockdown)
- [ ] Understand local laws on device searches and encryption
- [ ] Know the Duress feature's legal and personal risks before using it
- [ ] Bring your own charger; avoid public USB ports

### After installing a new app
- [ ] Source verified (App Store / developer signature)
- [ ] Deny all unneeded permissions; use Storage/Contact Scopes
- [ ] Block Network if it works offline
- [ ] Sensors permission denied if not needed
- [ ] Put in an appropriate profile
- [ ] Uninstall if not used within a month

---

## 11. Common mistakes

| Mistake | Why it hurts | Better |
|---|---|---|
| Installing too many "privacy" apps | Each app adds attack surface and trust | Install the minimum |
| Trusting VPNs blindly | Provider sees traffic; leaks happen | Know what it protects; use kill switch |
| Weak PIN | Brute-force/forensic risk | Long random PIN or passphrase |
| Leaving the bootloader unlocked | Full verified boot disabled; unsupported | Lock only after a successful, verified flash |
| Installing random APKs | Malware, no verified updates | Trusted sources, verify signatures |
| Mixing sensitive and normal identities in one profile | Correlation | Separate profiles and accounts |
| Believing GrapheneOS alone gives anonymity | SIM, network, accounts still identify you | Read section 9 |
| Using Google services without understanding the tradeoff | Account links activity to you | Isolated profile, minimal permissions, or avoid |
| A configured Private DNS server together with a VPN | Private DNS is global; VPN configurations are per profile and a configured Private DNS server takes precedence over VPN-provided DNS [**Official**](#tag-official) | Private DNS is global. Do not configure a Private DNS hostname alongside a VPN; if any secondary profile uses a VPN, turn Private DNS fully Off globally, as GrapheneOS strongly recommends [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). This guide additionally recommends Off with any VPN as a stricter author policy [**Advice**](#tag-advice). |
| Testing Duress casually | Irreversible wipe | Back up; never test on a device with data |

---

## 12. Quick-reference tables

### Settings

| Setting | Recommended value | Why | Risk if ignored |
|---|---|---|---|
| Bootloader | Locked | Full verified boot | Tampering, unsupported install |
| OEM unlocking | Off | Prevents unlocking without access to the OS | Easier flashing of modified OS |
| Screen lock | 6+ digit random PIN / passphrase | Resists guessing | Easy unlock |
| PIN scrambling | On | Reduces shoulder surfing | Code observed |
| Auto-reboot | 18 h (default) or shorter | Each lock starts the countdown; a successful unlock of any profile cancels it. Expiry returns data to BFU; no repeats in BFU | Exposure until the locked countdown expires; not protection while unlocked |
| USB-C port | Charging-only when locked (or stricter) | Reduces USB attack surface | Exposure to USB data attacks |
| Updates / channel | Auto, Stable | Security fixes | Known vulnerabilities |
| Location | Off / while in use / approximate | Less tracking | Persistent location trail |
| Network permission | Block for offline apps | Blocks telemetry over the network | Hidden data leaks |
| Sensors permission | Deny by default for new apps | Limits sensor side channels | Fingerprinting/side channels |
| Private DNS | Automatic (default) normally. Private DNS is global. Do not configure a Private DNS hostname alongside a VPN; if any secondary profile uses a VPN, turn Private DNS fully Off globally, as GrapheneOS strongly recommends [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). This guide additionally recommends Off with any VPN as a stricter author policy [**Advice**](#tag-advice). | Automatic gives opportunistic encryption; a configured hostname forces authenticated DNS-over-TLS | VPN conflicts and unexpected DNS behavior if misconfigured |
| Google Play | Optional, isolated profile | Limits Google scope | Account-linked profiling |
| Duress | Optional, with backup | Optional wipe feature; not a general anti-seizure control | Accidental irreversible wipe |

### Apps

| App type | Recommended option | Alternative | Notes |
|---|---|---|---|
| Browser | Vanadium | Tor Browser (special cases) | Tor Browser provides weaker exploit protection than Vanadium; see section 9. Don't add many |
| Messaging | Signal | Other audited E2EE | Registration requires a phone number; usernames only hide it from other users |
| 2FA | Aegis | FIDO2 key | Keep recovery offline |
| Password manager | KeePassDX | Bitwarden | Local DB or trusted sync |
| VPN | Mullvad / WireGuard | RethinkDNS | Official FAQ recommends these two apps; choice depends on trust, jurisdiction, logging, payment and threat model. According to the GrapheneOS FAQ, Mullvad's app is tested on GrapheneOS with hardware memory tagging, while the official WireGuard app has invalid memory accesses detected when MTE is enabled [**Official**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). With MTE enabled by default, prefer Mullvad. If WireGuard is essential, check current compatibility and use only a necessary per-app exception; never disable MTE globally [**Advice**](#tag-advice). |
| Maps | Organic Maps | OsmAnd | Offline |
| Email | Proton Mail | Self-hosted | Metadata remains; providers may log IPs temporarily and must disclose data when legally obligated (Proton privacy policy) |
| Storage | Cryptomator | Local only | Encrypt first |
| Notes | Standard Notes / Joplin | Local notes | Block network if offline |
| Camera | GrapheneOS Camera | | Check metadata |
| PDF | Built-in PDF Viewer | | Strip metadata |

### Threat level

| Level | Main priorities | Recommended setup |
|---|---|---|
| Basic | Updates, lock, stay locked | Official install, locked bootloader, 6+ digit PIN, few apps |
| Strong privacy (daily) | Permissions, profile separation, less Google | Above + scopes, Network/Sensors permission, optional isolated Play profile, VPN with kill switch |
| Higher-opsec | Reduced seizure exposure through BFU state and a strong passphrase, identity separation, discipline | Above + passphrase, short auto-reboot, strict USB, separate identity profiles, travel plan, Auditor, professional advice |

---

## 13. Sources

**Primary GrapheneOS documentation:** the linked pages below; pinned GrapheneOS project-source links in the body are a separate primary evidence kind, not documentation or APK tests.

- Home: <https://grapheneos.org/>
- Install overview: <https://grapheneos.org/install/>
- Web installer: <https://grapheneos.org/install/web>
- CLI installer: <https://grapheneos.org/install/cli>
- Usage guide: <https://grapheneos.org/usage>
- Features: <https://grapheneos.org/features>
- FAQ: <https://grapheneos.org/faq>
- Releases and changelog: <https://grapheneos.org/releases>
- Auditor / attestation: <https://attestation.app/>

**External project documentation and repositories:** Accrescent, Obtainium, Signal and Android/Google documentation are primary for their own claims, not official GrapheneOS sources. Distinguish documentation from project source; third-party guides such as privacygear.nl are secondary.

- Accrescent: <https://accrescent.app/>
- Obtainium: <https://github.com/ImranR98/Obtainium>
- Google Android Help, Lockdown: <https://support.google.com/android/answer/9075927?hl=en>
- F-Droid: <https://f-droid.org/en/about/> and <https://f-droid.org/docs/FAQ_-_App_Developers/>
- Mullvad VPN: <https://mullvad.net/>
- Tor Project: <https://www.torproject.org/>
- Signal, phone-number privacy and usernames: <https://signal.org/blog/phone-number-privacy-usernames/>
- Signal Terms of Service: <https://signal.org/legal/>
- Android developer documentation (eSIM/EID): <https://source.android.com/docs/core/connect/esim-euicc-api>

[**Advice**](#tag-advice) labels identify this guide’s recommendations. [**Verify**](#tag-verify) labels identify unresolved points.
