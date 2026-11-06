# GrapheneOS Cryptophone Guide (English)

> **What this is:** a maximum-hardening, single-purpose GrapheneOS configuration for sensitive communication and research. It is stricter and simpler than the daily-driver guide ([daily-driver-guide-en.md](daily-driver-guide-en.md)), which it does not replace.
>
> **What this is not:** a way to become anonymous or unbreakable. It reduces attack surface, metadata exposure, identity correlation and the impact of a compromise. It does not defeat a compromised supply chain, a compromised computer, malicious hardware, physical coercion, a trusted-but-compromised app, a determined adversary with device access, carrier and network metadata, or human error.
>
> **Status:** written 2026-11-05. GrapheneOS claims were checked against the official GrapheneOS pages (install, usage, features, FAQ, releases). Other claims were checked against the named external primary sources. Menu names change between releases.
>
> **Tags:** [**Official**](#tag-official) = stated in official GrapheneOS documentation. [**External**](#tag-external) = stated by a named non-GrapheneOS primary source (for example EFF, Tor Project, Signal, an app's own site). [**Advice**](#tag-advice) = this guide's judgment. [**Verify**](#tag-verify) = could not be confirmed; *Verify against current official documentation.*
>
> **Not legal advice.** Any statement about searches, compelled unlocking or data destruction is general and jurisdiction-dependent. Get local legal advice.

German version: [cryptophone-guide-de.md](cryptophone-guide-de.md)

## Table of contents

- [1. Purpose and threat model](#1-purpose-and-threat-model)
- [2. Hard device policy](#2-hard-device-policy)
- [3. Device setup](#3-device-setup)
- [4. Hardening settings](#4-hardening-settings)
- [5. Profiles and compartments](#5-profiles-and-compartments)
- [6. Sandboxed Google Play](#6-sandboxed-google-play)
- [7. Apps](#7-apps)
- [8. Communication OPSEC](#8-communication-opsec)
- [9. Network OPSEC](#9-network-opsec)
- [Behavioral OPSEC / Verhaltens-OPSEC](#behavioral-opsec--verhaltens-opsec)
- [10. Travel and physical security](#10-travel-and-physical-security)
- [11. Incident response](#11-incident-response)
- [12. Useful websites / Nützliche Webseiten](#useful-websites--nützliche-webseiten)
- [13. Checklists](#13-checklists)
- [14. Anti-patterns](#14-anti-patterns)
- [15. Essential vs optional, and verification status](#15-essential-vs-optional-and-verification-status)

[Tag legend](#tag-legend)

---

<a id="tag-legend"></a>
## Tag legend

Every tag in this guide links to its entry below.

| Tag | Meaning |
|---|---|
| <a id="tag-official"></a>**[Official]** | Stated in official GrapheneOS documentation (features, usage, FAQ, installer, release notes or project source). Variants such as "Official, release notes" name the page concerned; combined tags such as "Official/Advice" link to the first type. |
| <a id="tag-advice"></a>**[Advice]** | This guide's recommendation or general security practice; not a hard fact and not an official GrapheneOS statement. |
| <a id="tag-external"></a>**[External]** | Stated by a named non-GrapheneOS primary source (for example EFF, Tor Project, Signal, an app's own site); not official GrapheneOS documentation. |
| <a id="tag-verify"></a>**[Verify]** | Could not be confirmed. The reason is stated next to the tag. Each tag jumps to the first place where the reason for its topic is given. |

**Open verification topics** (each links to the place where the reason is given):

- [Country-specific SIM registration rules](#verify-sim-rules)
- [Legal, border and compelled-unlock rules by country](#verify-legal)
- [Menu paths and labels](#verify-menu-paths)
- [Bluetooth/Wi-Fi auto-off menu path](#verify-menu-bt-wifi)
- [Private Space clipboard menu path](#verify-menu-clipboard)
- [Signal on Accrescent](#verify-signal-accrescent)
- [Cryptomator Accrescent build and Google Drive](#verify-cryptomator-accrescent)
- [IMEI visibility of a SIM-less phone](#verify-imei)
- [GrapheneOS stance on Tor VPN](#verify-tor-vpn)
- [Whether eSIM activation needs an account, ID or payment](#verify-esim)
- [Text of the CBP border-search directive](#verify-cbp)

---

## 1. Purpose and threat model

### What the device is for

- Sensitive messaging
- Sensitive browsing
- Secure notes and 2FA
- A separate, compartmentalized identity or role
- Travel or higher-risk environments

### What it is not for

- Everyday social media
- Random app experimentation
- Personal photos
- Banking and shopping
- Contacts-heavy daily use
- Logging into old personal accounts

If an activity is on this list, do it on another device. Mixing roles on this device destroys most of its value.

### Four concepts, kept apart

| Concept | Question | Example control | Does not give you |
|---|---|---|---|
| **Security** | Can the device or its apps be compromised? | Updates, locked bootloader, strong passphrase, few apps | Privacy from services you use |
| **Privacy** | Who collects which data about me? | Permission control, no Google account, minimal telemetry | Anonymity |
| **Anonymity** | Can actions be attributed to me? | Separate identities, careful network behavior | Anything, if one linkable detail leaks |
| **Compartmentalization** | If one identity is exposed, how much follows? | Separate profiles, accounts, SIM, ideally separate devices | Protection against a compromised device |

### Threat model for this guide

Adversaries considered: opportunistic thieves, malware and malicious apps, network observers (Wi-Fi operator, ISP, VPN provider), carriers, service providers, and an adversary who obtains the powered-off or locked device. A well-resourced targeted attacker is a **partial** consideration only: this guide raises the cost for such an adversary, but does not claim to stop one.

### What it does not defeat

| Not defeated | Why |
|---|---|
| Compromised supply chain or malicious hardware | You cannot verify hardware beyond attestation; Auditor checks hardware, firmware and OS but not every app [**Official**](#tag-official) |
| Compromised computer used to install or back up | An attacker who used a compromised flashing computer to install a malicious OS can be detected afterwards by verified boot and attestation [**Official**](#tag-official), provided you compare the displayed key hash against the official list on a separate trusted device and use Auditor paired from another device; the install page on a compromised computer can show anything. [**Advice**](#tag-advice) A compromised computer you also use for sensitive work is a separate problem |
| Physical coercion | No software setting changes this |
| Malware via a trusted but compromised app | The app sandbox limits damage but does not remove trust in an app you chose |
| Determined adversary with device access | Raises cost; does not guarantee protection, especially once the phone is unlocked or in the after-first-unlock state |
| Carrier and network metadata | The carrier sees SIM, IMEI, towers and timing no matter what the OS does |
| Human error | The most common failure |

**Remaining risk of this section:** the threat model itself may be wrong. Re-check it whenever your role or location changes. See EFF's "Your Security Plan" module (listed under Useful websites).

---

## 2. Hard device policy

These are rules, not suggestions. Each rule has a reason; if you cannot follow one, understand what you are giving up.

1. **One purpose.** The device does sensitive communication and research, nothing else.
2. **No app without a documented reason.** Keep a short list: app, source, purpose, permissions granted, date added. Remove apps you no longer need.
3. **No reused identity material.** Do not reuse personal accounts, usernames, email addresses, phone numbers, profile pictures or recovery contacts.
4. **No real-name contacts** unless operationally necessary, and then only the specific contact (Contact Scopes, section 4).
5. **Separate SIM/eSIM.** Do not use the SIM or eSIM of your normal phone unless your threat model explicitly accepts correlation. Do not move a SIM between this device and another one: carriers can log IMSI/IMEI pairs, so a new SIM in the same phone, or an old SIM in a new phone, can link identities (see 9.1). Also avoid carrying or powering on this device together with your personal phone at the same times and places, buying the SIM and device together or with traceable payment, and topping up with a linked payment method. SIM registration and ID rules are country-specific. Set a SIM PIN. [**Advice**](#tag-advice) <a id="verify-sim-rules"></a>[**Verify**](#verify-sim-rules) the rules of your country.
6. **No personal payment methods** for anything tied to this identity.
7. **No biometrics** if your threat model includes coercion, seizure or forced unlock. EFF notes that there is less protection against compelled face and fingerprint unlocking than against compelled password disclosure, in the protest context it describes. [**External**](#tag-external) Whether and where either can be compelled is jurisdiction-dependent; get legal advice. <a id="verify-legal"></a>[**Verify**](#verify-legal) GrapheneOS permits only 5 total fingerprint attempts (stock Android allows 20 with delays). [**Official**](#tag-official)
8. **Strong secret.** Use a long random alphanumeric passphrase or a long random PIN. Tradeoff: the secure element limits guesses to 20 total attempts with escalating delays, which the project says offers a high level of security even for a random 6-digit PIN. [**Official**](#tag-official) A longer passphrase (up to 128 characters; diceware supported [**Official**](#tag-official)) stays strong even against an attacker who defeats the secure element's rate limit, at the cost of typing effort and shoulder-surfing exposure. [**Advice**](#tag-advice) **Recommended:** a diceware-style passphrase, or a random PIN of 8 or more digits if typing a passphrase is unworkable. [**Advice**](#tag-advice)
9. **Auto-reboot on** (section 4).
10. **USB-C port restricted** (section 4).
11. **Radios off by default:** Bluetooth, Wi-Fi, NFC and location off unless in use.
12. **Updates immediately.**
13. **Backups minimal, encrypted, offline** (section 4).
14. **Nothing on the device that you cannot afford to lose or have read.**

**Remaining risk:** policy only works if followed every day. A single reuse of an old username or phone number can undo months of separation.

---

## 3. Device setup

### 3.1 Hardware and software rules

- **Supported Pixel only**, preferably a recommended 8th-generation or newer model, which has a minimum of 7 years of support and hardware memory tagging. [**Official**](#tag-official) Check <https://grapheneos.org/faq#supported-devices> before buying. Carrier-variant Pixels may not allow bootloader unlocking, so buy an unlocked retail unit; enabling OEM unlocking can require internet access on some variants. [**Official**](#tag-official)
- **Official GrapheneOS only**, installed with the official **web installer** (<https://grapheneos.org/install/web>) or the **CLI guide** (<https://grapheneos.org/install/cli>). Follow the chosen guide to the letter, without skipping, reordering or adding steps. [**Official**](#tag-official)
- **Forbidden:** third-party recovery, custom ROMs, root, Magisk, Xposed, LSPosed, unofficial APK stores, modified system components, "privacy ROMs", and obscurity tools. They weaken or remove verified boot and the sandbox. [**Advice**](#tag-advice)
- Prefer a device you bought and installed yourself. The project does not endorse companies that sell preinstalled devices. [**Official**](#tag-official) Buying tricks do not make the device anonymous; retailers may keep CCTV, IMEI and payment records. [**Advice**](#tag-advice)

### 3.2 Installation outline

> ⚠️ **Unlocking and locking the bootloader each erase all data.** Back up anything on the device first; a used device will be wiped, and installation erases it.

1. Boot the stock Android, update it, enable developer options (**Settings → About phone → Build number**), then enable **OEM unlocking** under **Settings → System → Developer options**. On a Pixel 6a, update to June 2022 or newer by OTA and factory reset first. [**Official**](#tag-official)
2. Boot into the bootloader interface by holding **volume down** while the device boots until the red triangle and "Fastboot Mode" appear. Do not select "Start". [**Official**](#tag-official)
3. **Unlock** the bootloader (web installer button or `fastboot flashing unlock`) and confirm on the device. This wipes the device. [**Official**](#tag-official)
4. **Flash** (web installer **Flash release**, or CLI: verify the image signature with `ssh-keygen -Y verify` using `allowed_signers`, extract, run `flash-all`). Do not interact with the device until it finishes. [**Official**](#tag-official)
5. **Lock the bootloader only after the official installer/flasher reports successful flashing (for the CLI, also after the signature check in step 4).** Then lock it (web installer button or `fastboot flashing lock`) and confirm on the device. **Locking wipes all data again.** [**Official**](#tag-official)

> ⚠️ **If verification or flashing fails or is incomplete, do not lock the bootloader.** Leave it unlocked and re-flash; the device may not boot until a verified GrapheneOS image has been flashed successfully. Locking with a missing, incomplete or invalid OS can leave the device unrecoverable, because OEM unlocking can only be re-enabled from a booting OS. Re-download, re-verify, retry, or ask in the official GrapheneOS support channels. [**Advice**](#tag-advice)

6. During first setup, keep the **disable OEM unlocking** toggle on the last screen **checked** (the default). [**Official**](#tag-official)
7. **Verify the installation.** Expect the yellow boot notice; compare the displayed verified-boot key hash with the list on the install page. During setup there must be no "bootloader not locked" warning. If you see it, the installation is incomplete; lock now only if the original flash and verification completed successfully, otherwise do not lock and re-flash (see the warning above). [**Official**](#tag-official) Compare the key hash first (on a separate trusted device against the official list), then pair **Auditor** from a second Android device, then use the device. The comparison happens after locking and is the final check. Pair Auditor immediately after installation, before the device leaves your control; attestation is only meaningful if the pairing happened beforehand. [**Official**](#tag-official) for the pairing model; the ordering is [**Advice**](#tag-advice).
8. **Update immediately** and keep the Stable channel. [**Official**](#tag-official)
9. Turn off USB debugging and wireless debugging. [**Advice**](#tag-advice)

**Remaining risk:** the install page and your computer are trusted components. The CLI method with signature verification reduces trust in the project's web infrastructure but not in your computer or the hardware. Use a computer that you trust and that you do not use for the sensitive work itself.

---

## 4. Hardening settings

Menu names follow current official documentation and change between releases. <a id="verify-menu-paths"></a>[**Verify**](#verify-menu-paths) any path marked so.

For every setting: the recommended cryptophone value, why, what it protects against, what it does **not** protect against, and the usability cost.

### 4.1 Device access

| Setting | Recommended value | Why | Protects against | Does not protect against | Usability cost |
|---|---|---|---|---|---|
| **Screen lock** (Settings → Security & privacy → Device unlock) [**Official**](#tag-official) | Long random passphrase (diceware) or random PIN of 8+ digits; no biometrics | Strong practical defense against guessing; removes the compelled-biometric vector | Casual and forensic guessing, shoulder-surfing with scrambling | Coercion, a device unlocked in your hand, malware in the unlocked state | High: typing the secret often |
| **Auto-lock timeout** | Short, for example 30-60 s with a passphrase or 15-30 s with a short PIN; pick one you will keep. Lock immediately on the power button | Shortens the unlocked window | Opportunistic access to an unattended phone | An attacker who grabs it while unlocked | Frequent re-unlocking; a timeout so short that you weaken your secret is counterproductive |
| **PIN scrambling** | On if you use a PIN | Makes observing the PIN harder; applies to lock screen and SIM PIN [**Official**](#tag-official) | Shoulder-surfing, smudge leaks | Cameras that see digits being pressed on a scrambled pad | Slower entry |
| **Biometrics** | Off | See policy rule 7 | Compelled fingerprint or face unlock | Compelled disclosure of the passphrase (jurisdiction-dependent) | Lose convenience |
| **Lockdown** (power menu) | Know it exists: hold the power button, then tap Lockdown (if no menu appears, check Settings → System → Gestures → Press & hold power button). It temporarily disables biometrics, requires the PIN or password and hides lock-screen notifications (privacygear.nl, a secondary source; GrapheneOS's own pages do not describe it) [**External**](#tag-external). With biometrics off it adds little, and do not count on it returning the phone to the at-rest (BFU) state; powering off is the checkpoint action [**Advice**](#tag-advice) | Disables biometric and smart unlock quickly | Short-notice biometric unlock | Everything else | One extra step |
| **Auto-reboot** (Exploit protection) | 4 hours when traveling, 8-12 hours for a phone carried daily [**Advice**](#tag-advice); official default is 18 h, range 10 min to 72 h [**Official**](#tag-official) | Returns the device to the encrypted at-rest state (BFU, Before First Unlock; explained under Behavioral OPSEC) when unused; does not apply while already in BFU | Forensic extraction of a device left in the after-first-unlock state | Seizure while the phone is in use, a weak secret, or a compromised secure element | After each reboot the Owner profile must be unlocked first, then the communication profile; no messages or notifications arrive until both are unlocked. Pick an interval you will keep |
| **USB-C port** (Exploit protection [**Official**](#tag-official); the usage page also writes "Security & privacy" for the parent menu) | "Charging-only when locked" (default) at minimum; "Charging-only" or stricter if you never use USB data [**Official**](#tag-official) | Blocks new USB connections once locked | USB-based attacks on a locked phone | Attacks while unlocked, or via other radios | Cannot transfer files while locked |
| **Memory tagging (MTE)** (Exploit protection; Pixel 8 and newer) | Enable it for all apps (Settings → Security & privacy → Exploit protection → Memory tagging → Enable by default, per privacygear.nl [**External**](#tag-external)); disable it per app only if an app crashes | GrapheneOS already uses hardware memory tagging for the base OS and known compatible apps and offers the option to use it for all apps [**Official**](#tag-official) | Exploitation of memory-corruption bugs in apps (buffer overflows, use-after-free) | Logic bugs, a compromised OS or hardware, and anything that is not memory corruption | Poorly written apps may crash |
| **Duress PIN/password** (Device unlock, Owner profile) [**Official**](#tag-official) | Optional; decide deliberately (section 10). Requires both a PIN and a password; entering the real credential takes precedence, so no wipe occurs [**Official**](#tag-official) | Irreversibly wipes device and eSIMs when entered; not a general anti-seizure control | An adversary who types credentials into the live device | Extraction that never enters the credential, an already-imaged device, or legal consequences | Risk of accidental, irreversible wipe |

### 4.2 Radios, location and sensors

| Setting | Recommended value | Why | Protects against | Does not protect against | Usability cost |
|---|---|---|---|---|---|
| **Bluetooth** | Off; enable only for a specific accessory; use the "Turn off Bluetooth automatically" timeout (label from the GrapheneOS Settings source) [**Official**](#tag-official); <a id="verify-menu-bt-wifi"></a>[**Verify**](#verify-menu-bt-wifi) the menu location | Reduces proximity attack surface and tracking via nearby devices | Proximity attacks, passive tracking by Bluetooth beacons | A beacon that sees a device you left Bluetooth on for | No wireless accessories by default |
| **Wi-Fi** | Off unless in use; per-connection MAC randomization stays on (default) [**Official**](#tag-official); do not join hidden networks, which reduce privacy [**Official**](#tag-official) | Limits passive tracking and rogue-network exposure | Passive tracking by MAC, rogue hotspots | The Wi-Fi operator seeing your traffic and your IP | Manual toggling |
| **Wi-Fi and Bluetooth scanning** (Settings → Location → Location services) [**Official**](#tag-official) | Off (default) | Scanning runs even when the radios are "off" | Radios staying active in the background | n/a | Slower location lock |
| **Location** | Off by default; "only while using" for a specific need | Reduces location trail | Apps and SDKs collecting location | Network location from the carrier | Maps need a manual toggle |
| **NFC** | Off (Settings → Connected devices → Connection preferences → NFC, per privacygear.nl [**External**](#tag-external)) | Removes a proximity input | Proximity attacks | n/a | No tap-to-pay (not wanted here anyway) |
| **Cellular type** (Settings → Network & internet → SIMs → SIM → Preferred network type) [**Official**](#tag-official) | LTE-only if your carrier works reliably in LTE-only | Disables 2G, 3G and 5G code paths, reducing remote-exploit surface [**Official**](#tag-official) | Remote exploitation through legacy radio code | Interception of calls and texts, carrier metadata, location by the carrier. The project says it is not a confidentiality feature [**Official**](#tag-official) | No fallback in poor coverage; traditional voice calls work only with VoLTE or Wi-Fi calling [**Official**](#tag-official) |
| **SUPL** (Settings → Location) [**Official**](#tag-official) | Keep the GrapheneOS proxy or set to Off | Avoids the carrier's default SUPL server | Leaking coarse location to the carrier's SUPL server | Cell-tower location by the carrier | Slower GNSS fix when Off |
| **eSIM support** (Settings → Network & internet) [**Official**](#tag-official) | Off unless you use an eSIM | Disabled by default; managing eSIMs needs proprietary Google functionality, but not Google Play | n/a | An eSIM has its own identifier and activation can require an account or ID | Extra step to enable when needed |
| **Camera and microphone** | Deny by default; grant per use ("only this time" / "while using") | Limits hot-mic and camera abuse | Silent recording by apps | A compromised OS or hardware | Prompt each time |
| **Sensors permission** (Settings → Security & privacy → More security & privacy) [**Official**](#tag-official) | Disable by default for newly installed apps | Zeroes data for accelerometer, gyroscope, compass and others | Sensor-based fingerprinting and side channels | Other covert channels | A few apps may misbehave |

### 4.3 Permissions and data

| Setting | Recommended value | Why | Protects against | Does not protect against | Usability cost |
|---|---|---|---|---|---|
| **App permissions** | Grant the minimum; review after each install | Smaller blast radius | Over-collection by apps | A trusted app abusing granted data | Occasional breakage |
| **Network permission** [**Official**](#tag-official) | Block for any app that works offline (notes, PDF, authenticator, password manager) | The app sees "network down"; also blocks localhost use between profiles | Telemetry and exfiltration by offline tools | Data leaving by another path you allowed | Apps that sync stop syncing |
| **Contact Scopes** [**Official**](#tag-official) | On for every app that asks for contacts; grant only the single contact, group or data needed; writes are blocked | The app sees an empty contact list by default | Whole-address-book upload | A contact you did grant | Manual granting |
| **Storage Scopes** [**Official**](#tag-official) | On for every app that asks for storage; grant only needed files or folders | Limits file exposure | Whole-storage scanning | Files you did grant | Manual granting |
| **Clipboard** | Treat as readable by the foreground app and the keyboard; avoid copying secrets; use the password manager's autofill where possible. Clipboard blocking to/from the parent profile exists for Private Space in recent releases (release notes 2025-05; setting "Cross-profile shared clipboard" with the option "Disallowed" in the GrapheneOS Settings source) [**Official**](#tag-official), but Private Space is not part of this guide's profile model; <a id="verify-menu-clipboard"></a>[**Verify**](#verify-menu-clipboard) the exact menu path | Clipboard is readable by apps in the foreground | Leaking secrets via the clipboard | Keyloggers or a compromised keyboard | Retyping |
| **Notifications** | Hide sensitive content on the lock screen; do not show message previews | A locked phone should reveal nothing | Shoulder-surfing, glimpsing at a locked phone | Notifications you allowed to show text | Less glanceable |
| **Screenshots** | Never for sensitive material; screenshots are stored and may be backed up | Screenshots persist and travel | Local residue | A recipient photographing their own screen | Habit change |

### 4.4 Browser, DNS, VPN, updates, backups, loss

| Setting | Recommended value | Why | Protects against | Does not protect against | Usability cost |
|---|---|---|---|---|---|
| **Browser** | **Vanadium** in the isolated browsing profile. JavaScript JIT is off by default, with a per-site toggle; extension support is not planned (by design) [**Official**](#tag-official). Keep it that way. [**Advice**](#tag-advice) | Strongest sandbox among common mobile browsers per the project [**Official**](#tag-official); fewer plugins means less fingerprinting | Many browser exploits, extension-based tracking | IP-based tracking, logging into accounts, browser fingerprinting by site | Some sites break with JIT off |
| **Private DNS** (Settings → Network & internet → Private DNS) | **Automatic** (default) when not using a VPN; **Off when a VPN is active** [**Official**](#tag-official) | Automatic gives opportunistic DNS-over-TLS; a hostname forces authenticated DoT. Private DNS is global but VPN settings are per profile, so the two interact badly; the 2025-07 release fixed two VPN leaks [**Official**](#tag-official) | A passive local listener (Automatic mode); active attackers can force fallback [**Official**](#tag-official) | Domains leaking via TLS SNI, destination IPs, the DNS provider seeing your queries. Not an alternative to Tor or a VPN [**Official**](#tag-official) | None in Automatic mode |
| **VPN** | Use only if you can name the threat it addresses (untrusted local network or ISP). Use the official Mullvad or WireGuard app, as the GrapheneOS FAQ recommends [**Official**](#tag-official). Enable **Always-on VPN** and **Block connections without VPN** | Hides destinations and content from the local network and ISP; hides your IP from sites | A hostile Wi-Fi operator or ISP | The VPN provider seeing your traffic (trust shifts), accounts you log into, cell-tower location, calls and SMS. EFF: "A VPN is not a tool for anonymity" [**External**](#tag-external) | Setup and per-profile configuration |
| **Updates** | System Updater enabled, **Stable** channel, reboot to finish [**Official**](#tag-official) | Security fixes are among the most valuable protections | Known vulnerabilities | Unknown (zero-day) vulnerabilities | Occasional restarts |
| **Backups** | **No full-device backup by default.** Keep only: an encrypted copy of the password-manager database, an encrypted authenticator export, and offline recovery codes, stored apart from the device | Backups are an extra copy an adversary can seize | Loss of device = loss of access | A compromised backup medium | Rebuilding after loss |
| **Seedvault** (built-in backup) | Do not use for the sensitive profile unless you need it. If used, use a locally stored encrypted target. The project plans to replace Seedvault because its upstream was taken over by a group not sharing its goals [**Official**](#tag-official) | Avoids a cloud copy | Cloud exposure of device data | A seized backup drive | n/a |
| **Device loss/theft** | Assume it is lost to an adversary until proven otherwise (section 11). No remote-wipe feature is described in the official features, usage or FAQ pages [**Official**](#tag-official); Duress is local only | Plan for the worst | n/a | n/a | n/a |

**Remaining risks of this section:** every setting is a mitigation, not a guarantee. Settings that rely on the secure element or on the OS itself fail if either is compromised. A strict setup that you work around because it is too inconvenient is worse than a slightly looser one you follow.

---

### 4.5 Anti-forensic apps: Wasted, Sentry, and why GrapheneOS Duress is better

This section complements the Duress row in section 4.1. It does not replace it.

**What they are.**

| App | What it does | Source |
|---|---|---|
| **Wasted** | Locks the device and optionally wipes it (factory reset) on a trigger: PanicKit, tile or shortcut, a message with a secret code, a device not unlocked for a set time, a USB data connection while locked, a fake messenger app being launched, or a duress password entered in the companion app "Duress" [**External**](#tag-external) | Wasted README, <https://github.com/x13a/Wasted>; F-Droid, <https://f-droid.org/packages/me.lucky.wasted/> |
| **Sentry** | A "tiny app to enforce security policies": limits failed password attempts, can disable USB data connections and safe boot, and notifies on failed attempts. Same developer account (x13a); Wasted's README points to it for "base security" [**External**](#tag-external) | Sentry README, <https://github.com/x13a/Sentry> |

Both are open source under GPL-3 [**External**](#tag-external). They were widely discussed in the GrapheneOS community; that popularity is not evidence that they are safe to use now [**Advice**](#tag-advice).

**Why they are not recommended.**

| Reason | Detail | Limitation |
|---|---|---|
| Exploited by forensics companies | GrapheneOS stated on 13 June 2024 that forensics companies exploited apps like Wasted and Sentry against users, by abusing their attempt to wipe the device when an attack is detected; GrapheneOS addressed it as part of its duress PIN/password feature and reported it so that Google fixed it across Android (<https://x.com/GrapheneOS/status/1801294115407106186>; a social-media post, not grapheneos.org documentation) [**External**](#tag-external) | The other reasons below stand on their own |
| Reliability | A forum user reports that they are no longer reliable since around Android 15, especially over longer timeframes, because the timers do not always start automatically as they rely on foreground services (<https://discuss.grapheneos.org/d/28627-wasted-sentry>; one community report, not an official statement or a test) [**External**](#tag-external) [**Advice**](#tag-advice). Neither README mentions Android 15. The F-Droid page lists version 1.5.10 from 2022 as the newest, and both READMEs say the architecture will be redesigned because Google changed the DevicePolicyManager API [**External**](#tag-external) | An app whose behavior depends on background services can silently fail when you need it |
| Sensitive permissions | Wasted: Device Admin, Foreground Service and Receive Boot Completed (Wasted README). Sentry: Device Admin, Device Owner (set via ADB), notification listener and query-all-packages (Sentry README) [**External**](#tag-external) | Each is a privileged component on a device that should have a tiny app list (section 7) |
| Attack surface | Third-party code with high privileges adds surface without a reliable benefit over the built-in feature [**Advice**](#tag-advice) | Open source does not by itself make an app safe to run with these privileges |

**Why GrapheneOS Duress is better.**

| Property | Duress | Limitation |
|---|---|---|
| Built into the OS | No third-party app to install, update or trust [**Official**](#tag-official) | It is still an OS feature you must configure deliberately (section 4.1) |
| Wipe | Irreversible; also removes installed eSIMs [**Official**](#tag-official) | Irreversible means irreversible, including after an accidental trigger |
| Credentials | Requires both a PIN and a password; entering the real credential takes precedence, so no wipe occurs [**Official**](#tag-official) | It only helps when the adversary types credentials into the live device |
| Permissions and attack surface | No extra app permissions or app attack surface [**Advice**](#tag-advice) | It is not a proof of absence of flaws |
| Reboot, interruption, where it is accepted | The wipe does not require a reboot and cannot be interrupted; it triggers when the duress credential is entered anywhere the device credentials are requested, on the lock screen and in OS prompts [**Official**](#tag-official) (GrapheneOS features page, <https://grapheneos.org/features>) | Once triggered there is no undo, including after an accidental entry [**Advice**](#tag-advice) |

**Legal and ethical warning.** Using a duress PIN to wipe a device during a lawful inspection or a compelled unlock can have serious legal consequences, for example obstruction charges in the US [**Advice**](#tag-advice). Rules differ by country (section 10.2). Get local legal advice before relying on any duress or wipe feature. Duress is not a "get out of jail free" card: it destroys your own data, and it can look like destruction of evidence.

**Recommendation.** Do not install Wasted or Sentry on a cryptophone [**Advice**](#tag-advice). They are intentionally not in the app lists of this guide. If your threat model justifies it, use the built-in Duress PIN/password instead [**Official**](#tag-official), and accept the trade-off: once triggered, the wipe cannot be undone.

---

## 5. Profiles and compartments

### 5.1 Recommended minimal structure

| Profile | Contents | Rules |
|---|---|---|
| **1. Owner** | System management only: updates, App Store, settings | No social apps, no personal accounts, no browsing unless necessary. The Owner profile stores sensitive system-wide data and must be unlocked first after reboot [**Official**](#tag-official) |
| **2. Secure communication** | Signal (or another appropriate messenger), authenticator, password manager, secure notes, minimal contacts | Only the apps in section 7. Network blocked for offline apps |
| **3. Isolated browsing (optional)** | Browser only | No persistent accounts, no contacts, no personal files. End the session when done |

### 5.2 What profiles do and do not do

- Profiles separate apps, app data, keys and most settings. **End session** (power menu or user switcher) fully purges that profile's keys from memory and puts it at rest. It is not possible for the Owner profile without a reboot. [**Official**](#tag-official)
- **Profiles do not create anonymity.** All profiles share the same hardware, SIM, IMEI, IP address and your habits. A reused phone number, email, name, contact, file or writing style links identities again. [**Advice**](#tag-advice)
- **Wi-Fi and Bluetooth can correlate profiles.** The same radios and the same networks are used by all profiles.
- **A VPN configured in one profile does not automatically solve every network-leak scenario.** Each profile has its own VPN configuration, while Private DNS is global. [**Official**](#tag-official) Verify behavior per profile (section 13 checklist).
- **Do not move sensitive data casually between profiles.** Avoid shared storage, shared clipboard and cross-profile notifications.
- **Each profile has its own lock method; give every profile its own strong secret.** A weak secret on one profile undermines that compartment. Profiles can have different unlock methods [**Official**](#tag-official); the recommendation is [**Advice**](#tag-advice).
- GrapheneOS raises the profile limit to 31 secondary profiles plus a guest, and secondary profiles can be set not to run in the background. [**Official**](#tag-official) Use as few as you need.

### 5.3 Remaining risks

Profiles are compartments for data, not for identity. For a high-risk role, a **separate device, separate SIM/eSIM and a separate network usage pattern** are the realistic boundary. Profile separation alone is compartmentalization, not a complete boundary. [**Advice**](#tag-advice)

---

## 6. Sandboxed Google Play

- **Do not install Sandboxed Google Play by default** on a cryptophone.
- Install it **only** if a specific required app cannot work otherwise, and if you accept the Google dependency.
- If installed, **isolate it in a separate profile**, never in the Owner profile. The official guide calls the Owner-profile install "the simplest" but it is less isolated. [**Official**](#tag-official) [**Advice**](#tag-advice)
- **Never log into a personal Google account.** A Google account links the profile to an identity at Google. Signing in is optional unless you need Play Store installs, in-app purchases or account-dependent features. [**Official**](#tag-official) Account creation often requests phone verification. [**Advice**](#tag-advice)
- A separate profile limits data access but does not prevent Google from correlating the account through IP address, device characteristics, timing or account activity. [**Advice**](#tag-advice)
- Installing **Google Play services** from the App Store installs Google Play services and the Google Play Store; both run as ordinary sandboxed apps with no special privileges. [**Official**](#tag-official)
- Prefer apps that do not require Google Play.

**Remaining risk:** even in a separate profile, Google likely sees the apps you install through it and the device information it receives. [**Advice**](#tag-advice)

---

## 7. Apps

### 7.1 Rules

- Every app needs a documented purpose, source and permission list.
- Prefer open-source, actively maintained apps.
- Install only from these sources, in this order of preference: the **GrapheneOS App Store**; the developer's **official verified source** (verify the signature); **Accrescent** (available in the GrapheneOS App Store; in alpha [**External**](#tag-external)); and **F-Droid** only as a fallback for apps unavailable elsewhere. Do not use Aurora Store or another Google Play frontend.
- Verify publisher and signature where possible (for example a published signing-certificate fingerprint).
- No beta, modded, cracked or "privacy fork" apps without a strong reason.
- Review permissions after installation; remove apps that are no longer needed.

### 7.2 Source notes

| Source | Note |
|---|---|
| **GrapheneOS App Store** | Distributes GrapheneOS's own apps and, optionally, Sandboxed Google Play [**Official**](#tag-official) |
| **Accrescent** | Security and privacy focused app store, currently in alpha [**External**](#tag-external). Its own site says it can be downloaded from the GrapheneOS App Store, "the recommended approach for GrapheneOS users" [**External**](#tag-external). It updates apps automatically, unattended and without privileges on Android 12 and later, and needs no account [**External**](#tag-external). The GrapheneOS app repository contains it (package `app.accrescent.client`) [**Official**](#tag-official) |
| **F-Droid** | Open-source apps. Apps not set up for reproducible builds are signed with per-app F-Droid keys; for developer-signed reproducible apps F-Droid publishes a version only if its build matches the developer's [**External**](#tag-external) (F-Droid documentation). Updates can lag behind the developer |
| **Developer's official source** | Verify the signing-certificate fingerprint or checksum from a channel separate from the download. Keep track of updates yourself |

**Where Signal comes from:** Signal distributes through Google Play and as a direct APK at signal.org/android/apk, which publishes the signing-certificate fingerprint [**External**](#tag-external); it is not in F-Droid's main repository [**External**](#tag-external) and not in the GrapheneOS app repository [**Official**](#tag-official). Whether Accrescent offers it is <a id="verify-signal-accrescent"></a>[**Verify**](#verify-signal-accrescent) (Accrescent publishes no app list). If you must install an APK from the developer's site, verify its signing certificate, grant "Install unknown apps" to one app only (the browser or file manager you used) and revoke it afterwards. Manual APK installation requires manual re-download and signature verification for updates; it does not provide automatic updates (signal.org/android/apk, which gives the SHA-256 fingerprint and an apksigner check) [**External**](#tag-external). Re-grant the permission for each new release; otherwise the device runs outdated software. The same applies to any app that is not in your chosen stores. [**Advice**](#tag-advice)

> ⚠️ Never sideload from random APK sites. Root (Magisk), LSPosed and Xposed remove the security model.

### 7.3 Mandatory categories

| Category | Choice | Why | Remaining risk |
|---|---|---|---|
| **Browser** | **Vanadium** (built-in) | Hardened Chromium, also the system WebView [**Official**](#tag-official) | Does not hide your IP or stop fingerprinting by itself |
| **Secure messenger** | **Signal** | End-to-end encrypted, audited, widely used. Registration requires a phone number; usernames can hide your number from other users but do not remove the requirement. [**External**](#tag-external) (EFF; Signal blog post on phone-number privacy and usernames) | Number-based registration links the account to a SIM; metadata exposure remains; the other person's device can compromise the chat |
| **Password manager** | **KeePassDX** (GPL-3.0, local database) [**External**](#tag-external) | No cloud account needed; local database | A stolen database with a weak master secret; Android app sandbox only |
| **2FA/authenticator** | **Aegis** (GPL-3.0) [**External**](#tag-external) | Open source, encrypted vault | A lost vault without a backup; a compromised phone reveals codes |
| **Secure notes** | **Entries inside the KeePassDX database** | No extra app and no extra account | The same single point of failure as the password database |
| **VPN client, only if justified** | **Mullvad** official app, or the official WireGuard app [**Official**](#tag-official) | The two apps the GrapheneOS FAQ recommends; Mullvad's app is open source (GPL-3.0) [**External**](#tag-external) | Trust shifts to the provider; choice depends on jurisdiction, logging, payment and threat model |
| **File transfer, only if justified** | Prefer sending the file through the end-to-end encrypted messenger. No extra app | Fewer apps | File metadata (EXIF, document properties) must be stripped first |

### 7.4 Optional categories

| Category | Choice | Notes |
|---|---|---|
| **Encrypted cloud/storage** | **Cryptomator** [**External**](#tag-external) | Dual-licensed (GPLv3 and commercial) [**External**](#tag-external). Google Drive is supported in the Google Play Store and APK Store variants but not in the F-Droid variants (proprietary dependencies), and the main F-Droid build also lacks clouds that need an API key [**External**](#tag-external); whether the Accrescent build supports Google Drive is <a id="verify-cryptomator-accrescent"></a>[**Verify**](#verify-cryptomator-accrescent) (Cryptomator's documentation does not say). Only the APK Store variant has an automatic updater built in; the Play Store, F-Droid and Accrescent variants do not, or update differently through their stores [**External**](#tag-external). All variants are free with read-only vault access; writing needs a paid license key [**External**](#tag-external). Encrypting does not hide that you use cloud storage |
| **Maps, only if needed** | **Organic Maps** (Apache-2.0) [**External**](#tag-external) | Works offline. Its README says the project is far from financial sustainability, so check its maintenance status before relying on it |
| **PDF/document reader, only if needed** | Built-in **PDF Viewer** [**Official**](#tag-official) | Block Network; documents carry metadata |
| **Tor Browser, only if needed** | **Tor Browser for Android** from the Tor Project [**External**](#tag-external) | See section 9; the GrapheneOS project says its security is weak compared to Vanadium and that Tor makes users more of a target [**Official**](#tag-official) |

Apps explicitly **not** recommended: more messengers, more browsers, social apps, cloud-synced note apps that need an account, and any "privacy" app without a documented need.

**Remaining risk:** each app is added trust and attack surface. The safest list is the shortest list.

### 7.5 App store comparison

Every store below installs apps into the normal app sandbox. The differences are whether an account is needed, how updates arrive and whom you have to trust. Facts about third-party stores are tagged [**External**](#tag-external) and come from each project's own documentation; the recommendations are this guide's judgment.

| Store | Account required? | Google dependency | Update mechanism | App selection (size, quality) | Security model | Recommendation: daily driver / cryptophone |
|---|---|---|---|---|---|---|
| **GrapheneOS App Store** | No account is mentioned as a requirement in the GrapheneOS documentation [**Official**](#tag-official) | None for the store itself; it can also install Sandboxed Google Play, which is optional [**Official**](#tag-official) | Updates the apps from its repository in the background, including the Sandboxed Google Play components [**Official**](#tag-official) | Small: GrapheneOS's own apps (for example Camera, PDF Viewer, Auditor, Vanadium), the Sandboxed Google Play components and a few others such as the Accrescent client [**Official**](#tag-official) | First-party app repository and client maintained by the GrapheneOS project and integrated into the OS [**Official**](#tag-official) | Daily driver: first choice. Cryptophone: first choice; install Sandboxed Google Play only if a required app cannot work otherwise (section 6) [**Advice**](#tag-advice) |
| **Accrescent** | No account required [**External**](#tag-external) | None stated by the project [**External**](#tag-external) | Automatic, unattended, unprivileged updates on Android 12 and later [**External**](#tag-external) | Small curated catalogue; the project is in alpha [**External**](#tag-external) | App signing key pinning for first-time installs, signed repository metadata, and no remote APK signing, so developers keep control of their signing keys [**External**](#tag-external) | Daily driver: use it for the apps it carries. Cryptophone: the same. Install the client from the GrapheneOS App Store, as Accrescent's own site recommends for GrapheneOS users [**External**](#tag-external). In the source order of 7.1 it ranks below verified developer releases only because of its alpha status [**Advice**](#tag-advice) |
| **F-Droid** | No account needed; F-Droid says it does not track what you install [**External**](#tag-external) | No Google dependency stated; an independent repository of free and open-source apps [**External**](#tag-external) | Through the F-Droid client; speed depends on the app, because F-Droid builds on its own timeline and some apps are outdated or lag behind the developer [**Advice**](#tag-advice) | Large catalogue of free and open-source apps; quality and update speed vary by app and repository [**Advice**](#tag-advice) | Apps are checked for security problems before they are added [**External**](#tag-external). For apps with reproducible builds F-Droid publishes the developer's signature after verifying the build; other apps are signed with F-Droid's own keys [**External**](#tag-external) | Daily driver: fallback for apps the stores above do not carry; check that the app is maintained. Cryptophone: fallback only (rule in 7.1) [**Advice**](#tag-advice) |
| **Aurora Store** | Yes, a Google account is needed. By default it fetches shared account credentials from Aurora Store's service (shared dummy accounts handed out through token dispensers); you can also sign in with your personal Google account [**Official**](#tag-official) | Full: it is an alternative frontend to the Google Play Store [**Official**](#tag-official) | Updates the Play apps it installed. GrapheneOS accepts updates of Google Play services, the Google Services Framework and the Play Store only from its own App Store or the Play Store itself, so do not use Aurora for those [**Official**](#tag-official) | The whole Play catalogue, mostly closed source [**Advice**](#tag-advice) | Developer-signed Play apps, but installs run through Google under a shared or a personal account. Shared dummy accounts are not anonymity: you rely on the dispenser service, the account is shared with many other users, and Google can still correlate device information and installs; a personal account ties installs to you [**Advice**](#tag-advice) | Daily driver: last resort, only in a separate profile and never with your main Google account. Cryptophone: do not use [**Advice**](#tag-advice) |
| **Obtainium** | No store account; it reads the developers' own release pages (for example GitHub, GitLab or F-Droid) [**External**](#tag-external) | None, unless the app itself needs Google | Checks the release pages you configured, notifies you of new releases and installs them [**External**](#tag-external); it is not a store with its own review | Whatever apps publish APKs on supported release pages; you choose and configure each source yourself | Only as strong as your trust in each source and your verification: it does not make an unsigned or compromised release safe. Obtainium itself publishes a signing-certificate fingerprint and a PGP key for verification (Obtainium README, section "Installation") [**External**](#tag-external); its source is on GitHub (<https://github.com/ImranR98/Obtainium>) | Daily driver: optional helper for apps that are only distributed as APKs and that the stores above do not carry. Cryptophone: not by default; it adds an app with the "Install unknown apps" permission and network access, so use it only for a documented need and verify each source [**Advice**](#tag-advice) |
| **Manual APK download** | No store account; the developer's site decides | None, unless the app itself needs Google | No automatic updates: every update needs a manual re-download and signature verification (for Signal, signal.org/android/apk gives the SHA-256 fingerprint and an apksigner check) [**External**](#tag-external) | Whatever the developer publishes; not every app offers an APK | Depends entirely on your verification: compare the signing-certificate fingerprint or checksum through a channel separate from the download, grant "Install unknown apps" to one app only and revoke it afterwards [**Advice**](#tag-advice) | Daily driver: only when an app is available nowhere else. Cryptophone: only for apps unavailable elsewhere (for example Signal); verify the signature and update by hand [**Advice**](#tag-advice) |

**Remaining risk:** the store you choose changes who learns which apps you install and how quickly fixes reach you. It does not make an app trustworthy, and no login mode of any Google-based store makes you anonymous.

---

## 8. Communication OPSEC

- **Use end-to-end encrypted messaging.** Check who can still see **metadata**: contact graph, timing, IP address, phone number.
- **Verify safety numbers or safety keys** where the app supports it. EFF describes comparing the digits or QR code in person or by phone and marking the contact verified. [**External**](#tag-external) A changed number usually means a new phone or a reinstall (Signal blog), but confirm through another channel. [**External**](#tag-external)
- **Do not trust "encrypted" claims blindly.** Ask what is encrypted, between whom, and what the provider still knows.
- **Do not reuse phone numbers across identities.**
- **Do not add contacts from your personal life** to a sensitive identity.
- **Do not discuss operational details in group chats.** Larger groups mean more devices that can leak.
- **Disappearing messages are an additional control only.** Signal states they are "not for situations where your contact is your adversary" and that a recipient can photograph the screen. [**External**](#tag-external) Signal backups exclude only view-once messages and messages due to disappear within 24 hours, so messages with longer timers can be in a backup [**External**](#tag-external); use short timers or no backups on this device.
- **The other person's device can compromise the conversation.** End-to-end encryption protects the transport, not the endpoints.
- **Do not screenshot sensitive conversations.** Do not forward sensitive material casually.
- **Strip metadata** (EXIF, document properties) before sharing files.

**Remaining risk:** a compromised endpoint, a screenshot, a forwarded message or a traffic-analysis observer defeats encryption's protection of content or of the fact of communication.

---

## 9. Network OPSEC

### 9.1 Mobile network

- A SIM or eSIM identifies you to the carrier. The carrier knows which towers your phone uses and when; EFF says there is no way to hide from this tracking while the phone is powered on [**External**](#tag-external), and the network observes SIM and device together [**External**](#tag-external).
- **Identity correlation via the carrier:** carrying or powering on this device together with your personal phone, at the same times and places, shows the same towers; buying the SIM and device together or with traceable payment, top-ups, and mandatory SIM registration or ID rules (country-specific) can all link the line to you. The IMEI stays fixed when the SIM changes. The premise that cell towers locate phones is described by the Freedom of the Press Foundation. [**External**](#tag-external) The correlation scenarios are [**Advice**](#tag-advice).
- An eSIM has its own identifier and often needs an account, ID or payment at activation. [**Advice**](#tag-advice)
- Calls, SMS and VoLTE are carrier services; a VPN does not cover them.
- LTE-only mode reduces remote exploitation of legacy radio code. It is not a substitute for end-to-end encrypted calls and texts. [**Official**](#tag-official)
- EFF reports that disabling 2G can protect against some cell-site simulators; it has not seen concrete evidence of their use at protests. [**External**](#tag-external) Do not claim more.
- **Airplane mode does not make a phone untrackable.** Freedom of the Press Foundation notes it may not block location services, and EFF notes apps may store GPS data and send it later; turning the phone off is the strongest step available (FPF: "the best technical step"). No software state is proof, and a powered-off phone can still have been located where it was last on. [**External**](#tag-external)
- **Wi-Fi-only** (no SIM) removes the SIM-based link to a carrier, not IP or Wi-Fi exposure. A phone without a SIM can still place emergency calls where national rules allow it (Android requires emergency numbers to work without a SIM) [**External**](#tag-external); whether the IMEI is visible to the network then is <a id="verify-imei"></a>[**Verify**](#verify-imei). Wi-Fi must be on for such a device by necessity (relaxing rule 11), and some services need a phone number at registration.

### 9.2 Public Wi-Fi and captive portals

- Public Wi-Fi exposes your traffic to the operator and shows your IP. Use it only for traffic you would accept the operator seeing; do the same for updates and app installs, and avoid your home Wi-Fi if correlation matters (section 9.5). [**Advice**](#tag-advice)
- **Captive portals** may ask for a phone number or email address. [**Advice**](#tag-advice) EFF warns (2017 article) that they resemble a man-in-the-middle, train users to ignore certificate warnings and can tie activity to a login or identity. [**External**](#tag-external) With **Block connections without VPN** active, a portal login cannot be completed; lift the block temporarily only if you accept that, or avoid the portal. [**Advice**](#tag-advice)
- CCTV, payment records and location patterns can still link a person to a place.
- A VPN hides destinations and content from the local network, not the fact that a VPN is in use.

### 9.3 VPN, Tor, DNS

| Tool | Helps with | Does not help with |
|---|---|---|
| **VPN** | Untrusted local network or ISP; hides your IP from sites | The provider seeing traffic; cell location; accounts you log into; calls and SMS. "A VPN is not a tool for anonymity"; "If you are interested in increased anonymity, Tor is a better solution than a VPN" [**External**](#tag-external) |
| **Tor Browser** | Hides your IP from sites via multi-hop routing | Logging in or revealing your name defeats it ("they know who you are"); Tor protects only apps configured to use it; Tor Browser rounds window sizes to limit fingerprinting and resizing weakens that, so keep the default window size ([**Advice**](#tag-advice)); do not install extra add-ons or use other browsers with Tor [**External**](#tag-external). On mobile the project calls its security weak [**Official**](#tag-official) |
| **Private DNS** | Opportunistic or authenticated DNS encryption | Not an alternative to Tor or a VPN; off when a VPN is active [**Official**](#tag-official) |

**Tor is not for everything.** It is slow, fingerprintable and does not make a non-browser app anonymous. The Tor Project offers Tor VPN (beta) to route other apps and says the beta "should not be used for sensitive activities" [**External**](#tag-external); Orbot is a Guardian Project app. A GrapheneOS maintainer wrote in the project's issue tracker (2020) that Orbot is poorly implemented and maintained and that the project will not fork or bundle it [**Official**](#tag-official); the FAQ and usage pages name no Tor app, and the project's stance on Tor VPN is <a id="verify-tor-vpn"></a>[**Verify**](#verify-tor-vpn) (not stated in the sources checked).

### 9.4 Bluetooth and nearby devices

- Leave Bluetooth off. Nearby trackers and beacons can log a device that advertises. [**Advice**](#tag-advice)
- Do not pair this device with accessories that are linked to your personal identity.

### 9.5 Never mix identities over the network

Do not log into personal accounts on this device, do not open personal links, and do not use the same home Wi-Fi for the sensitive identity and for your personal one if correlation matters.

**Remaining risk:** the carrier, the Wi-Fi operator, the VPN provider and the destination server each see a slice. No tool in this section removes all of them at once.

---

## Behavioral OPSEC / Verhaltens-OPSEC

The settings in section 4 protect the device. This section covers what you do with it, because identities are usually linked by habits, not by technical flaws. Every recommendation below has a stated limitation, and none of them makes you anonymous. Sources are GrapheneOS documentation [**Official**](#tag-official), named external primary sources such as EFF Surveillance Self-Defense, Freedom of the Press Foundation and Tor Project [**External**](#tag-external) (see the Useful websites section), and this guide's judgment [**Advice**](#tag-advice). Anything not confirmed is [**Verify**](#tag-verify).

### SIM / eSIM discipline

| Situation | Do | Why | Limitation |
|---|---|---|---|
| Choosing connectivity | Use a dedicated SIM or eSIM for this identity, or go Wi-Fi-only if you can live without calls, SMS and mobile data [**Advice**](#tag-advice) | A dedicated line is not linked to your normal phone; Wi-Fi-only removes the SIM-based link to a carrier | A SIM still ties the line to a carrier and to registration and payment records. Wi-Fi-only still exposes your IP address and the Wi-Fi networks you use, and some services need a phone number at registration |
| Reusing a SIM or eSIM across identities | Never (see policy rule 5) | One SIM is one IMSI and one number at the carrier; every identity that uses it can be linked by the carrier and by anyone who knows the number [**Advice**](#tag-advice) | Separate SIMs can still be linked through the other items in this section |
| IMSI/IMEI pairing | Do not move the SIM between phones, and do not put an old SIM into a new phone | The network observes both the SIM and the device together, so moving a SIM to another device offers minimal protection (EFF) [**External**](#tag-external) | A pairing already logged cannot be undone; a new SIM in an old phone links in the same way |
| eSIM | Treat an eSIM like a SIM | An eSIM has an EID that identifies its eUICC hardware (Android documentation) [**External**](#tag-external); activation often needs an account, ID or payment, so it is not more anonymous [**Advice**](#tag-advice) <a id="verify-esim"></a>[**Verify**](#verify-esim) (no primary source found for the account, ID or payment part). eSIM support is off by default in GrapheneOS [**Official**](#tag-official) | A Duress wipe also removes installed eSIM profiles [**Official**](#tag-official); re-downloading one depends on the carrier |
| Removing or disabling the SIM | Remove the SIM or disable the eSIM when you do not need cellular and want to avoid the carrier link | Stops SIM-based registration on the network [**Advice**](#tag-advice) | Emergency calls can work without a SIM where national rules allow it [**External**](#tag-external); whether the IMEI is visible to the network then is [**Verify**](#verify-imei); Wi-Fi and IP exposure remain |
| Prepaid or "anonymous" SIM | Understand the limits before relying on one | Prepaid reduces contract and billing links only | Most countries require ID to buy a prepaid SIM (EFF) [**External**](#tag-external); the exact rules are country-specific [**Verify**](#verify-sim-rules); buying with a card, buying together with the phone, topping up with a traceable payment, and carrying it next to your personal phone all create trails [**Advice**](#tag-advice) |
| Phone number | Never reuse your personal number for a sensitive identity | The number links accounts, including your messenger account | Signal registration requires a number; usernames only hide it from other users [**External**](#tag-external) |

### When to turn the phone off

**BFU and AFU.** Before First Unlock (BFU) is the state after boot until you unlock for the first time: data is at rest and the profile keys are not in memory. After First Unlock (AFU) the keys are in memory and more is exposed. GrapheneOS auto-reboot returns a locked device to the at-rest state after a set time and does not apply while the device is already in BFU. [**Official**](#tag-official)

| When | Do | Why | Limitation |
|---|---|---|---|
| Before sensitive locations or meetings | Power the phone off fully before you arrive, not at the door [**Advice**](#tag-advice) | A powered-off phone produces no new radio activity and no new location trail | The carrier and any other observer still see where and when the phone went offline, and a habit of switching off at the same place is itself a signal [**Advice**](#tag-advice) |
| Before borders and high-risk checkpoints | Power off completely, and start the phone only in a place you trust [**Advice**](#tag-advice). EFF's US border material makes the same point [**External**](#tag-external) (US-specific, see section 10) | A fully powered-off device is in BFU | Does not stop a search of the device; the rules differ by country [**Verify**](#verify-legal) |
| When it is not actively needed | Keep it off | Less location trail, less exposure | You receive no messages or notifications while it is off; do not use this rule if you must be reachable |
| Auto-reboot | Keep it on (section 4.1) | Returns an unused device to BFU even if you forget | It is a partial mitigation only: it does not help during a seizure that happens before the timer runs out, and it does not replace a manual power-off [**Advice**](#tag-advice) |

**Powered off is not "untrackable".** Freedom of the Press Foundation calls turning the device off the best technical step against location tracking [**External**](#tag-external). It cannot undo location history that already exists. FPF notes that in rare circumstances Wi-Fi and Bluetooth signals can continue to be emitted even when a device is powered off [**External**](#tag-external), and EFF notes that malware could make a phone pretend to power off [**External**](#tag-external). Airplane mode is weaker: it may not block location services, and apps can store location and send it later [**External**](#tag-external).

**Faraday bags.** A bag can be useful when you cannot leave a device behind and want to block radio signals while it is inside; FPF lists it as an option for the strictest location protection [**External**](#tag-external). It gives a false sense of security when you assume it works without testing it, when it is not fully closed, or when you think it protects against a compromised device or fixes bad habits. FPF states no limits, so the limits above are [**Advice**](#tag-advice); FPF also notes that leaving the device behind is the only foolproof method [**External**](#tag-external). It is no substitute for powering off.

### What NOT to do

| Do not | Why | Limitation |
|---|---|---|
| Log into old personal accounts (Google, social media, banking) | One login ties the device to your real identity | A new account is a new trail; accounts you create still need a clean email, number and payment method |
| Reuse usernames, emails, profile pictures or recovery contacts | Reuse is a common way identities are linked | Writing style, timing and contacts can still link identities |
| Add real-name contacts casually | Contact graphs identify people | When a real-name contact is necessary, use Contact Scopes (section 4.3); the contact still knows who you are |
| Discuss operational details in group chats | More members mean more devices that can leak | End-to-end encryption does not protect against a member's compromised device |
| Screenshot or forward sensitive material casually | Copies persist and travel beyond your control | Disappearing messages do not prevent a recipient from photographing the screen [**External**](#tag-external) |
| Use the same payment method for sensitive and personal purchases | Payment records link identities | Any payment method has its own records; cash has limits too (CCTV, serial numbers) [**Advice**](#tag-advice) |
| Install apps "just to try" | Each app adds trust and attack surface (section 7) | Uninstalling does not undo what the app already collected |
| Keep saved or personal Wi-Fi networks, or join hidden ones | Hidden networks are broadcast when your phone scans for them [**Official**](#tag-official); saved personal networks tie the device to places you are linked to [**Advice**](#tag-advice) | Joining any Wi-Fi still shows your IP address and timing to the operator; MAC randomization does not hide behavior |
| Use Bluetooth accessories linked to your personal devices | Pairing links device identities | Bluetooth beacons and nearby devices can still observe a device that is advertising [**Advice**](#tag-advice) |
| Rely on "deleted" data as protection | Deleted data can remain in backups, caches and recipients' devices | Full storage encryption protects data at rest, not data that has already been copied elsewhere [**Advice**](#tag-advice) |

### Daily habits

| Habit | Why | Limitation |
|---|---|---|
| Keep the device off when not needed | Less exposure and location trail | You miss messages; choose an interval you will actually keep |
| Use a strong passphrase, not just biometrics (section 2) | Resists guessing and compelled biometric unlock | It does not help once the phone is unlocked in your hand |
| Keep auto-reboot on | Returns the device to BFU | Partial mitigation only (see above) |
| Check for updates regularly | Security fixes are among the most valuable protections [**Advice**](#tag-advice) | Does not stop unknown vulnerabilities |
| Review installed apps and permissions weekly | Catches drift and forgotten apps | A trusted app can still misuse what you granted |
| Use disappearing messages as an extra layer | Reduces what remains on devices | "Not for situations where your contact is your adversary" and the recipient can photograph the screen [**External**](#tag-external) |
| Verify safety numbers with contacts | Detects a changed key | EFF describes comparing the digits or QR code in person or by phone [**External**](#tag-external). A changed number usually means a new phone or a reinstall (Signal blog); confirm through another channel [**External**](#tag-external) |
| Keep the device physically secure and never leave it unattended | Physical access defeats many controls | Even a locked, attended device can be taken; treat a device out of your control as untrusted (section 11) |

### Travel-specific behavior

Section 10 has the full travel and border detail. In day-to-day behavior:

- **Decide before travel what must be on the device.** Remove the rest, including chat and browsing histories where practical [**External**](#tag-external) (EFF's 2025 journalist checklist, US-specific). Limitation: anything left on it can be read if the device is searched.
- **Consider a separate travel device or a clean profile.** Limitation: EFF's 2017 US border guide warns that unusual or wiped devices could attract suspicion and questions [**External**](#tag-external) (US-specific), and it still has a SIM and an IMEI.
- **Power off before borders and checkpoints.** Limitation: it does not stop the search itself.
- **Border searches may happen; do not carry what you cannot afford to lose or have read.** Rules differ by country [**Verify**](#verify-legal). Limitation: no setting makes a seized device safe.
- **Do not rely on hidden files or "deleted" data.** Limitation: forensic tools can recover more than most users expect [**Advice**](#tag-advice).
- **Have a recovery plan for lost, seized or compromised devices** (section 11), with recovery codes offline and separate from the device. Limitation: a plan helps only if you rehearse it.

### Identity separation in practice

- **One device equals one identity, or strictly separated profiles.** Limitation: all profiles share hardware, SIM, IMEI, IP address and your habits [**Official**](#tag-official) (profile isolation) [**Advice**](#tag-advice) (the limits).
- **Never mix a sensitive and a personal identity in the same profile.** Limitation: a profile separates data, not the person using it.
- **Use a separate email address, phone number, username and profile picture per identity.** Limitation: you must keep them separate every time; one slip links them.
- **Do not cross-share files, clipboard content or notifications between identities.** Limitation: a screenshot or a copied line is enough to cross the boundary.
- **Metadata can correlate identities even with technical separation.** Timing, location, contacts and writing style are all signals [**Advice**](#tag-advice); signing into an account while using Tor tells the site who you are [**External**](#tag-external).

**Remaining risk:** Behavior is the weakest link: it takes discipline every day, and a single mistake can undo months of separation. For a high-risk role, a separate device, a separate SIM or eSIM and a separate network usage pattern are the realistic boundary; this section reduces exposure, it does not remove it.

---

## 10. Travel and physical security

This is not legal advice. Search, seizure and compelled-unlock rules differ by country and change over time. [**Verify**](#verify-legal) the rules of every country you enter or transit. The EFF border material cited here is a US baseline only; EFF SSD and FPF border guidance covers the US only, and no primary source in scope covers other countries.

### 10.1 Before travel

- **Minimize data.** Decide what must be on the device and remove the rest, including chat and browsing histories where practical. [**External**](#tag-external) (EFF's journalist-travel checklist, US-specific)
- **Remove unnecessary apps.**
- **Use a travel device or a clean profile** if appropriate; do not carry sensitive data you cannot afford to lose or have read. EFF's 2017 US border guide warns that unusual or wiped devices could attract suspicion and questions. [**External**](#tag-external) (US-specific)
- **Update and reboot.** Set a short auto-reboot interval.
- **Back up** only what you need, encrypted, and keep the backup elsewhere.
- **Recovery codes** stay offline, encrypted and separate from the device.

### 10.2 At borders and checkpoints

- **Power the device off fully** before screening; EFF notes that a fully powered-down device restores disk encryption. [**External**](#tag-external) (US-specific checklist)
- **Use strong authentication.** Long, unpredictable, alphanumeric secrets are recommended; EFF's 2025 checklist advises deciding in advance whether you will unlock and, if you do, typing the passcode yourself and asking to be present (US-specific). [**External**](#tag-external)
- **Biometrics:** EFF says there is less protection against compelled face and fingerprint unlocking than against compelled password disclosure in the protest context. [**External**](#tag-external) Keep biometrics off. Jurisdiction-dependent. [**Verify**](#verify-legal)
- **Understand border-search realities:** in the US, non-citizens who refuse a search request may be denied entry (EFF checklist; US-specific). [**External**](#tag-external)
- Under US CBP policy, officers may search only data resident on the device, not live cloud content (US-specific; other countries differ). EFF's 2025 checklist says officers must put the device in airplane mode or otherwise disconnect it; CBP's current border-search directive is No. 3340-049B, dated 01/28/2026 (<https://www.cbp.gov/document/directives/cbp-directive-no-3340-049b-border-search-electronic-devices>), and EFF doubts practice always matches policy. [**External**](#tag-external) <a id="verify-cbp"></a>[**Verify**](#verify-cbp) (only the directive's title and date could be confirmed; its text is a scanned PDF that could not be read) Airplane mode does not protect data already on the device and does not make the phone untrackable (section 9.1).
- **Duress/wipe:** do not rely on it. Wiping data during a compelled unlock can be treated as obstruction in some jurisdictions, and refusing a passcode can itself be an offence in some jurisdictions. [**Verify**](#verify-legal) Get local legal advice first.

### 10.3 Physical measures

- **Do not rely on hidden files or "deleted" data** as protection.
- **Faraday bags:** Freedom of the Press Foundation lists them as an option for the strictest location protection if you cannot leave a device behind. [**External**](#tag-external) FPF presents it as a last-resort option and states no limits; you cannot easily verify that a bag works. [**Advice**](#tag-advice) A Faraday bag does not fix OPSEC; it only blocks radio signals while the device is inside.
- Avoid public USB charging; use your own charger and cable.
- Do not leave the device unattended. If it was out of your control, treat it as untrusted and check Auditor attestation. [**Advice**](#tag-advice)

**Remaining risk:** a determined adversary with physical control of an unlocked or after-first-unlock device may succeed regardless. Travel advice reduces exposure; it does not guarantee safety.

---

## 11. Incident response

For each scenario: immediate actions, what to assume is compromised, what to rotate, what not to do, and when to stop using the device. These are [**Advice**](#tag-advice) unless stated.

| Scenario | Immediate actions | Assume compromised | Rotate | Do not | Stop using the device when |
|---|---|---|---|---|---|
| **Lost device** | Power it off if you can; note the time and place; tell trusted contacts out-of-band | Everything on it if the secret is weak or the device was unlocked | Accounts and sessions that were active on it | Do not call or message the lost device's number to "test" it; ask the carrier to block the SIM (a SIM PIN helps); do not assume it was wiped | It is not recovered, or recovered after unknown access |
| **Stolen device** | As above; report if appropriate | Everything on it, including cached messages | Messenger sessions, passwords, 2FA seeds, recovery codes that were on it | Do not retaliate or contact the thief | Always (replace it) |
| **Suspected malware** | Stop sensitive use; boot and update; check installed apps and permissions; consider a clean reinstall | The profile and every secret typed or displayed on it | Everything used on the device | Do not "clean" in place and keep using it | A reinstall does not remove symptoms |
| **Suspicious app** | Uninstall; revoke permissions; check what it accessed | Data the app could reach (Network, Contacts, Storage) | Credentials typed while it was installed | Do not re-install "to test" | It had broad access you cannot rule out |
| **Account compromise** | Sign out everywhere; change the password and 2FA from a clean device; revoke sessions and linked devices | The account, its contacts, its history | Password, recovery data, 2FA seed | Do not reuse the old password; do not reuse the account's recovery contact | The account cannot be recovered |
| **SIM/eSIM compromise** | Contact the carrier (ask about a SIM PIN and a port-out/SIM-swap lock); assume number takeover; re-verify contacts through another channel; consider Signal's Registration Lock [**External**](#tag-external) (a PIN required for re-registration; Signal cannot reset or recover the PIN, and if you forget it with Registration Lock enabled you may be locked out for up to 7 days; Registration Lock expires after 7 days of inactivity; re-registration can use a token plus the Signal PIN instead of SMS, and tokens are invalidated by a new registration or account deletion [**External**](#tag-external)) | The phone number and anything verified by SMS | Accounts that use the number for recovery or 2FA | Do not rely on SMS 2FA afterwards | You cannot regain the number |
| **Physical seizure** | Where the law allows, you may decline to answer; seek legal help [**Verify**](#verify-legal) for your country; note what happened | The device and everything on it, even if returned | All accounts and secrets that were on it | Do not reuse the device without a full re-flash through the official installer (unlock, flash, lock). With OEM unlocking off, this needs a device that still boots and lets you re-enable it; if that is not possible, treat it as permanently untrusted and replace it. Never lock after a failed or incomplete flash | Always, unless you can verify integrity (Auditor, clean reinstall) and accept the risk |
| **Accidental identity link** | Stop; stop using the linked identity; list what was exposed | The identity involved and its contacts | Usernames, email, phone number where possible | Do not delete or destroy data in ways that may be unlawful in your jurisdiction; get legal advice first [**Verify**](#verify-legal) | The link cannot be broken |

> ⚠️ Do not use the Duress wipe as a general incident-response tool. It is irreversible. [**Official**](#tag-official)

**Remaining risk:** you may not know an incident happened. Treat unexplained behavior as an incident.

---

## Useful websites / Nützliche Webseiten

Only official or reputable nonprofit sources. Trust levels are this guide's assessment.

| Name | URL | Purpose | When to use | Trust | Warning |
|---|---|---|---|---|---|
| GrapheneOS | <https://grapheneos.org/> | Official documentation: install, usage, features, FAQ, releases | Before every installation or change | Highest for GrapheneOS | Menus change per release |
| GrapheneOS discussion forum | <https://discuss.grapheneos.org/> | Official forum for longer posts, linked from the contact page | Questions the docs do not answer | High, but posts are user content | Not an authoritative statement unless from the project |
| Tor Project | <https://www.torproject.org/>, <https://support.torproject.org/tor-browser/features/fingerprinting-protections/>, <https://support.torproject.org/tor-browser/security/using-tb-safely/> and <https://support.torproject.org/tor-browser/security/using-tor-with-other-browsers/> | Tor Browser documentation and support | Before using Tor | High | Tor does not protect what you reveal by logging in |
| Signal | <https://signal.org/>, <https://signal.org/blog/phone-number-privacy-usernames/>, <https://signal.org/android/apk/>, <https://support.signal.org/hc/en-us/articles/360007059792-Signal-PIN> and <https://support.signal.org/hc/en-us/articles/5440120029082-Re-registering-using-your-Signal-PIN> | Messenger documentation, blog and support articles | Before relying on Signal features | High for Signal behavior | Registration requires a number; Signal cannot reset or recover your PIN |
| EFF Surveillance Self-Defense | <https://ssd.eff.org/> | Threat modeling ("Your Security Plan"), passwords, Signal, VPNs, protests, phones | Planning and learning | High (nonprofit) | Often US-centric; VPN module says it cannot vouch for any VPN |
| Freedom of the Press Foundation | <https://freedom.press/digisec/> and <https://freedom.press/digisec/guides/> | Digital security training and guides for journalists | Source protection, location privacy | High (nonprofit) | Guides vary in age; check dates |
| Reporters Without Borders | <https://rsf.org/en/digital-security-lab> and <https://resources.rsf.org/digital-security-and-spyware-guide/> | Reporters Without Borders Digital Security Lab (forensic support for journalists) and its Digital Security and Spyware Guide (published 17/12/2025) | Context and journalist safety | High (nonprofit) | RSF gives approximate menu paths that vary by Android version and manufacturer, and no country-specific legal advice |
| Have I Been Pwned | <https://haveibeenpwned.com/> | Check whether an email address appears in known breaches | After a suspected account compromise | Reputable | You submit an email address to a third party; use it from another device and an address you accept exposing |
| Accrescent | <https://accrescent.app/> | App store for Android | Evaluating app sources | Reputable, in alpha | In alpha; available in the GrapheneOS App Store |
| F-Droid | <https://f-droid.org/>, <https://f-droid.org/en/about/> and <https://f-droid.org/docs/FAQ_-_App_Developers/> | Open-source app repository | App sourcing | Reputable | Signing model depends on reproducible-build verification |
| Aegis Authenticator | <https://github.com/beemdevelopment/Aegis> | Official repository (GPL-3.0) | Install and verify | Official project page | Verify the signing certificate |
| KeePassDX | <https://github.com/Kunzisoft/KeePassDX> and <https://www.keepassdx.com/> | Official repository and site (GPL-3.0) | Install and verify | Official project page | Free and Pro versions on Google Play |
| Mullvad VPN | <https://mullvad.net/> and <https://github.com/mullvad/mullvadvpn-app> | Official app and source | Only if a VPN is justified | Official; recommended by the GrapheneOS FAQ | A VPN is not anonymity |
| Cryptomator | <https://cryptomator.org/android/>, <https://github.com/cryptomator/android> and <https://docs.cryptomator.org/android/setup/> | Official app pages | Optional encrypted storage | Official | Channel and license differ; verify |
| Organic Maps | <https://organicmaps.app/> and <https://github.com/organicmaps/organicmaps> | Offline maps | Optional | Official | Funding is described as precarious by the project |
| Tor Browser download | <https://download.torproject.org/> | Official Tor Browser for Android download | Only if Tor is justified | Official | Do not install add-ons or use other browsers with Tor |
| GrapheneOS X post, 13 June 2024 | <https://x.com/GrapheneOS/status/1801294115407106186> | GrapheneOS statement that forensics companies exploited wipe apps such as Wasted and Sentry | Section 4.5 | Statement by the project, but a social-media post, not documentation | Posts can be edited or deleted; not on grapheneos.org |
| GrapheneOS forum thread "wasted-sentry" | <https://discuss.grapheneos.org/d/28627-wasted-sentry> | Community discussion of Wasted and Sentry, including Android 15 reliability reports | Section 4.5 | User content, not official | A single user's observation; not independently tested here |
| privacygear.nl GrapheneOS hardening guide | <https://privacygear.nl/en/guides/grapheneos-hardening-guide/> | Settings walkthrough with menu paths (Lockdown, NFC, memory tagging) | Cross-checking menu paths | Secondary source (reviewed 5 Nov 2026, GrapheneOS 2026110200); not official GrapheneOS documentation | Paths vary by release and Android version; it recommends Orbot for app-level Tor, which a GrapheneOS maintainer criticized in 2020 |

Excluded on purpose: VPN affiliate lists, "anonymous phone" sellers, cracked-app sites, random Telegram channels, influencer blogs as primary sources, and any tool that requires trusting an unknown third party.

---

## 13. Checklists

### Initial cryptophone setup
- [ ] Supported, recommended Pixel (8th generation or newer)
- [ ] Official GrapheneOS installed via the web installer or CLI guide
- [ ] Bootloader locked **only after** a successful, verified flash
- [ ] OEM-unlocking toggle left checked on the last setup screen
- [ ] Verified-boot key hash checked; Auditor used if possible
- [ ] Updates installed, Stable channel
- [ ] Long random passphrase or long random PIN; biometrics off; PIN scrambling on
- [ ] Auto-reboot set; USB-C restricted
- [ ] Bluetooth, NFC and location off; Wi-Fi off except while updating or installing apps
- [ ] Debugging off
- [ ] Profiles created: Owner, secure communication, optional browsing
- [ ] App list with documented purposes created

### Before first sensitive use
- [ ] Fresh accounts only; no personal data used
- [ ] Separate SIM/eSIM or Wi-Fi-only decision made
- [ ] Safety numbers verified with each contact
- [ ] Notifications hide content
- [ ] Network permission blocked for offline apps
- [ ] Backup policy decided; recovery codes stored offline
- [ ] Private DNS Off if a VPN is used; VPN kill switch tested

### Weekly maintenance
- [ ] Updates installed and rebooted
- [ ] Review installed apps and permissions
- [ ] Remove unused apps
- [ ] Review the app list against the documented purposes
- [ ] Re-test backups and recovery (monthly is enough)

### Before travel
- [ ] Minimize data; remove unneeded apps and histories
- [ ] Update and reboot; set a short auto-reboot
- [ ] Decide travel device vs clean profile
- [ ] Decide biometrics (off) and know Lockdown
- [ ] Know the local rules on device search and compelled unlock [**Verify**](#verify-legal)
- [ ] Recovery codes offline and separate
- [ ] Own charger and cable

### After installing any app
- [ ] Source verified (App Store, developer signature or, as a fallback, Accrescent/F-Droid)
- [ ] Purpose, source and permissions documented
- [ ] Deny unneeded permissions; use Contact Scopes and Storage Scopes
- [ ] Block Network if it works offline
- [ ] Sensors permission denied if not needed
- [ ] Placed in the correct profile

### Before connecting to public Wi-Fi
- [ ] Is this traffic acceptable for the operator to see?
- [ ] VPN decision made (and Private DNS Off if used)
- [ ] No personal account logins
- [ ] Captive portal: do not enter a real phone number or email
- [ ] Disconnect and forget the network afterwards

### If the device is lost or stolen
- [ ] Power off if possible
- [ ] Notify trusted contacts out-of-band
- [ ] Rotate passwords, 2FA seeds and recovery codes that were on it
- [ ] Re-verify contacts' safety numbers after replacing the device
- [ ] Treat any recovered device as untrusted until reinstalled

### If identity compromise is suspected
- [ ] Stop using the linked identity
- [ ] List exactly what was exposed
- [ ] Rotate usernames, email and numbers where possible
- [ ] Re-verify contacts through a separate channel
- [ ] Seek advice if the compromise has legal or safety consequences

---

## 14. Anti-patterns

| Claim | Realistic version |
|---|---|
| "More privacy apps = more secure" | Each app adds trust and attack surface. The safest list is the shortest list |
| "VPN = anonymous" | A VPN shifts trust to the provider. EFF: "A VPN is not a tool for anonymity" [**External**](#tag-external) |
| "Tor = safe for everything" | Tor protects only apps configured for it, and logging in or revealing details defeats it [**External**](#tag-external). The project calls Tor Browser's security on Android weak [**Official**](#tag-official) |
| "GrapheneOS = untrackable" | The carrier, Wi-Fi operator and services still see slices of your activity |
| "Deleted data is gone" | Deleted data may persist in backups, caches and recipients' devices |
| "An encrypted messenger protects against a compromised phone" | End-to-end encryption protects the transport, not the endpoints |
| "A second profile makes me anonymous" | Profiles share hardware, SIM, IP and your habits. [**Advice**](#tag-advice) |
| "Airplane mode makes a phone untrackable" | It may not block location services and apps can send stored data later; powering off is the strongest step available [**External**](#tag-external) |
| "A faraday bag solves OPSEC" | It blocks radios while closed; it does not fix accounts, habits or a compromised device [**Advice**](#tag-advice) |
| "A burner phone is automatically anonymous" | EFF lists conditions for a burner phone to work at all (no reuse of SIM or device, not carried together with your regular phone, not calling the same people) [**External**](#tag-external); location and number correlation remain [**Advice**](#tag-advice) |

---

## 15. Essential vs optional, and verification status

### Essential

- Official install, **bootloader locked after a verified flash**, OEM unlocking disabled
- Immediate updates, Stable channel
- Long secret, no biometrics, auto-reboot, USB-C restricted
- Tiny documented app list; Network permission blocked for offline apps
- No Google Play by default; separate SIM/eSIM or Wi-Fi-only; no reused identity material
- Minimal, encrypted, offline backups; incident plan

### Optional

- LTE-only mode, VPN, Tor Browser, Cryptomator, Organic Maps, Duress, Lockdown habit, a travel device

### What the setup protects against

Opportunistic theft, many exploit classes, malicious apps (through the sandbox), casual and forensic guessing (through the secure element and a strong secret), USB attacks on a locked phone, a hostile local network, and a lot of over-collection by apps.

### What it does not protect against

Everything listed in section 1, plus a compromised endpoint on the other side, traffic analysis, and your own mistakes.

### Verification status

| Item | Status |
|---|---|
| GrapheneOS install, lock/unlock, wipes, secure-element limits, auto-reboot, USB-C modes, scopes, permissions, Private DNS and VPN guidance, LTE-only, eSIM, Vanadium behavior, Accrescent and the PDF Viewer in the app repository, Private Space clipboard setting, absence of a remote wipe | Verified against the official pages [**Official**](#tag-official) |
| EFF (including the 2025 border checklist), Tor Project, FPF (including powered-off signals), RSF (Digital Security and Spyware Guide), Signal blog and support articles (including backups, safety numbers, Signal PIN, Registration Lock and the APK page), HIBP, app licenses and sources | Spot-checked against the named primary sources; Lockdown, the NFC path and the memory-tagging path rest on a secondary source (privacygear.nl) [**External**](#tag-external) |
| Tor VPN (GrapheneOS stance); exact menu paths for Bluetooth/Wi-Fi auto-off and the Private Space clipboard setting; Signal on Accrescent; whether eSIM activation needs an account, ID or payment; IMEI visibility of a SIM-less phone; the text of CBP directive 3340-049B; non-US border and legal rules | [**Verify**](#tag-verify) |

*Verify against current official documentation.*
