# GrapheneOS-Leitfaden (Deutsch)

> **Stand:** erstellt am 05.11.2026 und gegen die offiziellen GrapheneOS-Seiten geprüft (Features, Usage, FAQ, Web-/CLI-Installer, Releases). Menünamen und Geräteliste ändern sich zwischen Versionen. Wo etwas vom Gerät oder der Version abhängen kann, steht das im Text. Bei allem mit [**Prüfen**](#tag-verify) gilt: *Mit der aktuellen offiziellen Dokumentation abgleichen.*
>
> **Legende:** [**Offiziell**](#tag-official) = steht in der offiziellen GrapheneOS-Dokumentation. [**Empfehlung**](#tag-advice) = Einschätzung dieses Leitfadens bzw. allgemeine Sicherheitspraxis, keine offizielle Aussage von GrapheneOS.

English version: [daily-driver-guide-en.md](daily-driver-guide-en.md) · Für ein strengeres Einzweck-Setup siehe [cryptophone-guide-de.md](cryptophone-guide-de.md)

## Inhaltsverzeichnis

1. [Einführung](#1-einführung)
2. [Unterstützte Geräte und Vorbereitung](#2-unterstützte-geräte-und-vorbereitung)
3. [Installation](#3-installation)
4. [Einrichtung beim ersten Start](#4-einrichtung-beim-ersten-start)
5. [Grundlegende Härtung](#5-grundlegende-härtung)
6. [Erweiterte Härtung](#6-erweiterte-härtung)
7. [Apps: sichere Installation und Auswahl](#7-apps-sichere-installation-und-auswahl)
8. [Sandboxed Google Play](#8-sandboxed-google-play)
9. [Anonymität: realistische OPSEC](#9-anonymität-realistische-opsec)
10. [Checklisten für den Alltag](#10-checklisten-für-den-alltag)
11. [Häufige Fehler](#11-häufige-fehler)
12. [Schnellreferenz-Tabellen](#12-schnellreferenz-tabellen)
13. [Quellen](#13-quellen)
14. [Verbesserungen gegenüber dem bisherigen Leitfaden](#14-verbesserungen-gegenüber-dem-bisherigen-leitfaden)
15. [Änderungsprotokoll](#15-änderungsprotokoll)

[Tag-Legende](#tag-legend)

---

<a id="tag-legend"></a>
## Tag-Legende

Jede Markierung in diesem Leitfaden verweist auf ihren Eintrag unten.

| Markierung | Bedeutung |
|---|---|
| <a id="tag-official"></a>**[Offiziell]** | Steht in der offiziellen GrapheneOS-Dokumentation (Features, Usage, FAQ, Installer, Versionshinweise oder Projektquelltext). |
| <a id="tag-advice"></a>**[Empfehlung]** | Empfehlung dieses Leitfadens bzw. allgemeine Sicherheitspraxis; keine harte Tatsache und keine offizielle Aussage von GrapheneOS. |
| <a id="tag-verify"></a>**[Prüfen]** | Nicht bestätigt. Der Grund steht neben der Markierung. Jede Markierung springt zur ersten Stelle, an der der Grund für ihr Thema genannt wird. |

**Offene Prüfthemen** (jedes verweist auf die Stelle, an der der Grund genannt wird):

- [Menüpfade und Bezeichnungen](#verify-menu-paths)
- [Rechtliche, Grenz- und Zwangsentsperrungs-Regeln je Land](#verify-legal)
- [Ob die eSIM-Aktivierung ein Konto, einen Ausweis oder eine Zahlung braucht](#verify-esim)

---

## 1. Einführung

### Was GrapheneOS ist und was nicht

GrapheneOS ist ein gehärtetes, quelloffenes Betriebssystem auf Android-Basis für unterstützte Pixel-Geräte. Es baut auf dem Android Open Source Project (AOSP) auf und ergänzt Exploit-Schutz (z. B. gehärteten Speicherallokator, Hardware Memory Tagging ab Pixel 8), ein strengeres Berechtigungsmodell und Datenschutzfunktionen. [**Offiziell**](#tag-official)

Es ist **nicht**:

- ein Anonymitätswerkzeug. Es verbirgt weder Rufnummer, SIM, Netzbetreiber, IP-Adresse noch Konten;
- ein Ersatz für gute Gewohnheiten. Eine schwache PIN, ein entsperrter Bootloader oder viele unvertrauenswürdige Apps heben einen großen Teil des Schutzes wieder auf;
- Schutz vor allem. Ein mächtiger, gezielter Angreifer mit physischem Zugriff, ein entsperrtes Gerät oder eine Firmware-Lücke können trotzdem zum Erfolg führen. GrapheneOS erhöht den Aufwand für Angreifer, garantiert aber keine Sicherheit.

### Sicherheit, Datenschutz und Anonymität

| Begriff | Fragestellung | Beispielmaßnahme |
|---|---|---|
| **Sicherheit** | Kann jemand ins Gerät oder in Apps eindringen? | Updates, starker Sperrcode, gesperrter Bootloader, App-Sandbox |
| **Datenschutz** | Wer sieht welche Daten über mich? | Berechtigungskontrolle, weniger Tracker, kein Google-Konto |
| **Anonymität** | Lassen sich Handlungen mir zuordnen? | Getrennte Identitäten, keine verknüpfbaren Konten, Sorgfalt im Netz. Auf einem Smartphone sehr schwer |

Man kann hohe Sicherheit bei geringer Anonymität haben (ein gut geschütztes Telefon, das auf den eigenen Namen läuft).

### Für wen ist dieser Leitfaden

Für Besitzer eines unterstützten Pixels, die einen klaren Weg von der Installation bis zum Alltag suchen. Er ist anfängerfreundlich, bleibt aber technisch präzise.

### Beispiele für Bedrohungsmodelle

| Profil | Typische Sorgen | Realistisches Ziel |
|---|---|---|
| **Durchschnittsnutzer** | Diebstahl, Schadsoftware, Werbetracking | Updates, starke PIN, wenige Apps, keine unnötigen Berechtigungen |
| **Datenschutzbewusste Nutzer** | Datenhändler, App-Telemetrie, Profilbildung über Konten | Alles oben plus Profiltrennung, kein oder eingeschränktes Google, weniger Netzwerk-Exposition |
| **Journalisten / Aktivisten mit hohem Risiko** | Beschlagnahme, gezielte Überwachung, Quellenschutz | Alles oben plus lange Passphrase, kurzer Auto-Reboot, USB-Sperre, strikte Identitätstrennung, Reisedisziplin und fachkundige Beratung |

### Wogegen dieser Leitfaden schützt und wogegen nicht

**Hilft bei:** Gelegenheitsdiebstahl, viel verbreiteter Schadsoftware, den Auswirkungen vieler Exploit-Klassen, flüchtigem physischem Zugriff auf ein gesperrtes Gerät, massenhaftem App-Tracking.

**Löst nicht:** Standortdaten von Netzbetreiber und Funkzellen, dein eigenes Verhalten und die Verknüpfung über Konten, eine App, der du bewusst vertraust und die kompromittiert ist, Nötigung, oder einen gut ausgestatteten gezielten Angreifer. Das Ziel ist, **Exposition zu verringern**, nicht Perfektion zu erwarten.

Der Leitfaden behandelt legalen Datenschutz und persönliche Sicherheit. Er hilft nicht, rechtmäßige Ermittlungen zu umgehen.

---

## 2. Unterstützte Geräte und Vorbereitung

### Unterstützte Geräte [**Offiziell**](#tag-official)

Zum Zeitpunkt der Erstellung nennt die FAQ offiziellen Produktionssupport für: Pixel 6, 6 Pro, 6a, 7, 7 Pro, 7a, Fold, Tablet, 8, 8 Pro, 8a, 9, 9 Pro, 9 Pro XL, 9 Pro Fold, 9a, 10, 10 Pro, 10 Pro XL, 10 Pro Fold und 10a. Die FAQ nennt für Pixel 6 und 6 Pro ein OEM-Mindest-Supportende im Oktober 2026; behandle sie daher als am oder nach dem Supportende (offizielle Updates enden typischerweise kurz danach). Ältere Modelle hatten ein 5-Jahres-Minimum. [**Offiziell**](#tag-official)

GrapheneOS empfiehlt ausdrücklich Pixel 8 oder neuer (8, 8 Pro, 8a, 9er- und 10er-Serie), weil der Hersteller mindestens sieben Jahre Support ab dem Marktstart des jeweiligen Modells bietet und diese Geräte Hardware Memory Tagging unterstützen. Prüfe vor dem Kauf die aktuelle Liste unterstützter Geräte; dieses Minimum garantiert nicht sieben verbleibende Jahre zum Kaufzeitpunkt. Ältere gelistete Geräte haben kürzeren oder erweiterten Support und sind nur Übergangslösungen. Die Liste oben entspricht der FAQ vom 05.11.2026; prüfe sie vor dem Kauf erneut unter <https://grapheneos.org/faq#supported-devices>, da sie sich ändert.

Provider-gesperrte Varianten (vor allem manche US-Modelle) erlauben ggf. kein Entsperren des Bootloaders. Kaufe ein freies Gerät oder stelle sicher, dass es entsperrbar ist.

### Warum offizieller Support und Verified Boot wichtig sind [**Offiziell**](#tag-official)

- Offiziell unterstützte Geräte erhalten volle Firmware-, Kernel- und Vendor-Sicherheitsupdates. Ein Gerät ohne Herstellersupport lässt sich nicht allein durch das Betriebssystem absichern.
- Verified Boot prüft bei jedem Start das Betriebssystem und erkennt Manipulationen. Es wirkt nur voll, wenn der Bootloader nach der Installation **gesperrt** ist. GrapheneOS hinterlegt dafür einen eigenen Signaturschlüssel, sodass dieser Schutz für GrapheneOS gilt und nicht für Stock-Android.
- Das Projekt leistet keinen Support für Geräte mit entsperrtem Bootloader, da dies eine unvollständige Installation ist.

### Benötigte Ausstattung

- ein unterstütztes Pixel und sein USB-C-Kabel oder ein hochwertiges, standardkonformes USB-C-Kabel;
- ein Computer mit mindestens 2 GB freiem Arbeitsspeicher und 32 GB freiem Speicher, mit unterstütztem Betriebssystem auf echter Hardware (eine virtuelle Maschine wird nicht empfohlen). Der Web-Installer läuft auch auf einem Android-Telefon oder -Tablet;
- ein unterstützter Browser: Chromium (nicht das Snap-Paket von Ubuntu), Vanadium, Google Chrome, Microsoft Edge oder Brave mit deaktivierten Brave Shields [**Offiziell**](#tag-official);
- Internetzugang (der Installer lädt das Release herunter);
- ein **Backup** aller Daten, die du behalten willst.

> ⚠️ **Warnung: Die Installation löscht das Gerät.** Das Entsperren und das spätere Sperren des Bootloaders löschen jeweils alle Daten. Sichere vorher alles und verlasse dich danach nicht auf den alten Gerätezustand.

### Kauf und Vorbereitung

- Offiziell empfohlen wird, ein unterstütztes Pixel selbst zu kaufen und GrapheneOS selbst zu installieren. Das Projekt ist mit Firmen, die Geräte mit vorinstalliertem GrapheneOS verkaufen, nicht verbunden und empfiehlt sie nicht. [**Offiziell**](#tag-official)
- Wer trotzdem ein vorinstalliertes Gerät kauft, prüft nach Erhalt den Verified-Boot-Schlüssel-Hash (siehe [3.6](#36-installation-überprüfen)) und die verbleibende Supportdauer.
- Ein Kauf im Laden, bar oder ohne Konto kann *manche* Kaufspuren verringern. Das Gerät wird dadurch **nicht** anonym: Gerätekennungen, deine SIM und späteres Verhalten verknüpfen es wieder mit dir. Händler können zudem Aufzeichnungen wie Videoüberwachung, Bestands-/IMEI-Daten oder Zahlungsmetadaten speichern, die selbst einen Barkauf einer Person zuordnen können. Verlasse dich nicht auf Kauftricks.

---

## 3. Installation

> ⚠️ Nutze **ausschließlich** die offiziellen Installer unter <https://grapheneos.org/install/>. Verwende niemals inoffizielle Images, vermeintliche „GrapheneOS-Installer“, nicht überprüfbare Spiegel oder Drittanleitungen, die Schritte überspringen lassen. Laut Projekt sind Drittanleitungen oft veraltet und enthalten falsche Ratschläge. [**Offiziell**](#tag-official)

### 3.1 Methode A: Web-Installer (für die meisten empfohlen)

Seite: <https://grapheneos.org/install/web>

**Vorbereitung**

1. Starte das Stock-Android, schließe die Einrichtung ab und verbinde dich mit dem Internet.
2. Aktualisiere das Stock-Android. Beim **Pixel 6a** funktioniert die OEM-Entsperrung mit dem werkseitigen Stock-Android nicht: per OTA auf den Stand Juni 2022 oder neuer aktualisieren, **danach das Gerät auf Werkseinstellungen zurücksetzen**. [**Offiziell**](#tag-official)
3. Entwickleroptionen aktivieren: **Einstellungen → Über das Telefon** und mehrfach auf **Build-Nummer** tippen.
4. Unter **Einstellungen → System → Entwickleroptionen** **OEM-Entsperrung** aktivieren. Bei Provider-Varianten braucht dieser Schritt Internetzugang, damit das Stock-Android prüfen kann, ob das Gerät gesperrt verkauft wurde.

**Entsperren** (löscht das Gerät)

5. Öffne auf dem Computer die Installationsseite im unterstützten Browser. Auf klassischen Linux-Distributionen brauchst du udev-Regeln für USB-Zugriff ohne Root (Arch: `android-udev`; Debian/Ubuntu: `android-sdk-platform-tools-common`). Nutze einen direkten Port und ein gutes Kabel, keinen Hub, und verbinde das Telefon. [**Offiziell**](#tag-official)
6. Starte das Telefon im Bootloader (halte beim Start die Leiser-Taste gedrückt, wie in der CLI-Anleitung; die Webseite erklärt es ebenfalls) und klicke auf der Seite auf **Unlock bootloader**.
7. Bestätige am Telefon mit den Lautstärketasten und der Ein-/Aus-Taste.

**Flashen**

8. Nutze die Schaltflächen der Seite zum Herunterladen des Releases und **Flash release**. Der Installer flasht Firmware, startet in den Bootloader neu und flasht das Betriebssystem selbstständig. Ziehe das Kabel nicht und bediene das Telefon nicht, bis der Vorgang fertig ist. [**Offiziell**](#tag-official)

**Sperren**

9. **Sperre den Bootloader erst, nachdem der offizielle Installer/Flasher erfolgreiches Flashen gemeldet hat.** Wähle dann auf der Seite **Lock bootloader** und bestätige am Telefon mit Lautstärke- und Ein-/Aus-Taste. Ist das Flashen fehlgeschlagen, wurde es unterbrochen oder ist es unvollständig, sperre nicht: Lass den Bootloader entsperrt und flashe erneut. Ein Sperren mit fehlendem, unvollständigem oder ungültigem Betriebssystem kann das Gerät unwiederbringlich machen, weil die OEM-Entsperrung nur aus einem startenden Betriebssystem wieder aktiviert werden kann. **Das Sperren löscht alle Daten erneut**; deshalb muss es geschehen, bevor du Daten auf das Gerät legst. [**Offiziell**](#tag-official) für Sperrschritt und Löschung; die Warnung vor Fehlschlägen ist [**Empfehlung**](#tag-advice)

> ⚠️ **Das Sperren niemals auslassen.** Die Installation ist erst abgeschlossen, wenn der Bootloader nach einem erfolgreichen, verifizierten Flash gesperrt wurde. Das Sperren aktiviert das volle Verified Boot und verhindert Flashen, Formatieren und Löschen von Partitionen per Fastboot. [**Offiziell**](#tag-official)

10. Starte GrapheneOS und schließe die Einrichtung ab (siehe [Abschnitt 4](#4-einrichtung-beim-ersten-start)).

### 3.2 Methode B: Kommandozeile (fortgeschritten)

Seite: <https://grapheneos.org/install/cli>

Diese Methode erlaubt die Installation, ohne der Web-Infrastruktur des Projekts zu vertrauen: Du lädst das Factory-Image herunter, **überprüfst die Signatur mit OpenSSH** und flashst mit `fastboot`. Nötig sind ein unterstütztes System mit aktuellem `fastboot` und OpenSSH sowie genug Verständnis, um nicht blind Anweisungen zu folgen. Das Projekt rät, die Anleitung **buchstabengetreu zu befolgen, ohne Schritte auszulassen, umzuordnen oder hinzuzufügen**. [**Offiziell**](#tag-official)

Ablauf im Überblick (die aktuelle Seite enthält die genauen Befehle, Versionen und Prüfsummen; diese ändern sich):

1. **`fastboot` besorgen.** Für die meisten wird das eigenständige Google-platform-tools-Release empfohlen; die Seite nennt je System Download- und SHA-256-Prüfbefehle und verlangt, es zum `PATH` hinzuzufügen. Prüfe vor dem Weitermachen `fastboot --version`.
2. **OEM-Entsperrung aktivieren** im Stock-Android (wie 3.1, Schritte 1-4, einschließlich Hinweis zum Pixel 6a).
3. **In das Bootloader-Interface starten:** Halte beim Start die Leiser-Taste gedrückt, bis das rote Warndreieck und „Fastboot Mode“ erscheinen. Wähle „Start“ nicht mit der Ein-/Aus-Taste aus. Gerät verbinden.
4. **Entsperren:** `fastboot flashing unlock`, am Gerät mit Lautstärke- und Ein-/Aus-Taste bestätigen. Das löscht alle Daten.
5. **Factory-Images beschaffen und prüfen:** `allowed_signers`, die Datei `DEVICE_NAME-install-VERSION.zip` und ihre `.zip.sig` herunterladen, dann die Signatur mit `ssh-keygen -Y verify` genau wie auf der Seite gezeigt prüfen. Vergleiche den Signaturschlüssel mit den anderen dort genannten Quellen. Flashe niemals ein Image, dessen Prüfung fehlschlägt. **Schlägt die Verifizierung fehl oder schlägt das Flashen fehl oder ist unvollständig, sperre den Bootloader nicht.** Lass ihn entsperrt und flashe erneut; das Gerät startet womöglich nicht, bis ein verifiziertes GrapheneOS-Image erfolgreich geflasht und der Bootloader danach gesperrt wurde. Ein Sperren mit fehlendem, unvollständigem oder ungültigem Betriebssystem kann das Gerät unwiederbringlich machen, weil die OEM-Entsperrung nur aus einem startenden Betriebssystem wieder aktiviert werden kann. [**Empfehlung**](#tag-advice) Lade das Image erneut herunter, verifiziere es erneut und wiederhole die Installation, oder frage in den offiziellen GrapheneOS-Supportkanälen nach (auf der Installationsseite verlinkt).
6. **Flashen:** Zip entpacken (`bsdtar xvf` unter Linux, `tar xvf` unter macOS/Windows), ins Verzeichnis wechseln und `bash flash-all.sh` (Linux/macOS) bzw. `./flash-all.bat` (Windows) ausführen. Das Skript flasht die Firmware, startet in den Bootloader neu und flasht das Betriebssystem. Bediene das Gerät nicht, bis es fertig ist.
7. **Sperren:** Erst nach erfolgreichem Flashen und Verifizieren (das Flash-Skript ist fehlerfrei durchgelaufen und die Image-Signatur wurde verifiziert) `fastboot flashing lock` ausführen und am Gerät bestätigen. Sperre nie nach einem fehlgeschlagenen, unvollständigen oder nicht verifizierten Flash; es kann das Gerät unwiederbringlich machen (siehe Schritt 5). **Das Sperren löscht erneut alle Daten**; tu es, bevor du das Gerät benutzt.
8. GrapheneOS starten, Einrichtung abschließen und den Schalter zur OEM-Entsperrung auf dem letzten Einrichtungsbildschirm angehakt lassen.

> ⚠️ Prüfe die Signatur vor dem Flashen. Ein ungeprüftes Image macht den Sinn der CLI-Methode zunichte.

### 3.3 OEM-Entsperrung deaktivieren

Beim ersten Einrichten gibt es auf dem letzten Bildschirm einen Schalter für die OEM-Entsperrung, der **standardmäßig angehakt** ist. Das deaktiviert die OEM-Entsperrung und wird empfohlen. Später lässt sich das unter **Einstellungen → System → Entwickleroptionen** ändern. [**Offiziell**](#tag-official)

Ist die OEM-Entsperrung aus, kann der Bootloader nicht ohne Zugriff auf das Betriebssystem entsperrt werden. Damit entfällt ein Weg, ein manipuliertes System aufzuspielen.

### 3.4 USB- und drahtloses Debugging ausschalten

Schalte nach der Installation USB-Debugging und drahtloses Debugging aus, sofern du sie nicht aktiv brauchst. [**Empfehlung**](#tag-advice)

### 3.5 Häufige Fehler und Fehlerbehebung

| Problem | Wahrscheinliche Ursache | Was tun |
|---|---|---|
| Telefon wird nicht erkannt | Defektes Kabel/Hub, VM, fehlende Windows-Treiber | Originalkabel, direkten Port hinten am Rechner, echtes System nutzen; Hinweise der Seite beachten |
| „OEM-Entsperrung“ ausgegraut | Kein Internet bei Provider-Variante; Pixel 6a nicht auf Juni 2022+ aktualisiert oder danach nicht zurückgesetzt | Internet verbinden; Stock-Android aktualisieren; beim Pixel 6a nach dem OTA-Update auf Werkseinstellungen zurücksetzen |
| Flashen bricht ab | Kabel/Hub/Browser-Problem | **Bootloader nicht sperren.** Anderes Kabel/anderen Port probieren und den Vorgang vom Bootloader aus neu starten; erst nach vollständigem, erfolgreichem Flash sperren. Ein Sperren über einem fehlgeschlagenen, unvollständigen oder nicht verifizierten Flash kann das Gerät unwiederbringlich machen, weil die OEM-Entsperrung nur aus einem startenden Betriebssystem wieder aktiviert werden kann |
| Einrichtung zeigt Warnung „Bootloader nicht gesperrt“ | Sperr-Schritt ausgelassen | Nur wenn der ursprüngliche Flash erfolgreich abgeschlossen wurde: Im Willkommensbildschirm „Reboot to bootloader“ wählen und über die Installationsseite sperren. Das vor dem Aufspielen von Daten tun [**Offiziell**](#tag-official) (FAQ) |
| Gelber Startbildschirm | Erwartet: zeigt den GrapheneOS-Schlüssel-Hash | Siehe 3.6 |
| Festgefahren oder unsicher | | Im offiziellen Chat nachfragen (auf der Installationsseite verlinkt) |

### 3.6 Installation überprüfen

1. Beim Start sollte ein **gelber** Hinweis erscheinen, dass ein alternatives Betriebssystem geladen wird, mit einer ID aus dem SHA-256 des Verified-Boot-Schlüssels. Der volle Hash wird angezeigt, und du kannst ihn mit der Liste auf der Installationsseite vergleichen. [**Offiziell**](#tag-official) Die Prüfung ist nützlich, Verified Boot funktioniert aber auch ohne dein manuelles Nachprüfen.
2. Beim Einrichten darf keine Warnung zu einem entsperrten Bootloader erscheinen. Erscheint sie, ist die Installation unvollständig (siehe Tabelle zur Fehlerbehebung).
3. Für stärkere Gewissheit nutze die **Auditor**-App mit einem zweiten Android-Gerät (hardwarebasierte Attestierung). [**Offiziell**](#tag-official) Koppele sie unmittelbar nach der Installation, bevor das Gerät deine Kontrolle verlässt; eine Attestierung nach einem Verlust ist nur aussagekräftig, wenn die Kopplung vorher stattfand. [**Empfehlung**](#tag-advice) Sie prüft Hardware, Firmware und Betriebssystem, nicht jede installierte App.

---

## 4. Einrichtung beim ersten Start

Die Menünamen folgen der aktuellen offiziellen Dokumentation; Bezeichnungen können sich je nach Version unterscheiden. <a id="verify-menu-paths"></a>[**Prüfen**](#verify-menu-paths)

### 4.1 Erste Einstellungen

- Sprache wählen und den Schalter „OEM-Entsperrung deaktivieren“ auf dem letzten Bildschirm angehakt lassen (Standard).
- Kontoanmeldungen überspringen oder ablehnen. GrapheneOS braucht kein Google-Konto. [**Offiziell**](#tag-official)
- Aktiviere keine Nutzungsberichte, die du nicht brauchst. GrapheneOS kontaktiert eigene Server für Updates, Verbindungsprüfungen, Zeit und Ähnliches; die vollständige Liste steht im FAQ-Eintrag zu den Standardverbindungen. [**Offiziell**](#tag-official)

### 4.2 WLAN, mobile Daten, SIM und eSIM

- Aktualisiere das System zuerst in einem vertrauenswürdigen Netz. Bei höherem Risiko kann es sinnvoll sein, vor dem Verbinden einen starken Sperrcode zu setzen.
- Eine SIM oder eSIM verknüpft das Telefon mit einem Vertragskonto und einer Standortspur. Siehe [Abschnitt 9](#9-anonymität-realistische-opsec).
- Eine eSIM ist nicht anonymer als eine physische SIM; sie hat eine eigene Kennung (EID, laut Android-Dokumentation). [**Empfehlung**](#tag-advice) Ein Duress-Wipe entfernt installierte eSIM-Profile [**Offiziell**](#tag-official); das kündigt den Vertrag beim Netzbetreiber nicht. [**Empfehlung**](#tag-advice)
- Der LTE-only-Modus (Einstellungen → Netzwerk & Internet → SIMs → deine SIM → Bevorzugter Netzwerktyp) verringert die Ausnutzung von altem Funkmodul-Code aus der Ferne; laut Projekt ist er keine Vertraulichkeitsfunktion. [**Offiziell**](#tag-official) Er hilft nur, wenn dein Netzbetreiber im LTE-only-Modus zuverlässig funktioniert. [**Empfehlung**](#tag-advice)
- Wenn du kein Mobilfunknetz brauchst, kannst du das Telefon nur per WLAN nutzen (keine SIM eingelegt oder genutzt). Das vermeidet die SIM-basierte Verbindung zu einem Netzbetreiber, nicht aber WLAN-/IP-Exposition. Der Flugmodus ist kein Beweis für Ortungssicherheit, und Ausschalten ist stärker (siehe [cryptophone-guide-de.md, Abschnitt 9.1](cryptophone-guide-de.md#91-mobilfunknetz)). [**Empfehlung**](#tag-advice)

### 4.3 Bildschirmsperre

Pfad: **Einstellungen → Sicherheit & Datenschutz → Gerät entsperren** (englisch: Security & privacy → Device unlock). [**Offiziell**](#tag-official)

- Nutze eine **zufällige PIN mit mindestens 6 Ziffern** oder besser eine **Passphrase** (mehrere zufällige Wörter / lange alphanumerische Folge). Keine Geburtstage, keine wiederverwendeten Codes. [**Empfehlung**](#tag-advice) GrapheneOS unterstützt Passwörter mit bis zu 128 Zeichen, auch Diceware-Passphrasen. [**Offiziell**](#tag-official)
- Aktiviere **PIN-Scrambling** (zufällige Tastenanordnung; gilt für Sperrbildschirm und SIM-PIN). [**Offiziell**](#tag-official) Es erschwert das Mitlesen und Fingerabdruckspuren auf dem Display, kostet aber Tempo.
- Biometrie ist Komfort, nicht dein Hauptgeheimnis. GrapheneOS bietet **Zwei-Faktor-Fingerabdruck-Entsperrung** (Fingerabdruck plus PIN), sodass eine starke Passphrase die Hauptmethode bleiben kann. [**Offiziell**](#tag-official) Außerdem erlaubt es nur insgesamt 5 Fingerabdruck-Versuche (Stock-Android erlaubt 20 mit Wartezeiten), wodurch sich die Fingerabdruck-Entsperrung auch abschalten lässt, indem man mit einem anderen Finger absichtlich 5-mal scheitert. [**Offiziell**](#tag-official) Deaktiviere Biometrie, wenn du mit Zwang zum Entsperren rechnest.
- Nutze **Lockdown**, um die biometrische Entsperrung schnell abzuschalten: Drücke Ein-/Aus-Taste + Lauter und tippe dann auf Lockdown. Android kann Lockdown auch im Ein-/Aus-Menü anzeigen, nachdem du Einstellungen → Display → Erweitert → Sperrbildschirm-Anzeige → Lockdown-Option anzeigen aktiviert hast. Bis zum nächsten Entsperren deaktiviert es Benachrichtigungen auf dem Sperrbildschirm, die Entsperrung per Fingerabdruck/Gesicht und Extend Unlock (Google Android-Hilfe: <https://support.google.com/android/answer/9075927?hl=en>). Lockdown ist nicht dasselbe wie Ausschalten oder die Rückkehr des Geräts in den BFU-Zustand; dafür ausschalten oder neu starten. [**Empfehlung**](#tag-advice)

### 4.4 Auto-Reboot, USB-C und weitere Sicherheitseinstellungen

- **Auto-Reboot** startet ein gesperrtes Gerät nach einer festgelegten Zeit neu und versetzt die Daten zurück in den verschlüsselten Ruhezustand (BFU). Standard sind **18 Stunden**; einstellbar von 10 Minuten bis 72 Stunden oder aus. [**Offiziell**](#tag-official) Kürzer schützt mehr und stört mehr.
- **USB-C-Port** (**Einstellungen → Sicherheit → Exploit-Schutz**; die offizielle Usage-Seite schreibt für das übergeordnete Menü auch „Security & privacy“, die Bezeichnung kann also abweichen [**Offiziell**](#tag-official)) hat fünf Modi: Aus, Nur Laden, **Nur Laden, wenn gesperrt** (Standard), Nur Laden, wenn gesperrt, außer vor dem ersten Entsperren, An. [**Offiziell**](#tag-official) Wenn nie USB-Daten nötig sind, nutze „Nur Laden“ (Laden bei deaktivierten USB-Daten) oder „Aus“ (am strengsten; Laden ist auf den ausgeschalteten Zustand oder Fastboot beschränkt), je nach gewünschtem Kompromiss bei der Nutzbarkeit. [**Offiziell**](#tag-official) (grapheneos.org/features#usb-c-pogo-pins-control)
- Automatisches Abschalten von WLAN und Bluetooth gibt es (Bezeichnungen „Turn off Wi-Fi automatically“ und „Turn off Bluetooth automatically“ im Settings-Quelltext von GrapheneOS) [**Offiziell**](#tag-official); eine NFC-Auto-Aus-Einstellung wurde 2025 hinzugefügt und später wegen seltener System-/NFC-HAL-Absturzrisiken vorübergehend wieder entfernt [**Offiziell**](#tag-official) (Release-Notes). Ob sie in der aktuellen Version verfügbar ist, ist ungewiss: Eine verlässliche Bestätigung ihrer Wiederherstellung wurde nicht gefunden. Pfad: Einstellungen → Sicherheit & Datenschutz → Exploit-Schutz (manche GrapheneOS-Abschnitte kürzen das übergeordnete Menü zu „Sicherheit“ ab) enthält „Turn off Wi-Fi automatically“ und „Turn off Bluetooth automatically“ [**Offiziell**](#tag-official) (Settings-Quelltext von GrapheneOS: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/exploit_protection_settings.xml>).

### 4.5 Updates und Update-Kanäle

- Der System-Updater prüft etwa alle sechs Stunden und installiert signierte Updates per Funk. Lass ihn aktiviert. [**Offiziell**](#tag-official)
- Kanäle: **Stable**, **Beta**, **Alpha**. Releases laufen von Alpha über Beta nach Stable. Ein Downgrade ist im Allgemeinen nicht möglich, nimm daher **Stable**, sofern du vorübergehende Probleme nicht in Kauf nehmen willst. [**Offiziell**](#tag-official)
- Updates gehören zu den wertvollsten Gewohnheiten. Starte neu, wenn dazu aufgefordert wird.

---

## 5. Grundlegende Härtung

| Bereich | Was tun | Hinweise |
|---|---|---|
| **Updates** | Automatische Updates an, Stable-Kanal | Support endet, wenn der Hersteller keine Firmware mehr liefert |
| **Qualität der Sperre** | Zufällige PIN ab 6 Ziffern oder Passphrase, PIN-Scrambling | Das Secure Element begrenzt Versuche (insgesamt 20 mit steigenden Wartezeiten) [**Offiziell**](#tag-official) |
| **Sperrzeit** | Kurze Bildschirm-Zeitüberschreitung; Sperre sofort per Ein-/Aus-Taste | Komfort gegen Exposition [**Empfehlung**](#tag-advice) |
| **Auto-Reboot** | 18 h Standard; kürzer bei höherem Risiko | Neustart bringt das Telefon zurück in BFU |
| **USB-Zubehör** | „Nur Laden, wenn gesperrt“ (oder strenger) lassen | Neue USB-Geräte nur im entsperrten Zustand und bei Vertrauen zulassen |
| **Bluetooth / WLAN** | Aus, wenn nicht gebraucht; Auto-Abschaltung nutzen; WLAN nutzt standardmäßig MAC-Randomisierung pro Verbindung [**Offiziell**](#tag-official) | Scan-Schalter unter **Einstellungen → Standort → Standortdienste** sind standardmäßig aus |
| **Standort** | Verweigern oder „nur bei Nutzung“; ungefähren Standort bevorzugen | GrapheneOS leitet SUPL standardmäßig über einen eigenen Proxy und bietet einen Schalter [**Offiziell**](#tag-official) |
| **Kamera / Mikrofon** | Pro Nutzung gewähren („nur diesmal“/„bei Nutzung“) | Globale Schnellschalter nutzen, falls vorhanden |
| **Zwischenablage** | Keine Geheimnisse in geteilte Zwischenablagen kopieren | Zwischenablage zum/vom übergeordneten Profil ist für den Private Space in neueren Versionen sperrbar (Release-Notes 05/2025) [**Offiziell**](#tag-official): Einstellungen → Sicherheit & Datenschutz → Private Space → System → Cross-profile shared clipboard → Disallowed (Settings-Quelltext von GrapheneOS: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/private_space_settings.xml>). Kopiere Geheimnisse nicht in die Standard-Zwischenablage. GrapheneOS Secure Paste bietet eine Standardbeschränkung mit App-spezifischen Ausnahmen: aktivierte Drittanbieter-Apps können keine Zwischenablage-Inhalte lesen, die andere Apps gesetzt haben, aber ihre eigenen. Prüfe die Kompatibilität pro App [**Offiziell**](#tag-official) (grapheneos.org/features#secure-paste) |
| **Sperrbildschirm-Benachrichtigungen** | Sensible Inhalte ausblenden | Einstellungen → Benachrichtigungen (Bezeichnung variiert) |
| **App-Berechtigungen** | Im Berechtigungsmanager und Datenschutz-Dashboard prüfen | Ungenutzte Apps ganz entfernen |
| **Sensoren / Funktionen** | **Sensoren**-Berechtigung nutzen (verweigerte Apps erhalten Nullwerte) und globale Schalter | Kann für neue Apps standardmäßig verweigert werden [**Offiziell**](#tag-official) |

### Browser

Nutze **Vanadium**, den eingebauten gehärteten Chromium, der auch die System-WebView liefert. [**Offiziell**](#tag-official) Chromium-basierte Browser haben laut Projekt die stärkste Sandbox und Site Isolation unter den Browserfamilien. [**Offiziell**](#tag-official) Erwarte nicht, dass Vanadium allein Fingerprinting oder IP-Tracking verhindert: Das Verbergen der IP-Adresse erfordert einen Vermittler wie ein VPN oder Tor. [**Empfehlung**](#tag-advice) JavaScript-JIT ist in Vanadium standardmäßig aus, mit einem Schalter pro Website, und Erweiterungen sind nicht geplant. [**Offiziell**](#tag-official) Zusätzliche Browser vergrößern die Angriffsfläche; installiere sie nur mit gutem Grund.

### DNS und was es wirklich bringt

- Private DNS (DNS-over-TLS) verschlüsselt nur DNS-Anfragen. Die Ziel-IP bleibt sichtbar, und Domainnamen verraten sich weiterhin über TLS-SNI. Es ist „empfohlen, aber kein Ersatz für Tor oder ein VPN“. [**Offiziell**](#tag-official)
- **Standard (Automatisch):** für den normalen Gebrauch beibehalten. Im Automatik-Modus nutzt Android DNS-over-TLS opportunistisch, wenn die DNS-Server des Netzes es unterstützen. Das schützt nur vor passivem Mitlesen, da ein aktiver Angreifer den Rückfall auf unverschlüsseltes DNS erzwingen kann. [**Offiziell**](#tag-official)
- **Eigener Server:** Ein Hostname unter **Einstellungen → Netzwerk & Internet → Private DNS** erzwingt authentifiziertes DNS-over-TLS ohne Rückfall. Private DNS hat Vorrang vor DNS, das eine VPN-App liefert. Websites können deinen DNS-Server erkennen und zum Fingerprinting nutzen. [**Offiziell**](#tag-official)
- **Bei Nutzung eines VPN keinen konfigurierten Private-DNS-Hostnamen verwenden.** GrapheneOS empfiehlt ausdrücklich, Private DNS bei einem VPN in jedem Zweitprofil vollständig auszuschalten, bis dieses Zusammenspiel überarbeitet ist. Ein benannter Private-DNS-Server und automatisches opportunistisches DNS-over-TLS sind nicht dieselbe Einstellung. Jedes Profil hat eine eigene VPN-Konfiguration, Private DNS aber global ist; beides wirkt dann besonders bei mehreren Profilen schlecht zusammen. Laut Release-Notes 07/2025 braucht Android Private DNS im Zusammenspiel mit Zweitprofilen und VPNs zudem eine gründliche Überarbeitung, nachdem zwei VPN-Lecks behoben wurden. [**Offiziell**](#tag-official) Soll mit VPN gefiltert werden, nimm eine VPN-App, die beides kann (z. B. RethinkDNS). [**Offiziell**](#tag-official)
- Die Wahl eines DNS-Anbieters verschiebt das Vertrauen zu diesem Anbieter. Anonym macht sie dich nicht.

---

## 6. Erweiterte Härtung

### 6.1 Benutzerprofile und wann man sie nutzt

Jedes Profil hat eigenen verschlüsselten Speicher, eigene App-Daten und Schlüssel. Das **Owner**-Profil ist besonders: Es speichert sensible systemweite Daten, muss nach einem Neustart zuerst entsperrt werden und sieht die Daten anderer Profile nicht. [**Offiziell**](#tag-official)

Vorgeschlagene Aufteilung [**Empfehlung**](#tag-advice):

| Profil | Zweck |
|---|---|
| Owner | Verwaltung, Updates, App Store, vertrauenswürdige Kern-Apps. Minimal halten |
| Alltag/Persönlich | Normale Apps, wenn nicht alles im Owner-Profil liegen soll |
| Google/nicht vertrauenswürdig | Sandboxed Google Play und Google-abhängige Apps |
| Sensible Identität | Nur für eine getrennte Rolle (siehe [Abschnitt 9](#9-anonymität-realistische-opsec)) |

- Nutze **Sitzung beenden** (Ein-/Aus-Menü oder Benutzerwechsel), wenn du fertig bist. Dadurch werden die Schlüssel des Profils vollständig aus dem Speicher entfernt und das Profil kehrt in den Ruhezustand zurück. Beim Owner-Profil geht das nur per Neustart. [**Offiziell**](#tag-official)
- Sekundäre Profile lassen sich so einstellen, dass sie nicht im Hintergrund laufen. Android-**Private Space** und **Arbeitsprofil** werden ebenfalls unterstützt; GrapheneOS ergänzt in neueren Versionen Einstellungen wie Zwischenablage-Sperre und nicht verzögertes Sperren für den Private Space. [**Offiziell**](#tag-official) (Release-Notes)
- Profile trennen App-Daten und Schlüssel. Sie machen ein Profil weder anonym noch unverknüpfbar: Alle Profile teilen Hardware, SIM, IP-Adresse und deine Gewohnheiten, und eine wiederverwendete Rufnummer, E-Mail-Adresse, ein Name, Kontakt, eine Datei oder ein Schreibstil verknüpft Identitäten wieder. Verstehe Profile als Fächer für Daten, nicht als Tarnung.

### 6.2 App-Isolation

Apps sind standardmäßig voneinander durch die Sandbox getrennt. Härtung heißt hier vor allem: **weniger Apps wählen**, riskante Apps in ein eigenes Profil legen und die untenstehenden Scope-Berechtigungen nutzen.

### 6.3 Storage Scopes und Contact Scopes [**Offiziell**](#tag-official)

- **Storage Scopes**: Eine App, die breiten Dateizugriff will, sieht nur die von dir gewählten Dateien/Ordner statt des gesamten Speichers.
- **Contact Scopes**: Eine App sieht nur die von dir ausgewählten Kontakte.

Nutze sie, wann immer eine App Speicher- oder Kontaktzugriff anfordert.

### 6.4 Netzwerk- und Sensoren-Berechtigung [**Offiziell**](#tag-official)

- Die **Netzwerk**-Berechtigung blockiert direkten und indirekten Netzwerkzugriff pro App (und pro Profil); die App sieht „Netz aus“. Blockiere sie für Offline-Werkzeuge (Rechner, Notizen, Offline-PDF-Betrachter). Der Schalter ist schon bei der App-Installation verfügbar. Aus Kompatibilitätsgründen ist sie standardmäßig erlaubt.
- Die **Sensoren**-Berechtigung deckt Beschleunigungssensor, Gyroskop, Kompass und weitere Sensoren ab, die keine Android-Berechtigung haben; verweigerte Apps erhalten Nullwerte. Sie lässt sich für neu installierte Apps standardmäßig deaktivieren unter **Einstellungen → Sicherheit & Datenschutz → Weitere Sicherheit & Datenschutz**.

### 6.5 PIN-Scrambling, Duress und Geräte-Beschlagnahme

- Aktiviere **PIN-Scrambling** (siehe 4.3).
- **Duress-PIN/-Passwort** [**Offiziell**](#tag-official): Die Eingabe der Duress-PIN/des Duress-Passworts als Gerätezugangsdaten auf dem Sperrbildschirm oder in einer OS-Abfrage nach Gerätezugangsdaten löscht das Gerät unwiderruflich, einschließlich installierter eSIMs. Die Duress-PIN funktioniert auch als PIN der Zwei-Faktor-Fingerabdruck-Entsperrung, aktuell aber nicht als SIM-PIN. Passende echte Entsperrdaten haben Vorrang und löschen nicht. Einrichtung unter **Einstellungen → Sicherheit & Datenschutz → Gerät entsperren → Duress-Passwort** im Owner-Profil. PIN und Passwort müssen beide gesetzt werden. Es ist kein Fernlöschen.

> ⚠️ **Gefahr:** Der Duress-Wipe ist unumkehrbar. Lege vorher ein verschlüsseltes Backup an, teste ihn nie leichtfertig und wähle ihn nicht identisch mit deinen echten Zugangsdaten (die echten haben Vorrang, es würde also nichts gelöscht). Ob du ihn nutzt, ist eine rechtliche und persönliche Risikoentscheidung; das Vernichten von Daten während einer Ermittlung kann je nach Rechtsordnung rechtswidrig oder strafrechtlich relevant sein. Das Löschen von Daten während einer erzwungenen Entsperrung kann in manchen Rechtsordnungen als Behinderung der Ermittlungen gewertet werden. Die Verweigerung der Herausgabe eines Passcodes kann in manchen Rechtsordnungen selbst eine Straftat sein. Hole vor dem Vertrauen auf Duress, Auto-Wipe oder Verweigerungsstrategien lokalen Rechtsrat ein. [**Empfehlung**](#tag-advice) <a id="verify-legal"></a>[**Prüfen**](#verify-legal) Die Regeln deines Landes: Hier wird keine länderspezifische Rechtsaussage gemacht.

- Festplattenverschlüsselung: Daten sind mit Schlüsseln verschlüsselt, die an deine Zugangsdaten und sichere Hardware gebunden sind. **Nach einem Neustart (BFU) sind die Daten am besten geschützt**; nach dem ersten Entsperren (AFU) liegt mehr im Speicher. Kurzer Auto-Reboot und Ausschalten vor Grenzübertritten oder bei Übergabe des Geräts verringern die Exposition, aber nur bei starker Passphrase. Sie überwinden weder Beschlagnahme noch Zwang noch rechtmäßigen Zugriff. [**Empfehlung**](#tag-advice)
- Eine schwache PIN ist die größte Schwäche gegenüber Forensik-Werkzeugen; bei hohem Risiko nutze eine lange Passphrase, die auch gegen einen Angreifer stark bleibt, der die Versuchsbegrenzung des Secure Elements umgeht. [**Empfehlung**](#tag-advice)

### 6.6 Physische Sicherheit und Reisen

- Schalte das Telefon vor Situationen, in denen du die Kontrolle verlieren könntest, aus (oder starte neu).
- Schalte das Telefon vor Kontrollen aus; deaktiviere Biometrie (Lockdown) vor Kontrollen oder wenn Entsperrzwang droht. Kenne vorher die lokalen Regeln zur erzwungenen Entsperrung; eine Verweigerung kann in manchen Rechtsordnungen selbst eine Straftat sein. [**Prüfen**](#verify-legal)
- Erwäge ein Reisegerät oder minimale Daten, wenn du in Hochrisiko-Orte oder -Regionen reist.
- Vermeide öffentliche USB-Ladeports; nutze eigenes Ladegerät und Kabel.
- Prüfe die Auditor-Attestierung, wenn das Gerät außerhalb deiner Kontrolle war; das funktioniert nur, wenn Auditor unmittelbar nach der Installation gekoppelt wurde. [**Empfehlung**](#tag-advice)

### 6.7 Backups ohne Datenschutzloch

- GrapheneOS enthält **Seedvault** für verschlüsselte Backups auf lokalen Speicher oder über eine Storage-Provider-App. Das Projekt plant einen Ersatz, weil Seedvault upstream von einer Gruppe übernommen wurde, die seine Ziele nicht teilt; bis dahin ist es die beste verfügbare Option. [**Offiziell**](#tag-official)
- Halte Backups **verschlüsselt**, den Schlüssel nicht auf demselben Gerät. Teste die Wiederherstellung. Vermeide unverschlüsselte Cloud-Backups. Sichere Duress-Einstellungen oder 2FA-Seeds nicht an einem weniger geschützten Ort als das Telefon. [**Empfehlung**](#tag-advice)

---

## 7. Apps: sichere Installation und Auswahl

### 7.1 Quellen in Reihenfolge der Präferenz [**Empfehlung**](#tag-advice), sofern nicht anders markiert

1. **GrapheneOS App Store**: installiert von GrapheneOS gebaute Apps und Sandboxed Google Play, verteilt weitere Apps aus seinem Repository (darunter Accrescent und den PDF-Betrachter) und aktualisiert sie automatisch. [**Offiziell**](#tag-official)
2. **Offizielle Entwickler-Releases** (z. B. GitHub-Releases) mit **Signatur-/Hash-Prüfung**; Updates musst du dann selbst verfolgen.
3. **Accrescent**: ein separater App Store mit Fokus auf Sicherheit und Datenschutz. Laut eigener Seite befindet er sich in der Alpha-Phase und ist im GrapheneOS App Store verfügbar (das App-Repository des Projekts enthält ihn). [**Offiziell**](#tag-official) Er ist hier wegen der Alpha-Phase unterhalb verifizierter Entwickler-Releases eingeordnet. [**Empfehlung**](#tag-advice)
4. **F-Droid**: ausschließlich Open-Source-Apps. Apps mit reproduzierbaren Builds werden mit der Signatur des Entwicklers veröffentlicht, nachdem F-Droid den Build geprüft hat, andere Apps werden mit F-Droids eigenen Schlüsseln signiert, und F-Droid baut nach eigenem Zeitplan, daher können Updates verzögert kommen (siehe 7.5). Bevorzuge, wenn vorhanden, den Kanal des Entwicklers. Nutze F-Droid für Apps, die es anderswo nicht gibt, und installiere nur, was du brauchst.
5. **Aurora Store**: ein alternatives Play-Frontend. Es braucht weiterhin ein Google-Konto, holt aber standardmäßig geteilte Zugangsdaten vom Aurora-Dienst. [**Offiziell**](#tag-official) (Usage-Leitfaden) Play-Apps sind meist Closed Source [**Empfehlung**](#tag-advice) (allgemeine Schlussfolgerung), daher nur als letzter Ausweg. [**Empfehlung**](#tag-advice) Updates von Google Play-Diensten/Google Play Store werden nur vom GrapheneOS App Store oder dem Google Play Store selbst akzeptiert. [**Offiziell**](#tag-official) (Release-Notes)
6. **Manuelle APK**: nur wenn nötig. Prüfe den vom Entwickler veröffentlichten Fingerabdruck des Signaturzertifikats (z. B. mit `apksigner verify --print-certs datei.apk`) oder die Prüfsumme über einen vom Download getrennten Kanal. Gib „Unbekannte Apps installieren“ nur einer bestimmten App und entziehe es danach wieder.

> ⚠️ **Warnung:** Zufällige APK-Seiten, modifizierte oder „gecrackte“ Apps, Root (Magisk), LSPosed/Xposed und inoffizielle ROMs schwächen oder entfernen das Sicherheitsmodell. Root bricht die Verified-Boot-Garantien; Module laufen mit extremen Rechten. Lass es.

### 7.2 App vor der Installation bewerten [**Empfehlung**](#tag-advice)

- Wer veröffentlicht sie? Open Source? Aktuelle Updates? Unabhängiges Audit?
- Was fordert sie an? Braucht sie überhaupt Netzwerk/Kontakte/Standort?
- Braucht die Funktion ein Konto? Bevorzuge Apps, die offline funktionieren.
- Wie finanziert sie sich (Werbung, Analyse-SDKs)?
- Braucht sie Google Play-Dienste? Geht es auch über eine Web-Version oder Alternative?
- Nach der Installation: alles Unnötige verweigern, Netzwerk blockieren, wenn nicht nötig, dann testen.

### 7.3 Prinzip der minimalen Berechtigungen

Weniger Apps, weniger Berechtigungen, weniger Konten. Meide aufgeblähte, geschlossene, telemetriestarke Apps, wenn es eine einfache Alternative gibt. Installiere keine „Privacy“-Apps nur wegen des Namens.

### 7.4 Beispielauswahl (keine offiziellen Empfehlungen, außer wo angegeben) [**Empfehlung**](#tag-advice)

| Kategorie | Vorschlag | Alternative | Hinweise |
|---|---|---|---|
| Browser | **Vanadium** (eingebaut) | Tor Browser für bestimmte Zwecke | Schwächere Sicherheit als Vanadium; siehe Abschnitt 9. Nicht viele Browser installieren |
| Messenger | **Signal** | Andere geprüfte E2EE-Messenger | Ende-zu-Ende-verschlüsselt. Die Signal-Registrierung erfordert eine Rufnummer. Benutzernamen können deine Rufnummer vor anderen Nutzern verbergen, heben aber weder die Rufnummernpflicht auf noch beseitigen sie alle Metadaten-Exposition. Signal ist nicht im GrapheneOS-App-Repository [**Offiziell**](#tag-official). Signal ist im am 6. November 2026 geprüften Repository-Katalog von Accrescent nicht gelistet (Zeitstempel des Katalogs: 25. Februar 2026; die Verfügbarkeit kann sich ändern; <https://repo.accrescent.app/repodata.1.json>). Nutze stattdessen die Website-APK von Signal, Google Play oder eine andere ausdrücklich geprüfte Quelle (siehe 7.5). Prüfe das Repository erneut, wenn sich die Verfügbarkeit ändert. |
| 2FA/Authenticator | **Aegis** (Open Source) | Hardware-Sicherheitsschlüssel (FIDO2) | Tresor verschlüsselt sichern; Wiederherstellungscodes offline |
| Passwortmanager | **KeePassDX** oder Bitwarden | KeePassXC am Computer | Lokale Datenbank vermeidet ein Cloud-Konto |
| VPN-Client | Offizielle **Mullvad**- oder **WireGuard**-App | RethinkDNS (VPN + Filter) | Die GrapheneOS-FAQ empfiehlt die offizielle WireGuard-App und die offizielle Mullvad-App. Die VPN-Wahl hängt von Vertrauen, Rechtsordnung, Logging-Richtlinie, Zahlungsmethode und Bedrohungsmodell ab [**Offiziell**](#tag-official) |
| Karten/Navigation | **Organic Maps** oder OsmAnd | Web-Karten im Browser | Offline-Karten brauchen kein Netz |
| E-Mail | **Proton Mail** o. ä. mit E2E-Möglichkeit | Selbst gehostet | E-Mail ist metadatenreich; Anonymität gibt es dadurch nicht. Laut Datenschutzerklärung von Proton speichert es standardmäßig keine dauerhaften IP-Protokolle, kann IP-Protokolle aber vorübergehend zur Missbrauchsbekämpfung führen und gibt nur begrenzte Daten heraus, wenn es gesetzlich verpflichtet ist; andere Anbieter weichen ab |
| Cloud/Speicher | **Cryptomator** über einen Speicher deiner Wahl | Nur lokal | Vor dem Hochladen verschlüsseln |
| Notizen | **Standard Notes**, Joplin oder lokale Notiz-App | Netzwerk blockieren bei Offline-Notizen | Standard Notes wird weiter gepflegt (quelloffen, Ende-zu-Ende-verschlüsselt; seit 2024 mit Proton verbunden) |
| Kamera/Galerie | **GrapheneOS Kamera** (eingebaut) | | Vor dem Teilen EXIF-/Standorteinstellungen prüfen |
| PDF/Office | Eingebauter **PDF-Betrachter** | Offline-Office mit blockiertem Netzwerk | Dokumente können Metadaten enthalten |

Bezeichne eine App nur dann als anonym, wenn sie es technisch ist. „No-Logs“-VPNs, „private“ E-Mail und „verschlüsselte“ Notizen decken jeweils nur bestimmte Risiken ab.

### 7.5 App-Store-Vergleich

Jeder der folgenden Stores installiert Apps in die normale App-Sandbox. Die Unterschiede liegen darin, ob ein Konto nötig ist, wie Updates ankommen und wem du vertrauen musst. Aussagen zu Stores von Drittanbietern stammen aus der Dokumentation des jeweiligen Projekts (siehe Quellen); die Empfehlungen sind die Einschätzung dieses Leitfadens.

| Store | Konto nötig? | Google-Abhängigkeit | Update-Mechanismus | App-Auswahl (Umfang, Qualität) | Sicherheitsmodell | Empfehlung: Alltag / Cryptophone |
|---|---|---|---|---|---|---|
| **GrapheneOS App Store** | In der GrapheneOS-Dokumentation wird kein Konto als Voraussetzung genannt [**Offiziell**](#tag-official) | Keine für den Store selbst; er kann zusätzlich Sandboxed Google Play installieren, das optional ist [**Offiziell**](#tag-official) | Aktualisiert die Apps aus seinem Repository im Hintergrund, einschließlich der Komponenten von Sandboxed Google Play [**Offiziell**](#tag-official) | Klein: eigene GrapheneOS-Apps (zum Beispiel Kamera, PDF-Betrachter, Auditor, Vanadium), die Komponenten von Sandboxed Google Play und einige weitere wie der Accrescent-Client [**Offiziell**](#tag-official) | Das App-Repository von GrapheneOS und sein Client, vom GrapheneOS-Projekt gepflegt und in das Betriebssystem integriert [**Offiziell**](#tag-official) | Alltag: erste Wahl. Cryptophone: erste Wahl; Sandboxed Google Play nur installieren, wenn eine benötigte App sonst nicht funktioniert ([Abschnitt 8](#8-sandboxed-google-play)) [**Empfehlung**](#tag-advice) |
| **Accrescent** | Kein Konto nötig | Vom Projekt keine genannt | Automatische, unbeaufsichtigte Updates ohne Sonderrechte ab Android 12 | Kleiner, kuratierter Katalog; das Projekt befindet sich in der Alpha-Phase | Pinning des App-Signaturschlüssels bei der Erstinstallation, signierte Repository-Metadaten und kein Remote-APK-Signieren, sodass Entwickler ihre Signaturschlüssel behalten | Alltag: für die Apps nutzen, die er führt. Cryptophone: ebenso. Den Client aus dem GrapheneOS App Store installieren, wie es die Seite von Accrescent für GrapheneOS-Nutzer empfiehlt. In der Quellenreihenfolge von 7.1 steht er nur wegen der Alpha-Phase unter verifizierten Entwickler-Releases [**Empfehlung**](#tag-advice) |
| **F-Droid** | Kein Konto nötig; F-Droid sagt, es verfolge nicht, was du installierst | Keine Google-Abhängigkeit genannt; ein unabhängiges Repository freier und quelloffener Apps | Über den F-Droid-Client; die Geschwindigkeit hängt von der App ab, denn F-Droid baut nach eigenem Zeitplan, und manche Apps sind veraltet oder hinken dem Entwickler hinterher [**Empfehlung**](#tag-advice) | Großer Katalog freier und quelloffener Apps; Qualität und Update-Tempo schwanken je App und Repository [**Empfehlung**](#tag-advice) | Apps werden vor der Aufnahme auf Sicherheitsprobleme geprüft. Bei Apps mit reproduzierbaren Builds veröffentlicht F-Droid die Signatur des Entwicklers, nachdem es den Build geprüft hat; andere Apps werden mit F-Droids eigenen Schlüsseln signiert | Alltag: Ausweichlösung für Apps, die die obigen Stores nicht führen; prüfen, ob die App gepflegt wird. Cryptophone: nur als Ausweichlösung (Regel in 7.1) [**Empfehlung**](#tag-advice) |
| **Aurora Store** | Ja, ein Google-Konto ist nötig. Standardmäßig holt er geteilte Konto-Zugangsdaten vom Dienst von Aurora Store (geteilte Dummy-Konten, die über Token-Dispenser ausgegeben werden); du kannst dich auch mit deinem persönlichen Google-Konto anmelden [**Offiziell**](#tag-official) | Vollständig: Er ist ein alternatives Frontend des Google Play Stores [**Offiziell**](#tag-official) | Aktualisiert die Play-Apps, die er installiert hat. GrapheneOS akzeptiert Updates von Google Play-Diensten, Google Services Framework und Google Play Store nur von seinem eigenen App Store oder vom Play Store selbst, nutze Aurora dafür also nicht [**Offiziell**](#tag-official) | Der für das gewählte Konto und Gerät angezeigte Play-Katalog, einschließlich Kompatibilitäts- und Verteilungsbeschränkungen; die meisten gelisteten Apps sind Closed Source [**Empfehlung**](#tag-advice) | Von Entwicklern signierte Play-Apps, aber die Installationen laufen über Google unter einem geteilten oder einem persönlichen Konto. Geteilte Dummy-Konten sind keine Anonymität: Du verlässt dich auf den Dispenser-Dienst, das Konto teilen sich viele andere Nutzer, und Google kann Geräteinformationen und Installationen weiterhin korrelieren; ein persönliches Konto bindet die Installationen an dich [**Empfehlung**](#tag-advice) | Alltag: letzter Ausweg, nur in einem separaten Profil und nie mit deinem Haupt-Google-Konto. Cryptophone: nicht nutzen [**Empfehlung**](#tag-advice) |
| **Obtainium** | Kein Store-Konto; Obtainium kann konfigurierte Release-Quellen verfolgen. Manche unterstützten Quellen werden vom Entwickler kontrolliert (zum Beispiel ein GitHub- oder GitLab-Release des Entwicklers); andere sind Mirrors oder Aggregatoren. Bewerte jede konfigurierte Quelle einzeln und bevorzuge vom Entwickler kontrollierte URLs im Vertrauensmodell dieses Leitfadens | Keine, sofern die App selbst Google nicht braucht | Prüft die von dir eingerichteten Release-Seiten, benachrichtigt dich über neue Releases und installiert sie; es ist kein Store mit eigener Prüfung | Alle Apps, die auf unterstützten Release-Seiten APKs veröffentlichen; jede Quelle wählst und richtest du selbst ein. Es unterstützt auch Aggregator- und Mirror-Seiten (zum Beispiel APKPure, Aptoide, Uptodown und APKMirror nur zum Verfolgen) und F-Droid-Repositories von Drittanbietern; APKs von dort werden von Dritten gehostet oder neu verpackt, prüfe also das Signaturzertifikat gegen das des Entwicklers [**Empfehlung**](#tag-advice) | Nur so stark wie dein Vertrauen in jede Quelle und deine Prüfung: Es macht ein unsigniertes oder kompromittiertes Release nicht sicher. Obtainium selbst veröffentlicht einen Fingerabdruck des Signaturzertifikats und einen PGP-Schlüssel zur Prüfung (Obtainium-README, Abschnitt „Installation“); sein Quelltext liegt auf GitHub (<https://github.com/ImranR98/Obtainium>) | Alltag: optionale Hilfe für Apps, die nur als APK verteilt werden und die die obigen Stores nicht führen. Cryptophone: nicht standardmäßig; es fügt eine App mit der Berechtigung „Unbekannte Apps installieren“ und Netzwerkzugriff hinzu, nutze es also nur bei dokumentiertem Bedarf und prüfe jede Quelle [**Empfehlung**](#tag-advice) |
| **Manueller APK-Download** | Kein Store-Konto; die Seite des Entwicklers entscheidet | Keine, sofern die App selbst Google nicht braucht | Der Website-Build von Signal verwaltet Update-Prüfungen und Downloads selbst; für die Installation kann weiterhin eine Bestätigung über den Paketinstaller von Android nötig sein. Prüfe das Signaturzertifikat bei der Erstinstallation (signal.org/android/apk nennt den SHA-256-Fingerabdruck und eine apksigner-Prüfung). Andere manuell heruntergeladene APKs erfordern womöglich weiterhin manuelle Update-Verfolgung und Downloads | Was der Entwickler veröffentlicht; nicht jede App bietet eine APK | Hängt ganz von deiner Prüfung ab: Vergleiche den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal, gib „Unbekannte Apps installieren“ nur einer App und entziehe es danach wieder [**Empfehlung**](#tag-advice) | Alltag: nur, wenn eine App sonst nirgends erhältlich ist. Cryptophone: nur für anderswo nicht erhältliche Apps (zum Beispiel Signal); Signatur prüfen und von Hand aktualisieren [**Empfehlung**](#tag-advice) |

**Verbleibendes Risiko:** Der gewählte Store ändert, wer erfährt, welche Apps du installierst, und wie schnell Korrekturen dich erreichen. Er macht eine App nicht vertrauenswürdig, und kein Anmeldemodus eines Google-basierten Stores macht dich anonym.

---

## 8. Sandboxed Google Play

### Was es ist [**Offiziell**](#tag-official)

Eine Kompatibilitätsschicht, mit der du die **offiziellen** Google Play-Dienste und den Google Play Store als **normale Sandbox-Apps** installieren kannst. Beide erhalten keine Sonderrechte und keinen Systemzugriff und erreichen nur, was du ihnen wie jeder App gewährst. GrapheneOS nutzt Google Play-Dienste auch bei Installation nicht für Betriebssystemfunktionen. Apps in einem Profil können sie nur verwenden, wenn sie in diesem Profil installiert sind und die App sie ausdrücklich nutzt.

### Es ist optional

Viele Apps laufen auch ohne. Nutze möglichst viel ohne Google Play und behandle Play als Ausnahme. [**Offiziell**](#tag-official)

### Wann sinnvoll, wann vermeiden

| Installieren, wenn | Vermeiden, wenn |
|---|---|
| Eine benötigte App (Bank, Verkehr, Arbeit) ohne sie nicht läuft | Du deine Apps auch ohne sie betreiben kannst |
| Du Push-Benachrichtigungen von Google-abhängigen Apps brauchst | Dein Bedrohungsmodell Google ausschließt |
| Du sie vom Hauptprofil fernhalten willst | Du dich mit deinem Haupt-Google-Konto in einem Profil mit sensiblen Daten anmelden würdest |

### Installation [**Offiziell**](#tag-official)/[**Empfehlung**](#tag-advice)

1. Öffne den **App Store** und wähle **Google Play services**. Dadurch werden Google Play-Dienste und Google Play Store gemeinsam installiert (sie hängen voneinander ab). Entferne den Google Services Framework nicht, falls er aus einer Installation vor Android 15 vorhanden ist.
2. Wähle den Installationsort. **Owner-Profil:** der einfachste Weg (so nennt es die offizielle Anleitung), aber weniger isoliert; vertretbar, wenn du Google-Software in deiner Hauptumgebung akzeptierst. [**Empfehlung**](#tag-advice) **Separates Benutzer- oder Arbeitsprofil:** **empfohlen für datenschutzbewusste Nutzer und höheres Risiko**, weil nur die Apps in diesem Profil es nutzen können und das Owner-Profil (das sensible systemweite Daten hält) frei von Google-Software bleibt. [**Empfehlung**](#tag-advice) Der Cryptophone-Leitfaden ist strenger und erlaubt nur die Variante mit separatem Profil.
3. Gib den **Google Play-Diensten** eine **Ausnahme von der Akkuoptimierung**, wenn du zuverlässige Push-Benachrichtigungen brauchst (für den Google Play Store nicht nötig).
4. Optionale Konfiguration unter **Einstellungen → Apps → Sandboxed Google Play**.

### Berechtigungen minimieren [**Offiziell**](#tag-official)/[**Empfehlung**](#tag-advice)

- Standardmäßig werden Google-Play-Standortanfragen auf den Standortdienst des Betriebssystems umgeleitet, sodass du Google Play-Diensten keinen Standort gewähren musst. Lass es dabei.
- Verweigere Kontakte, SMS, Telefon, Kamera, Mikrofon, solange eine App sie nicht braucht. Gib Google Play-Diensten nie „Immer zulassen“ beim Standort.
- Deaktiviere die Werbe-ID, wo angeboten.

### Risiken und Abwägungen

- Ein Google-Konto ist **nicht anonym**. Die Anmeldung verknüpft das Profil mit einer Identität bei Google. Die Anmeldung ist optional, außer du willst Installationen über den Google Play Store, In-App-Käufe oder kontoabhängige App-Funktionen. [**Offiziell**](#tag-official) Google kann außerdem sehen, welche Apps du installierst und Geräteinformationen erhalten; gehe davon aus. [**Empfehlung**](#tag-advice)
- Beim Anlegen eines Google-Kontos wird häufig eine Telefonnummern-Verifizierung verlangt. [**Empfehlung**](#tag-advice)
- Ein separates Profil begrenzt den Datenzugriff, verhindert aber nicht, dass Google das Konto über IP-Adresse, Geräteeigenschaften, Zeitpunkte oder Kontoaktivität korreliert. [**Empfehlung**](#tag-advice)
- Die Kompatibilität ist hoch, aber nicht vollständig. Einige privilegierte Funktionen fehlen. [**Offiziell**](#tag-official)
- Profilisolierung: Google-abhängige Apps in ein Profil, sensible Daten und Identitäten in ein anderes, und Zwischenablage/Dateien nicht zwischen beiden teilen.
- Updates kommen über den GrapheneOS App Store.

---

## 9. Anonymität: realistische OPSEC

### Warum ein Telefon allein nicht anonym macht

Ein Telefon ist ein Bündel von Kennungen und ein Ortungssensor. Softwarehärtung ändert nicht, was Netz, Netzbetreiber oder genutzte Dienste sehen können.

| Faktor | Was er offenbart / verknüpft |
|---|---|
| **SIM/eSIM, IMSI, Rufnummer** | Identifizieren dich gegenüber dem Netzbetreiber. Betreiber protokollieren genutzte Funkzellen (Standort). Eine eSIM hat eine eigene Kennung (EID); die Anforderungen bei der Aktivierung hängen vom Netzbetreiber und vom Land ab <a id="verify-esim"></a>[**Prüfen**](#verify-esim) (keine allgemeingültige Primärquelle für Anforderungen an Konto, Ausweis oder Zahlung gefunden). Registrierungspflichten sind länderabhängig |
| **IMEI** | Hardwarekennung des Geräts, die das Netz sieht; SIM-Wechsel ändert sie nicht. Betreiber können IMSI/IMEI-Paare protokollieren, sodass eine neue SIM im selben Telefon oder eine alte SIM in einem neuen Telefon Identitäten verknüpfen kann; EFF: Das Netz beobachtet SIM und Gerät gemeinsam |
| **Mobilfunk-Metadaten** | Anruf-/SMS-/Datenverbindungen, Funkzellen, Zeitpunkte. Ein VPN verbirgt nicht, dass dein Telefon sich ins Netz einbucht. Anrufe, SMS und VoLTE sind Netzbetreiberdienste und werden von einem VPN nicht abgedeckt |
| **IP-Adresse** | Von jedem kontaktierten Server gesehen; nur durch VPN/Tor verborgen (Vertrauen verschiebt sich) |
| **Konten, E-Mail, Rufnummer bei Registrierungen** | Verknüpfen Aktivitäten über Dienste hinweg |
| **Zahlungsmittel, Lieferadressen** | Starke Verbindungen zur realen Welt |
| **Bluetooth/WLAN/Standort** | Korrelation über Geräte in der Nähe und Orte |
| **App-Telemetrie, Geräte-Fingerabdrücke** | App- und sitzungsübergreifende Korrelation |

### Öffentliches WLAN, VPN und Tor

| Werkzeug | Hilft bei | Hilft nicht bei |
|---|---|---|
| **Öffentliches WLAN** | Trennt den Verkehr von deiner Heim-IP | Konto-Logins, Zahlungen, Mobilfunknetz, WLAN-Betreiber sieht Verkehr. Captive Portals können Rufnummer oder E-Mail-Adresse verlangen, und Videoüberwachung, Zahlungsbelege und Standortmuster können eine Person weiterhin einem Ort zuordnen. GrapheneOS randomisiert die MAC-Adresse standardmäßig pro Verbindung [**Offiziell**](#tag-official) |
| **VPN** | Verbirgt Ziele und Inhalte vor lokalem Netz/Provider (dass ein VPN genutzt wird, bleibt sichtbar); verbirgt deine IP vor Seiten | Verschiebt Vertrauen zum VPN-Anbieter; verbirgt weder Mobilfunk-Standort noch Konten noch Verhalten; leckt bei Fehlkonfiguration. Nutze **Always-on-VPN + „Verbindungen ohne VPN blockieren“** [**Offiziell**](#tag-official). Bei aktiver Sperre lässt sich ein Captive-Portal-Login nicht abschließen; hebe sie nur vorübergehend auf, wenn du das in Kauf nimmst. [**Empfehlung**](#tag-advice) |
| **Tor** | Verbirgt deine IP vor Seiten durch Mehrfach-Routing | Verbirgt nicht, was du durch Logins oder Inhalte preisgibst; macht Verkehr auffällig; langsam; Exit-Knoten sehen unverschlüsselten Verkehr |

- **Wann ein VPN hilft:** in nicht vertrauenswürdigen Netzen, zum Verbergen vor lokalem Provider oder einer Seite, oder um aus einer stabilen IP-Region aufzutreten. **Wann nicht:** du meldest dich in Konten an, die auf dich laufen, oder die Bedrohung ist der Netzbetreiber oder der VPN-Anbieter selbst.
- **Tor auf dem Handy:** Laut Projekt ist die Sicherheit des Tor Browsers im Vergleich zu Vanadium schwach, und Tor kann einen selbst zu einem interessanteren Ziel machen. [**Offiziell**](#tag-official) Wer starke Tor-Anonymität braucht, ist mit einer eigenen Umgebung, also einem separaten Gerät oder einem separaten Betriebssystem und nicht bloß einer separaten App, besser bedient als mit einem Alltagstelefon. App-Routing über Orbot oder Tor VPN ersetzt die Nutzungsregeln des Tor Browsers nicht, und das Tor Project sagt, die Tor-VPN-Beta solle nicht für sensible Aktivitäten genutzt werden. Ein GrapheneOS-Maintainer schrieb 2020 im Issue-Tracker des Projekts, Orbot sei schlecht umgesetzt und gepflegt und das Projekt werde es weder forken noch bündeln. [**Offiziell**](#tag-official) FAQ und Usage-Seiten nennen keine Tor-App.
- Android erlaubt ein VPN pro Profil; stapele VPN-Apps nicht blind.

### Getrennte Identitäten statt nur Werkzeuge

Für eine legitim getrennte Rolle (z. B. berufliche oder aktivistische Identität):

1. Nutze ein **eigenes Profil** ohne Kontakte, Dateien, Konten oder Backups deiner persönlichen Identität.
2. Verwende separate E-Mail-Adressen/Konten, die du in diesem Profil anlegst und nirgends sonst nutzt.
3. Melde dich dort nie in persönlichen Konten an; verwende keine Benutzernamen, Avatare, Schreibstile oder Zeitpläne doppelt.
4. Teile keine Dateien, Zwischenablage oder Benachrichtigungen zwischen den Profilen.
5. Bedenke, dass dieselbe SIM, dasselbe Gerät, dasselbe Heim-WLAN, derselbe Standort und dieselben Zeiten die Profile untereinander und mit dir verknüpfen.
6. Entferne Metadaten (EXIF, Dokumenteigenschaften) vor dem Teilen.

**Bei einem Bedrohungsmodell mit hohem Risiko sind ein separates Gerät, eine separate SIM/eSIM und ein getrenntes Netzwerknutzungsmuster die realistische Grenze. Profiltrennung allein ist Kompartimentierung, keine vollständige Grenze.**

Das verringert unnötige Datenspuren und begrenzt Verknüpfungen. Es erzeugt keine Anonymität und muss im Rahmen des Gesetzes bleiben. Dieser Leitfaden hilft nicht, rechtmäßige Ermittlungen zu umgehen.

---

## 10. Checklisten für den Alltag

### Einrichtungstag
- [ ] Unterstütztes Pixel mit verbleibender Supportdauer geprüft
- [ ] Über offiziellen Installer installiert; **Bootloader gesperrt**
- [ ] Verified-Boot-Schlüssel-Hash geprüft (oder Auditor genutzt)
- [ ] OEM-Entsperrung aus; USB-Debugging aus
- [ ] Updates installiert; Kanal Stable
- [ ] Starke PIN/Passphrase; PIN-Scrambling an
- [ ] Auto-Reboot gesetzt; USB-C „Nur Laden, wenn gesperrt“ oder strenger
- [ ] Standort, Kamera, Mikrofon, Kontakte, Speicher geprüft
- [ ] Profile bei Bedarf angelegt; Backups eingerichtet und getestet

### Wöchentlich / monatlich
- [ ] Updates installiert und neu gestartet
- [ ] Datenschutz-Dashboard und Berechtigungen prüfen
- [ ] Ungenutzte Apps und Profile entfernen
- [ ] Bei VPN-Nutzung Kill-Switch-Verhalten prüfen
- [ ] Wiederherstellung des Backups testen

### Vor Reisen
- [ ] Aktualisieren und neu starten; Backup; unnötige Daten entfernen
- [ ] Kurzen Auto-Reboot setzen; stärkere Passphrase erwägen
- [ ] Über Biometrie entscheiden (deaktivieren/Lockdown)
- [ ] Lokale Gesetze zu Gerätedurchsuchung und Verschlüsselung kennen
- [ ] Rechtliche und persönliche Risiken der Duress-Funktion kennen, bevor du sie nutzt
- [ ] Eigenes Ladegerät mitnehmen; öffentliche USB-Ports meiden

### Nach der Installation einer neuen App
- [ ] Quelle verifiziert (App Store / Entwicklersignatur)
- [ ] Alle unnötigen Berechtigungen verweigert; Storage-/Contact-Scopes nutzen
- [ ] Netzwerk blockieren, wenn sie offline funktioniert
- [ ] Sensoren-Berechtigung verweigert, wenn nicht nötig
- [ ] In passendes Profil gelegt
- [ ] Deinstallieren, wenn sie einen Monat nicht genutzt wird

---

## 11. Häufige Fehler

| Fehler | Warum es schadet | Besser |
|---|---|---|
| Zu viele „Privacy“-Apps installieren | Jede App vergrößert Angriffsfläche und Vertrauensbedarf | Minimum installieren |
| VPNs blind vertrauen | Anbieter sieht Verkehr; Lecks passieren | Wissen, wovor es schützt; Kill-Switch nutzen |
| Schwache PIN | Brute-Force-/Forensikrisiko | Lange zufällige PIN oder Passphrase |
| Bootloader entsperrt lassen | Volles Verified Boot deaktiviert; nicht unterstützt | Nur nach erfolgreichem, verifiziertem Flash sperren |
| Zufällige APKs installieren | Schadsoftware, keine verifizierten Updates | Vertrauenswürdige Quellen, Signaturen prüfen |
| Sensible und normale Identität in einem Profil mischen | Korrelation | Getrennte Profile und Konten |
| Glauben, GrapheneOS allein liefere Anonymität | SIM, Netz, Konten identifizieren dich weiterhin | Abschnitt 9 lesen |
| Google-Dienste ohne Kenntnis der Abwägung nutzen | Konto verknüpft Aktivität mit dir | Isoliertes Profil, minimale Berechtigungen oder verzichten |
| Ein konfigurierter Private-DNS-Server zusammen mit einem VPN | Offizielle Empfehlung: Private DNS ist global, VPNs gelten pro Profil; es hat Vorrang vor VPN-DNS | Private DNS bei VPN-Nutzung auf Aus stellen |
| Duress leichtfertig testen | Unumkehrbarer Wipe | Backup; nie auf einem Gerät mit Daten testen |

---

## 12. Schnellreferenz-Tabellen

### Einstellungen

| Einstellung | Empfohlener Wert | Warum | Risiko bei Missachtung |
|---|---|---|---|
| Bootloader | Gesperrt | Volles Verified Boot | Manipulation, nicht unterstützte Installation |
| OEM-Entsperrung | Aus | Verhindert Entsperren ohne Zugriff auf das Betriebssystem | Leichteres Flashen eines modifizierten Systems |
| Bildschirmsperre | Zufällige PIN ab 6 Ziffern / Passphrase | Widersteht Raten | Leichtes Entsperren |
| PIN-Scrambling | An | Erschwert Mitlesen | Code wird beobachtet |
| Auto-Reboot | 18 h (Standard) oder kürzer | Bringt Daten zurück in BFU | Daten bleiben länger in AFU |
| USB-C-Port | Nur Laden, wenn gesperrt (oder strenger) | Verringert die USB-Angriffsfläche | Exposition gegenüber USB-Datenangriffen |
| Updates / Kanal | Automatisch, Stable | Sicherheitskorrekturen | Bekannte Schwachstellen |
| Standort | Aus / bei Nutzung / ungefähr | Weniger Tracking | Dauerhafte Standortspur |
| Netzwerk-Berechtigung | Für Offline-Apps blockieren | Blockiert Telemetrie über das Netzwerk | Verdeckte Datenabflüsse |
| Sensoren-Berechtigung | Für neue Apps standardmäßig verweigern | Begrenzt Sensor-Seitenkanäle | Fingerprinting/Seitenkanäle |
| Private DNS | Normalerweise Automatisch (Standard); Aus bei VPN-Nutzung | Automatisch verschlüsselt opportunistisch; ein konfigurierter Server kollidiert mit profilbezogenen VPNs | VPN-Konflikte, Lecks, seltsames Verhalten |
| Google Play | Optional, isoliertes Profil | Begrenzt Googles Reichweite | Kontobasiertes Profiling |
| Duress | Optional, mit Backup | Optionale Wipe-Funktion; keine allgemeine Schutzmaßnahme gegen Beschlagnahme | Versehentlicher unumkehrbarer Wipe |

### Apps

| App-Typ | Empfohlene Option | Alternative | Hinweise |
|---|---|---|---|
| Browser | Vanadium | Tor Browser (Sonderfälle) | Schwächere Sicherheit als Vanadium; siehe Abschnitt 9. Nicht viele hinzufügen |
| Messenger | Signal | Andere geprüfte E2EE | Registrierung erfordert eine Rufnummer; Benutzernamen verbergen sie nur vor anderen Nutzern |
| 2FA | Aegis | FIDO2-Schlüssel | Wiederherstellung offline |
| Passwortmanager | KeePassDX | Bitwarden | Lokale DB oder vertrauenswürdige Synchronisierung |
| VPN | Mullvad / WireGuard | RethinkDNS | Die offizielle FAQ empfiehlt diese beiden Apps; die Wahl hängt von Vertrauen, Rechtsordnung, Logging, Zahlung und Bedrohungsmodell ab |
| Karten | Organic Maps | OsmAnd | Offline |
| E-Mail | Proton Mail | Selbst gehostet | Metadaten bleiben; Anbieter können IPs vorübergehend protokollieren und müssen bei gesetzlicher Pflicht Daten herausgeben (Datenschutzerklärung von Proton) |
| Speicher | Cryptomator | Nur lokal | Zuerst verschlüsseln |
| Notizen | Standard Notes / Joplin | Lokale Notizen | Netzwerk blockieren, wenn offline |
| Kamera | GrapheneOS Kamera | | Metadaten prüfen |
| PDF | Eingebauter PDF-Betrachter | | Metadaten entfernen |

### Bedrohungsstufe

| Stufe | Hauptprioritäten | Empfohlenes Setup |
|---|---|---|
| Grundlegend | Updates, Sperre, gesperrt bleiben | Offizielle Installation, gesperrter Bootloader, PIN ab 6 Ziffern, wenige Apps |
| Starker Datenschutz (Alltag) | Berechtigungen, Profiltrennung, weniger Google | Oben plus Scopes, Netzwerk-/Sensoren-Berechtigung, optional isoliertes Play-Profil, VPN mit Kill-Switch |
| Höhere OPSEC | Verringerte Beschlagnahme-Exposition durch BFU-Zustand und starke Passphrase, Identitätstrennung, Disziplin | Oben plus Passphrase, kurzer Auto-Reboot, strenge USB-Einstellung, getrennte Identitätsprofile, Reiseplan, Auditor, fachkundige Beratung |

---

## 13. Quellen

**Offizielle GrapheneOS-Dokumentation (primär).** Alle [**Offiziell**](#tag-official)-Aussagen oben stammen von diesen Seiten:

- Startseite: <https://grapheneos.org/>
- Installationsübersicht: <https://grapheneos.org/install/>
- Web-Installer: <https://grapheneos.org/install/web>
- CLI-Installer: <https://grapheneos.org/install/cli>
- Usage-Leitfaden: <https://grapheneos.org/usage>
- Features: <https://grapheneos.org/features>
- FAQ: <https://grapheneos.org/faq>
- Releases und Changelog: <https://grapheneos.org/releases>
- Auditor / Attestierung: <https://attestation.app/>

**Weitere technische Quellen (sekundär; nur als Kontext, nicht für offizielle Aussagen):**

- Accrescent: <https://accrescent.app/>
- Obtainium: <https://github.com/ImranR98/Obtainium>
- Google Android-Hilfe, Lockdown: <https://support.google.com/android/answer/9075927?hl=en>
- F-Droid: <https://f-droid.org/en/about/> und <https://f-droid.org/docs/FAQ_-_App_Developers/>
- Mullvad VPN: <https://mullvad.net/>
- Tor Project: <https://www.torproject.org/>
- Signal, Rufnummern-Datenschutz und Benutzernamen: <https://signal.org/blog/phone-number-privacy-usernames/>

Aussagen mit [**Empfehlung**](#tag-advice) sind die Einschätzung dieses Leitfadens, keine offiziellen Positionen. Bei [**Prüfen**](#tag-verify): *Mit der aktuellen offiziellen Dokumentation abgleichen.*

---

## 14. Verbesserungen gegenüber dem bisherigen Leitfaden

Die vorherige Version dieses Leitfadens wurde geprüft. Beibehalten: Betonung des gesperrten Bootloaders, Auto-Reboot, USB-C-Einstellung, Netzwerk-/Sensoren-Berechtigung, Profiltrennung, „ein VPN ist keine Anonymität“. Korrigiert:

| Bisherige Aussage | Problem | Ersetzt durch |
|---|---|---|
| Private DNS `dns.quad9.net` / Mullvad-DNS empfohlen, auch mit Mullvad-VPN | Offizielle Empfehlung: bei VPN Private DNS auf Aus stellen; Private DNS ist global und kollidiert mit profilbezogenem VPN | Abschnitt 5 DNS: standardmäßig Automatisch, eigener Server nur ohne VPN; begrenzte Wirkung |
| „18 Stunden sind ein guter Startwert“ beim Auto-Reboot | 18 h ist der Standard; Bereich 10 Min. bis 72 h | Als Standard mit Abwägungen genannt |
| „Google Services Framework, Google Play-Dienste und Google Play Store“ installieren | Laut aktueller offizieller Anleitung installiert Google Play services den Google Play Store mit; GSF stammt nur aus älteren Installationen und soll dort nicht entfernt werden | Abschnitt 8 |
| Profil „Anonym“ | Irreführend: ein Profil erzeugt keine Anonymität | Profil „Sensible Identität“, Korrelationswarnungen |
| Wasted, Sentry, LockUp mit Vorbehalten empfohlen | Drittanbieter-Werkzeuge mit hohen Rechten; keine GrapheneOS-Funktionen; Fernlöschen hängt von Konnektivität ab | Aus den Empfehlungen entfernt |
| Tor-Hinweise und Orbot-Aussagen | Nicht verifizierte Details | Auf vorsichtige Aussagen gekürzt; die Orbot-Einschätzung bleibt ausschließlich als datierte Beobachtung aus dem Issue-Tracker von 2020 erhalten (<https://github.com/GrapheneOS/os-issue-tracker/issues/95#issuecomment-558702217>); die Haltung von GrapheneOS zu Tor VPN bleibt im [Cryptophone-Leitfaden](cryptophone-guide-de.md#verify-tor-vpn) unbestätigt |
| „OEM-Entsperrung/Entwickleroptionen danach deaktivieren“ | Offizieller Ablauf: Schalter auf dem letzten Einrichtungsbildschirm, standardmäßig an | Abschnitt 3.3 |
| Quellen: AnarSec, Civic Security, PrivacyGear, Privacy Guides | Sekundäre/Drittquellen für Sicherheitsaussagen | Durch offizielle Dokumentation ersetzt |
| Fest verdrahtete Menüpfade | Pfade variieren je nach Version | Pfade mit [**Prüfen**](#tag-verify), wo unsicher |

Entfernt: nicht verifizierte Details und Werkzeugempfehlungen. Hinzugefügt: Bedrohungsmodelle, Geräteliste, CLI-Methode, Verifikationsschritte, Checklisten, Tabellen.

---

## 15. Änderungsprotokoll

- **Beibehalten:** Grundprinzip (gesperrter Bootloader, starker Sperrcode, Updates), Auto-Reboot- und USB-C-Hinweise, Netzwerk-/Sensoren-/Speicher-Berechtigungen, Profiltrennung, Mullvad-Kill-Switch-Idee, Duress-Warnung, Backup-Hinweise, Abschluss-Checkliste.
- **Korrigiert:** DNS-Empfehlung, Installation der Google Play-Dienste, Formulierung „anonymes Profil“, Schritte zur OEM-Entsperrung, Qualität der Quellen.
- **Hinzugefügt:** Einführung und Bedrohungsmodelle, unterstützte Geräte, CLI-Installationsmethode, Überprüfung der Installation, Update-Kanäle, Bewertung von App-Quellen, App-Kategorientabelle, Abschnitt Sandboxed Google Play, OPSEC-Abschnitt, Reise-Checkliste, häufige Fehler, Referenztabellen.
- **Entfernt:** Empfehlungen zu Wasted/Sentry/LockUp, Blogs als Autorität, nicht überprüfbare Aussagen.
- **Prüfdurchgang:** Das Sperren des Bootloaders ist nun ausdrücklich an ein erfolgreiches, verifiziertes Flashen geknüpft, mit Ausweg bei fehlgeschlagener Verifizierung; Profilempfehlung für Play konsistent gemacht (separates Profil empfohlen); Formulierungen zu Signal, SIM/IMEI/eSIM, VPN sowie Tor/Proton präzisiert; Beschlagnahme- und Rechtsformulierungen nicht absolut und rechtsordnungsbewusst gefasst; Accrescent herabgestuft; unbestätigte Aussagen mit [Prüfen](#tag-verify) oder [Empfehlung](#tag-advice) markiert; deutsche Grammatik und EN/DE-Parität korrigiert.
