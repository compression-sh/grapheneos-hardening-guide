# GrapheneOS-Cryptophone-Leitfaden (Deutsch)

> **Was das ist:** eine maximal gehärtete GrapheneOS-Konfiguration mit nur einem Zweck, für sensible Kommunikation und Recherche. Sie ist strenger und einfacher als der Alltags-Leitfaden ([daily-driver-guide-de.md](daily-driver-guide-de.md)), den sie nicht ersetzt.
>
> **Was das nicht ist:** ein Weg zu Anonymität oder Unknackbarkeit. Sie verringert Angriffsfläche, Metadaten-Exposition, Identitätsverknüpfung und die Folgen einer Kompromittierung. Sie überwindet weder eine kompromittierte Lieferkette, einen kompromittierten Computer, manipulierte Hardware, körperlichen Zwang, eine vertrauenswürdige, aber kompromittierte App, einen entschlossenen Gegner mit Gerätezugriff, Metadaten von Netzbetreibern und Netzen noch menschliche Fehler.
>
> **Stand:** erstellt am 05.11.2026. GrapheneOS-Aussagen wurden gegen die offiziellen GrapheneOS-Seiten geprüft (Install, Usage, Features, FAQ, Releases). Weitere Aussagen wurden gegen die genannten externen Primärquellen geprüft. Menünamen ändern sich zwischen Versionen.
>
> **Markierungen:** **[Offiziell]** = steht in der offiziellen GrapheneOS-Dokumentation. **[Extern]** = steht in einer genannten Primärquelle außerhalb von GrapheneOS (z. B. EFF, Tor Project, Signal, die Seite der jeweiligen App). **[Empfehlung]** = Einschätzung dieses Leitfadens. **[Prüfen]** = nicht bestätigt; *Mit der aktuellen offiziellen Dokumentation abgleichen.*.
>
> **Keine Rechtsberatung.** Alle Aussagen zu Durchsuchung, erzwungener Entsperrung oder Datenvernichtung sind allgemein gehalten und hängen von der Rechtsordnung ab. Hole lokalen Rechtsrat ein.

English version: [cryptophone-guide-en.md](cryptophone-guide-en.md)

## Inhaltsverzeichnis

- [1. Zweck und Bedrohungsmodell](#1-zweck-und-bedrohungsmodell)
- [2. Strikte Geräterichtlinie](#2-strikte-geräterichtlinie)
- [3. Geräteeinrichtung](#3-geräteeinrichtung)
- [4. Härtungseinstellungen](#4-härtungseinstellungen)
- [5. Profile und Kompartimente](#5-profile-und-kompartimente)
- [6. Sandboxed Google Play](#6-sandboxed-google-play)
- [7. Apps](#7-apps)
- [8. Kommunikations-OPSEC](#8-kommunikations-opsec)
- [9. Netzwerk-OPSEC](#9-netzwerk-opsec)
- [Behavioral OPSEC / Verhaltens-OPSEC](#behavioral-opsec--verhaltens-opsec)
- [10. Reisen und physische Sicherheit](#10-reisen-und-physische-sicherheit)
- [11. Reaktion auf Vorfälle](#11-reaktion-auf-vorfälle)
- [12. Useful websites / Nützliche Webseiten](#useful-websites--nützliche-webseiten)
- [13. Checklisten](#13-checklisten)
- [14. Anti-Muster](#14-anti-muster)
- [15. Unverzichtbar vs. optional, und Prüfstatus](#15-unverzichtbar-vs-optional-und-prüfstatus)

---

## 1. Zweck und Bedrohungsmodell

### Wofür das Gerät da ist

- Sensible Nachrichten
- Sensibles Surfen
- Sichere Notizen und 2FA
- Eine getrennte, kompartimentierte Identität oder Rolle
- Reisen oder Umgebungen mit höherem Risiko

### Wofür es nicht da ist

- Alltägliche soziale Medien
- Zufälliges Ausprobieren von Apps
- Private Fotos
- Online-Banking und Einkaufen
- Alltag mit vielen Kontakten
- Anmeldungen in alten privaten Konten

Gehört eine Tätigkeit auf diese Liste, erledige sie auf einem anderen Gerät. Eine Vermischung der Rollen zerstört den größten Teil des Nutzens.

### Vier Begriffe, sauber getrennt

| Begriff | Frage | Beispielmaßnahme | Gibt dir nicht |
|---|---|---|---|
| **Sicherheit** | Kann das Gerät oder können Apps kompromittiert werden? | Updates, gesperrter Bootloader, starke Passphrase, wenige Apps | Datenschutz gegenüber genutzten Diensten |
| **Datenschutz** | Wer sammelt welche Daten über mich? | Berechtigungskontrolle, kein Google-Konto, minimale Telemetrie | Anonymität |
| **Anonymität** | Lassen sich Handlungen mir zuordnen? | Getrennte Identitäten, sorgfältiges Netzverhalten | Irgendetwas, wenn ein einziges verknüpfbares Detail durchsickert |
| **Kompartimentierung** | Wie viel folgt, wenn eine Identität auffliegt? | Getrennte Profile, Konten, SIM, idealerweise getrennte Geräte | Schutz vor einem kompromittierten Gerät |

### Bedrohungsmodell dieses Leitfadens

Betrachtete Gegner: Gelegenheitsdiebe, Schadsoftware und bösartige Apps, Netzbeobachter (WLAN-Betreiber, Internetanbieter, VPN-Anbieter), Netzbetreiber, Diensteanbieter und ein Gegner, der das ausgeschaltete oder gesperrte Gerät in die Hände bekommt. Ein gut ausgestatteter, gezielter Angreifer wird nur **teilweise** berücksichtigt: Der Leitfaden erhöht dessen Aufwand, behauptet aber nicht, ihn aufzuhalten.

### Was nicht überwunden wird

| Nicht überwunden | Warum |
|---|---|
| Kompromittierte Lieferkette oder manipulierte Hardware | Hardware lässt sich über die Attestierung hinaus nicht prüfen; Auditor prüft Hardware, Firmware und Betriebssystem, aber nicht jede App **[Offiziell]** |
| Kompromittierter Computer zum Installieren oder Sichern | Ein Angreifer, der über einen kompromittierten Flash-Computer ein bösartiges Betriebssystem aufgespielt hat, lässt sich danach durch Verified Boot und Attestierung erkennen **[Offiziell]**, sofern du den angezeigten Schlüssel-Hash auf einem getrennten, vertrauenswürdigen Gerät mit der offiziellen Liste vergleichst und Auditor von einem anderen Gerät aus gekoppelt hast; die Installationsseite auf einem kompromittierten Computer kann beliebige Inhalte zeigen. **[Empfehlung]** Ein kompromittierter Computer, den du auch für sensible Arbeit nutzt, ist ein eigenes Problem |
| Körperlicher Zwang | Keine Softwareeinstellung ändert das |
| Schadsoftware über eine vertrauenswürdige, aber kompromittierte App | Die App-Sandbox begrenzt den Schaden, beseitigt aber nicht das Vertrauen in eine selbst gewählte App |
| Entschlossener Gegner mit Gerätezugriff | Erhöht den Aufwand, garantiert keinen Schutz, besonders im entsperrten Zustand oder nach dem ersten Entsperren |
| Metadaten von Netzbetreiber und Netz | Der Netzbetreiber sieht SIM, IMEI, Funkzellen und Zeitpunkte, egal was das Betriebssystem tut |
| Menschliche Fehler | Der häufigste Ausfall |

**Verbleibendes Risiko dieses Abschnitts:** Das Bedrohungsmodell selbst kann falsch sein. Prüfe es neu, sobald sich deine Rolle oder dein Aufenthaltsort ändert. Siehe das EFF-Modul „Your Security Plan“ (unter Nützliche Webseiten aufgeführt).

---

## 2. Strikte Geräterichtlinie

Das sind Regeln, keine Vorschläge. Jede Regel hat einen Grund; wenn du eine nicht einhalten kannst, wisse, worauf du verzichtest.

1. **Ein Zweck.** Das Gerät dient sensibler Kommunikation und Recherche, sonst nichts.
2. **Keine App ohne dokumentierten Grund.** Führe eine kurze Liste: App, Quelle, Zweck, gewährte Berechtigungen, Datum. Entferne Apps, die du nicht mehr brauchst.
3. **Kein wiederverwendetes Identitätsmaterial.** Verwende keine privaten Konten, Benutzernamen, E-Mail-Adressen, Rufnummern, Profilbilder oder Wiederherstellungskontakte erneut.
4. **Keine Kontakte mit echtem Namen**, außer sie sind operativ nötig, und dann nur der betreffende Kontakt (Contact Scopes, Abschnitt 4).
5. **Eigene SIM/eSIM.** Nutze nicht die SIM oder eSIM deines normalen Telefons, außer dein Bedrohungsmodell nimmt die Verknüpfung ausdrücklich in Kauf. Stecke keine SIM zwischen diesem und einem anderen Gerät um: Netzbetreiber können IMSI/IMEI-Paare protokollieren, sodass eine neue SIM im selben Telefon oder eine alte SIM in einem neuen Telefon Identitäten verknüpfen kann (siehe 9.1). Vermeide außerdem, dieses Gerät zusammen mit deinem privaten Telefon mitzuführen oder einzuschalten (gleiche Zeiten, gleiche Orte), SIM und Gerät gemeinsam oder mit rückverfolgbarer Zahlung zu kaufen und mit einem verknüpften Zahlungsmittel aufzuladen. Regeln zur SIM-Registrierung und Ausweispflicht sind länderspezifisch. Setze eine SIM-PIN. **[Empfehlung]** **[Prüfen]** Die Regeln deines Landes.
6. **Keine privaten Zahlungsmittel** für alles, was zu dieser Identität gehört.
7. **Keine Biometrie**, wenn dein Bedrohungsmodell Zwang, Beschlagnahme oder erzwungenes Entsperren einschließt. Die EFF weist darauf hin, dass im von ihr beschriebenen Protestkontext weniger Schutz gegen erzwungenes Entsperren per Gesicht oder Fingerabdruck besteht als gegen erzwungene Herausgabe eines Passworts. **[Extern]** Ob und wo beides erzwungen werden kann, hängt von der Rechtsordnung ab; hole Rechtsrat ein. **[Prüfen]**
8. **Starkes Geheimnis.** Nutze eine lange zufällige alphanumerische Passphrase oder eine lange zufällige PIN. Abwägung: Das Secure Element begrenzt Versuche auf insgesamt 20 mit steigenden Wartezeiten, was laut Projekt selbst bei einer zufälligen 6-stelligen PIN ein hohes Schutzniveau bietet. **[Offiziell]** Eine längere Passphrase (bis 128 Zeichen; Diceware wird unterstützt **[Offiziell]**) bleibt selbst gegen einen Angreifer stark, der die Versuchsbegrenzung des Secure Elements umgeht, kostet aber Tippaufwand und erhöht die Gefahr des Mitlesens. **[Empfehlung]** **Empfohlen:** eine Diceware-Passphrase oder eine zufällige PIN mit 8 oder mehr Ziffern, wenn eine Passphrase unpraktikabel ist. **[Empfehlung]**
9. **Auto-Reboot an** (Abschnitt 4).
10. **USB-C-Port eingeschränkt** (Abschnitt 4).
11. **Funkmodule standardmäßig aus:** Bluetooth, WLAN, NFC und Standort aus, solange sie nicht gebraucht werden.
12. **Updates sofort.**
13. **Backups minimal, verschlüsselt, offline** (Abschnitt 4).
14. **Nichts auf dem Gerät, das du dir nicht leisten kannst zu verlieren oder gelesen zu wissen.**

**Verbleibendes Risiko:** Die Richtlinie wirkt nur, wenn sie täglich befolgt wird. Eine einzige Wiederverwendung eines alten Benutzernamens oder einer Rufnummer kann Monate der Trennung zunichtemachen.

---

## 3. Geräteeinrichtung

### 3.1 Regeln für Hardware und Software

- **Nur unterstützte Pixel-Geräte**, am besten ein empfohlenes Modell der 8. Generation oder neuer, das mindestens 7 Jahre Support und Hardware Memory Tagging bietet. **[Offiziell]** Prüfe vor dem Kauf <https://grapheneos.org/faq#supported-devices>. Pixel-Varianten von Netzbetreibern erlauben das Entsperren des Bootloaders womöglich nicht; kaufe ein freies Gerät aus dem Handel. Das Aktivieren der OEM-Entsperrung kann bei manchen Varianten Internetzugang erfordern. **[Offiziell]**
- **Nur offizielles GrapheneOS**, installiert mit dem offiziellen **Web-Installer** (<https://grapheneos.org/install/web>) oder der **CLI-Anleitung** (<https://grapheneos.org/install/cli>). Folge der gewählten Anleitung buchstabengetreu, ohne Schritte auszulassen, umzuordnen oder hinzuzufügen. **[Offiziell]**
- **Verboten:** Drittanbieter-Recovery, Custom-ROMs, Root, Magisk, Xposed, LSPosed, inoffizielle APK-Stores, veränderte Systemkomponenten, „Privacy-ROMs“ und Verschleierungswerkzeuge. Sie schwächen oder entfernen Verified Boot und die Sandbox. **[Empfehlung]**
- Kaufe und installiere das Gerät möglichst selbst. Das Projekt empfiehlt keine Firmen, die vorinstallierte Geräte verkaufen. **[Offiziell]** Kauftricks machen das Gerät nicht anonym; Händler können Videoaufnahmen, IMEI-Daten und Zahlungsdaten speichern. **[Empfehlung]**

### 3.2 Ablauf der Installation

> ⚠️ **Das Entsperren und das Sperren des Bootloaders löschen jeweils alle Daten.** Sichere vorher alles, was auf dem Gerät liegt; ein gebrauchtes Gerät wird gelöscht, die Installation löscht es.

1. Starte das Stock-Android, aktualisiere es, aktiviere die Entwickleroptionen (**Einstellungen → Über das Telefon → Build-Nummer**) und aktiviere unter **Einstellungen → System → Entwickleroptionen** die **OEM-Entsperrung**. Beim Pixel 6a zuerst per OTA auf Juni 2022 oder neuer aktualisieren und auf Werkseinstellungen zurücksetzen. **[Offiziell]**
2. Starte in das Bootloader-Interface: Halte beim Start die **Leiser-Taste** gedrückt, bis das rote Dreieck und „Fastboot Mode“ erscheinen. Wähle „Start“ nicht aus. **[Offiziell]**
3. **Entsperre** den Bootloader (Schaltfläche im Web-Installer oder `fastboot flashing unlock`) und bestätige am Gerät. Das löscht das Gerät. **[Offiziell]**
4. **Flashen** (Web-Installer **Flash release**, oder CLI: Image-Signatur mit `ssh-keygen -Y verify` anhand von `allowed_signers` prüfen, entpacken, `flash-all` ausführen). Bediene das Gerät nicht, bis es fertig ist. **[Offiziell]**
5. **Sperre den Bootloader erst, nachdem der offizielle Installer/Flasher erfolgreiches Flashen gemeldet hat (bei der CLI zusätzlich nach der Signaturprüfung in Schritt 4).** Sperre ihn dann (Schaltfläche im Web-Installer oder `fastboot flashing lock`) und bestätige am Gerät. **Das Sperren löscht erneut alle Daten.** **[Offiziell]**

> ⚠️ **Schlagen Verifizierung oder Flashen fehl oder sind sie unvollständig, sperre den Bootloader nicht.** Lass ihn entsperrt und flashe erneut; das Gerät startet womöglich nicht, bis ein verifiziertes GrapheneOS-Image erfolgreich geflasht wurde. Ein Sperren mit fehlendem, unvollständigem oder ungültigem Betriebssystem kann das Gerät unwiederbringlich machen, weil die OEM-Entsperrung nur aus einem startenden Betriebssystem wieder aktiviert werden kann. Lade das Image erneut herunter, verifiziere es erneut, wiederhole die Installation oder frage in den offiziellen GrapheneOS-Supportkanälen nach. **[Empfehlung]**

6. Lass bei der Ersteinrichtung den Schalter **OEM-Entsperrung deaktivieren** auf dem letzten Bildschirm **angehakt** (Standard). **[Offiziell]**
7. **Installation überprüfen.** Erwarte den gelben Startbildschirm-Hinweis; vergleiche den angezeigten Verified-Boot-Schlüssel-Hash mit der Liste auf der Installationsseite. Bei der Einrichtung darf keine Warnung „Bootloader nicht gesperrt“ erscheinen. Erscheint sie, ist die Installation unvollständig; sperre jetzt nur, wenn das ursprüngliche Flashen und Verifizieren erfolgreich abgeschlossen wurde, andernfalls nicht sperren und erneut flashen (siehe die Warnung oben). **[Offiziell]** Vergleiche zuerst den Schlüssel-Hash (auf einem getrennten, vertrauenswürdigen Gerät mit der offiziellen Liste), koppele dann **Auditor** von einem zweiten Android-Gerät aus und nutze erst danach das Gerät. Der Vergleich erfolgt nach dem Sperren und ist die abschließende Prüfung. Koppele Auditor unmittelbar nach der Installation, bevor das Gerät deine Kontrolle verlässt; die Attestierung ist nur aussagekräftig, wenn die Kopplung vorher stattfand. **[Offiziell]** für das Kopplungsmodell; die Reihenfolge ist eine **[Empfehlung]**.
8. **Sofort aktualisieren** und beim Stable-Kanal bleiben. **[Offiziell]**
9. USB-Debugging und drahtloses Debugging ausschalten. **[Empfehlung]**

**Verbleibendes Risiko:** Die Installationsseite und dein Computer sind Komponenten, denen du vertrauen musst. Die CLI-Methode mit Signaturprüfung verringert das Vertrauen in die Web-Infrastruktur des Projekts, nicht aber in deinen Computer oder die Hardware. Nutze einen Computer, dem du vertraust und den du nicht für die sensible Arbeit selbst verwendest.

---

## 4. Härtungseinstellungen

Die Menünamen folgen der aktuellen offiziellen Dokumentation und ändern sich zwischen Versionen. **[Prüfen]** bei jedem so markierten Pfad.

Für jede Einstellung: der empfohlene Cryptophone-Wert, warum, wogegen sie schützt, wogegen sie **nicht** schützt, und die Komforteinbuße.

### 4.1 Gerätezugang

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Bildschirmsperre** (Einstellungen → Sicherheit & Datenschutz → Gerät entsperren) **[Offiziell]** | Lange zufällige Passphrase (Diceware) oder zufällige PIN mit 8+ Ziffern; keine Biometrie | Starker praktischer Schutz gegen Raten; beseitigt den Angriffsweg erzwungener Biometrie | Raten, auch forensisch; Mitlesen mit Scrambling | Zwang, ein in deiner Hand entsperrtes Gerät, Schadsoftware im entsperrten Zustand | Hoch: häufiges Eintippen des Geheimnisses |
| **Sperrzeit** | Kurz, z. B. 30-60 s bei einer Passphrase oder 15-30 s bei einer kurzen PIN; wähle eine, die du durchhältst. Sofort sperren per Ein-/Aus-Taste | Verkürzt das entsperrte Zeitfenster | Gelegenheitszugriff auf ein unbeaufsichtigtes Telefon | Ein Angreifer, der es im entsperrten Zustand greift | Häufiges Neu-Entsperren; eine so kurze Zeit, dass du dein Geheimnis schwächst, ist kontraproduktiv |
| **PIN-Scrambling** | An, wenn du eine PIN nutzt | Erschwert das Beobachten der PIN; gilt für Sperrbildschirm und SIM-PIN **[Offiziell]** | Mitlesen, Fingerspuren | Kameras, die das Drücken auf der durchmischten Tastatur sehen | Langsamere Eingabe |
| **Biometrie** | Aus | Siehe Richtlinie Regel 7 | Erzwungene Entsperrung per Fingerabdruck oder Gesicht | Erzwungene Herausgabe der Passphrase (rechtsordnungsabhängig) | Weniger Komfort |
| **Lockdown** (Ein-/Aus-Menü) | Kennen: Halte die Ein-/Aus-Taste gedrückt und tippe dann auf Lockdown (erscheint kein Menü, prüfe Einstellungen → System → Gesten → Ein-/Aus-Taste gedrückt halten). Es deaktiviert Biometrie vorübergehend, verlangt die PIN oder das Passwort und blendet Benachrichtigungen auf dem Sperrbildschirm aus (privacygear.nl, eine Sekundärquelle; die eigenen Seiten von GrapheneOS beschreiben es nicht) **[Extern]**. Bei ausgeschalteter Biometrie bringt es wenig, und verlasse dich nicht darauf, dass es das Telefon in den Ruhezustand (BFU) zurückversetzt; die Handlung vor Kontrollen ist das Ausschalten **[Empfehlung]** | Schaltet biometrische und Smart-Entsperrung schnell ab | Kurzfristige biometrische Entsperrung | Alles andere | Ein zusätzlicher Schritt |
| **Auto-Reboot** (Exploit-Schutz) | 4 Stunden auf Reisen, 8-12 Stunden für ein täglich mitgeführtes Telefon **[Empfehlung]**; offizieller Standard ist 18 h, Bereich 10 Min. bis 72 h **[Offiziell]** | Bringt das ungenutzte Gerät in den verschlüsselten Ruhezustand (BFU, Before First Unlock; erklärt unter Verhaltens-OPSEC) zurück; gilt nicht, solange es schon in BFU ist | Forensische Extraktion eines Geräts im Zustand nach dem ersten Entsperren | Beschlagnahme während der Nutzung, ein schwaches Geheimnis oder ein kompromittiertes Secure Element | Nach jedem Neustart muss zuerst das Owner-Profil, dann das Kommunikationsprofil entsperrt werden; bis dahin kommen keine Nachrichten oder Benachrichtigungen an. Wähle ein Intervall, das du durchhältst |
| **USB-C-Port** (Exploit-Schutz **[Offiziell]**; die Usage-Seite schreibt für das übergeordnete Menü auch „Security & privacy“) | Mindestens „Nur Laden, wenn gesperrt“ (Standard); „Nur Laden“ oder strenger, wenn du nie USB-Daten nutzt **[Offiziell]** | Blockiert neue USB-Verbindungen nach dem Sperren | USB-Angriffe auf ein gesperrtes Telefon | Angriffe im entsperrten Zustand oder über andere Funkwege | Keine Dateiübertragung im gesperrten Zustand |
| **Memory Tagging (MTE)** (Exploit-Schutz; Pixel 8 und neuer) | Für alle Apps aktivieren (Einstellungen → Sicherheit & Datenschutz → Exploit-Schutz → Memory tagging → Enable by default, laut privacygear.nl **[Extern]**); pro App nur deaktivieren, wenn eine App abstürzt | GrapheneOS nutzt Hardware-Memory-Tagging bereits für das Basissystem und bekannte kompatible Apps und bietet die Option, es für alle Apps zu verwenden **[Offiziell]** | Ausnutzung von Speicherfehlern in Apps (Pufferüberläufe, Use-after-free) | Logikfehler, ein kompromittiertes System oder Hardware und alles, was kein Speicherfehler ist | Schlecht programmierte Apps können abstürzen |
| **Duress-PIN/-Passwort** (Gerät entsperren, Owner-Profil) **[Offiziell]** | Optional; bewusst entscheiden (Abschnitt 10). Erfordert PIN und Passwort; die Eingabe der echten Zugangsdaten hat Vorrang, dann erfolgt kein Löschen **[Offiziell]** | Löscht Gerät und eSIMs unwiderruflich bei Eingabe; keine allgemeine Schutzmaßnahme gegen Beschlagnahme | Einen Gegner, der Zugangsdaten in das laufende Gerät eingibt | Extraktion ohne Eingabe der Zugangsdaten, ein bereits abgebildetes Gerät oder rechtliche Folgen | Risiko eines versehentlichen, unumkehrbaren Löschens |

### 4.2 Funkmodule, Standort und Sensoren

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Bluetooth** | Aus; nur für ein bestimmtes Zubehör einschalten; die Zeitüberschreitung „Turn off Bluetooth automatically“ nutzen (Bezeichnung aus dem Settings-Quelltext von GrapheneOS) **[Offiziell]**; **[Prüfen]** Menüort | Verringert Angriffsfläche in der Nähe und Tracking über Geräte in der Umgebung | Angriffe aus der Nähe, passives Tracking durch Bluetooth-Beacons | Einen Beacon, der ein Gerät sieht, bei dem Bluetooth an blieb | Standardmäßig kein drahtloses Zubehör |
| **WLAN** | Aus, solange nicht genutzt; MAC-Randomisierung pro Verbindung bleibt an (Standard) **[Offiziell]**; keine versteckten Netzwerke verbinden, sie verringern die Privatsphäre **[Offiziell]** | Begrenzt passives Tracking und Gefahr durch Fremd-Hotspots | Passives Tracking per MAC, Fremd-Hotspots | Den WLAN-Betreiber, der Verkehr und IP sieht | Manuelles Umschalten |
| **WLAN- und Bluetooth-Scanning** (Einstellungen → Standort → Standortdienste) **[Offiziell]** | Aus (Standard) | Scanning läuft auch bei „ausgeschalteten“ Funkmodulen | Funkmodule, die im Hintergrund aktiv bleiben | n/a | Langsamere Ortung |
| **Standort** | Standardmäßig aus; „nur bei Nutzung“ für einen konkreten Bedarf | Verringert die Standortspur | Apps und SDKs, die Standort sammeln | Netz-Standort durch den Netzbetreiber | Karten brauchen manuelles Einschalten |
| **NFC** | Aus (Einstellungen → Verbundene Geräte → Verbindungseinstellungen → NFC, laut privacygear.nl **[Extern]**) | Entfernt einen Eingang aus der Nähe | Angriffe aus der Nähe | n/a | Kein kontaktloses Bezahlen (hier ohnehin unerwünscht) |
| **Mobilfunk-Typ** (Einstellungen → Netzwerk & Internet → SIMs → SIM → Bevorzugter Netzwerktyp) **[Offiziell]** | Nur LTE, wenn dein Netzbetreiber damit zuverlässig funktioniert | Schaltet 2G-, 3G- und 5G-Codepfade ab und verringert die Angriffsfläche für Remote-Exploits **[Offiziell]** | Remote-Ausnutzung über alten Funkmodul-Code | Abhören von Anrufen und SMS, Metadaten des Netzbetreibers, Ortung durch den Netzbetreiber. Laut Projekt keine Vertraulichkeitsfunktion **[Offiziell]** | Kein Rückfall bei schlechter Abdeckung; herkömmliche Sprachanrufe funktionieren nur mit VoLTE oder WLAN-Telefonie **[Offiziell]** |
| **SUPL** (Einstellungen → Standort) **[Offiziell]** | GrapheneOS-Proxy beibehalten oder Aus | Vermeidet den Standard-SUPL-Server des Netzbetreibers | Preisgabe eines groben Standorts an den SUPL-Server des Netzbetreibers | Funkzellen-Ortung durch den Netzbetreiber | Langsamerer GNSS-Fix bei Aus |
| **eSIM-Unterstützung** (Einstellungen → Netzwerk & Internet) **[Offiziell]** | Aus, solange du keine eSIM nutzt | Standardmäßig deaktiviert; die Verwaltung von eSIMs braucht proprietäre Google-Funktionen, aber nicht Google Play | n/a | Eine eSIM hat eine eigene Kennung, und die Aktivierung kann ein Konto oder einen Ausweis verlangen | Zusätzlicher Schritt zum Einschalten bei Bedarf |
| **Kamera und Mikrofon** | Standardmäßig verweigern; pro Nutzung gewähren („nur diesmal“ / „bei Nutzung“) | Begrenzt Missbrauch von Kamera und Mikrofon | Heimliche Aufnahme durch Apps | Ein kompromittiertes Betriebssystem oder Hardware | Rückfrage jedes Mal |
| **Sensoren-Berechtigung** (Einstellungen → Sicherheit & Datenschutz → Weitere Sicherheit & Datenschutz) **[Offiziell]** | Für neu installierte Apps standardmäßig deaktivieren | Liefert Nullwerte für Beschleunigungssensor, Gyroskop, Kompass und weitere | Sensorbasiertes Fingerprinting und Seitenkanäle | Andere verdeckte Kanäle | Einzelne Apps verhalten sich womöglich merkwürdig |

### 4.3 Berechtigungen und Daten

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **App-Berechtigungen** | Das Minimum gewähren; nach jeder Installation prüfen | Kleinerer Schadensradius | Übermäßiges Sammeln durch Apps | Eine vertrauenswürdige App, die gewährte Daten missbraucht | Gelegentliche Fehlfunktionen |
| **Netzwerk-Berechtigung** **[Offiziell]** | Für jede App blockieren, die offline funktioniert (Notizen, PDF, Authenticator, Passwortmanager) | Die App sieht „Netz aus“; blockiert auch Localhost-Nutzung zwischen Profilen | Telemetrie und Datenabfluss offline arbeitender Werkzeuge | Daten, die über einen anderen erlaubten Weg abfließen | Synchronisierende Apps synchronisieren nicht mehr |
| **Contact Scopes** **[Offiziell]** | Für jede App an, die Kontakte verlangt; nur den einen Kontakt, die Gruppe oder die nötigen Daten freigeben; Schreibzugriff ist blockiert | Die App sieht standardmäßig eine leere Kontaktliste | Hochladen des gesamten Adressbuchs | Einen Kontakt, den du freigegeben hast | Manuelles Freigeben |
| **Storage Scopes** **[Offiziell]** | Für jede App an, die Speicherzugriff verlangt; nur nötige Dateien oder Ordner freigeben | Begrenzt die Dateiexposition | Durchsuchen des gesamten Speichers | Dateien, die du freigegeben hast | Manuelles Freigeben |
| **Zwischenablage** | Als für die Vordergrund-App und die Tastatur lesbar betrachten; Geheimnisse möglichst nicht kopieren; wo möglich die Autofill-Funktion des Passwortmanagers nutzen. Das Sperren der Zwischenablage zum/vom übergeordneten Profil gibt es für den Private Space in neueren Versionen (Release-Notes 05/2025; Einstellung „Cross-profile shared clipboard“ mit der Option „Disallowed“ im Settings-Quelltext von GrapheneOS) **[Offiziell]**, der Private Space ist aber nicht Teil des Profilmodells dieses Leitfadens; **[Prüfen]** genauer Menüpfad | Apps im Vordergrund können die Zwischenablage lesen | Preisgabe von Geheimnissen über die Zwischenablage | Keylogger oder eine kompromittierte Tastatur | Neu tippen |
| **Benachrichtigungen** | Sensible Inhalte auf dem Sperrbildschirm ausblenden; keine Nachrichtenvorschau | Ein gesperrtes Telefon soll nichts verraten | Mitlesen, Blick auf ein gesperrtes Telefon | Benachrichtigungen, die Text anzeigen dürfen | Weniger auf einen Blick |
| **Screenshots** | Nie für sensibles Material; Screenshots werden gespeichert und womöglich gesichert | Screenshots bleiben bestehen und wandern weiter | Lokale Rückstände | Einen Empfänger, der seinen eigenen Bildschirm fotografiert | Gewohnheitsänderung |

### 4.4 Browser, DNS, VPN, Updates, Backups, Verlust

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Browser** | **Vanadium** im isolierten Browsing-Profil. JavaScript-JIT ist standardmäßig aus, mit Umschalter pro Website; Erweiterungen sind bewusst nicht geplant **[Offiziell]**. So lassen. **[Empfehlung]** | Laut Projekt die stärkste Sandbox unter gängigen mobilen Browsern **[Offiziell]**; weniger Plugins bedeuten weniger Fingerprinting | Viele Browser-Exploits, erweiterungsbasiertes Tracking | IP-basiertes Tracking, Anmeldung in Konten, Fingerprinting durch Websites | Manche Seiten gehen mit JIT aus kaputt |
| **Private DNS** (Einstellungen → Netzwerk & Internet → Private DNS) | **Automatisch** (Standard), wenn kein VPN genutzt wird; **Aus, wenn ein VPN aktiv ist** **[Offiziell]** | Automatisch liefert opportunistisches DNS-over-TLS; ein Hostname erzwingt authentifiziertes DoT. Private DNS ist global, VPN-Einstellungen aber gelten pro Profil, daher wirken beide schlecht zusammen; die Version 07/2025 behob zwei VPN-Lecks **[Offiziell]** | Einen passiven lokalen Mithörer (Automatik-Modus); aktive Angreifer können den Rückfall erzwingen **[Offiziell]** | Domains, die über TLS-SNI durchsickern, Ziel-IPs, den DNS-Anbieter, der deine Anfragen sieht. Kein Ersatz für Tor oder ein VPN **[Offiziell]** | Keine im Automatik-Modus |
| **VPN** | Nur nutzen, wenn du die adressierte Bedrohung benennen kannst (nicht vertrauenswürdiges lokales Netz oder Provider). Nutze die offizielle Mullvad- oder WireGuard-App, wie es die GrapheneOS-FAQ empfiehlt **[Offiziell]**. **Always-on-VPN** und **Verbindungen ohne VPN blockieren** aktivieren | Verbirgt Ziele und Inhalte vor lokalem Netz und Provider; verbirgt deine IP vor Websites | Einen feindlichen WLAN-Betreiber oder Provider | Den VPN-Anbieter, der den Verkehr sieht (Vertrauen verschiebt sich), Konten, in die du dich einloggst, Funkzellen-Ortung, Anrufe und SMS. EFF: „A VPN is not a tool for anonymity“ **[Extern]** | Einrichtung und Konfiguration pro Profil |
| **Updates** | System-Updater an, **Stable**-Kanal, zum Abschluss neu starten **[Offiziell]** | Sicherheitskorrekturen gehören zu den wertvollsten Schutzmaßnahmen | Bekannte Schwachstellen | Unbekannte (Zero-Day-)Schwachstellen | Gelegentliche Neustarts |
| **Backups** | **Standardmäßig kein vollständiges Geräte-Backup.** Nur sichern: eine verschlüsselte Kopie der Passwortmanager-Datenbank, einen verschlüsselten Authenticator-Export und Wiederherstellungscodes offline, getrennt vom Gerät | Backups sind eine zusätzliche Kopie, die ein Gegner beschlagnahmen kann | Verlust des Geräts = Verlust des Zugangs | Ein kompromittiertes Sicherungsmedium | Neuaufbau nach Verlust |
| **Seedvault** (eingebautes Backup) | Für das sensible Profil nicht nutzen, sofern nicht nötig. Falls doch, ein lokal gespeichertes verschlüsseltes Ziel. Das Projekt plant einen Ersatz, weil Seedvault upstream von einer Gruppe übernommen wurde, die seine Ziele nicht teilt **[Offiziell]** | Vermeidet eine Cloud-Kopie | Cloud-Exposition von Gerätedaten | Ein beschlagnahmtes Backup-Laufwerk | n/a |
| **Geräteverlust/Diebstahl** | Gehe davon aus, dass es bei einem Gegner liegt, bis das Gegenteil bewiesen ist (Abschnitt 11). In den offiziellen Features-, Usage- und FAQ-Seiten ist keine Fernlösch-Funktion beschrieben **[Offiziell]**; Duress wirkt nur lokal | Auf den schlimmsten Fall planen | n/a | n/a | n/a |

**Verbleibende Risiken dieses Abschnitts:** Jede Einstellung ist eine Abmilderung, keine Garantie. Einstellungen, die auf dem Secure Element oder dem Betriebssystem selbst beruhen, versagen, wenn eines davon kompromittiert ist. Ein strenges Setup, das du aus Bequemlichkeit umgehst, ist schlechter als ein etwas lockereres, das du einhältst.

---

## 5. Profile und Kompartimente

### 5.1 Empfohlene minimale Struktur

| Profil | Inhalt | Regeln |
|---|---|---|
| **1. Owner** | Nur Systemverwaltung: Updates, App Store, Einstellungen | Keine sozialen Apps, keine privaten Konten, kein Surfen, wenn es nicht nötig ist. Das Owner-Profil speichert sensible systemweite Daten und muss nach einem Neustart zuerst entsperrt werden **[Offiziell]** |
| **2. Sichere Kommunikation** | Signal (oder ein anderer geeigneter Messenger), Authenticator, Passwortmanager, sichere Notizen, minimale Kontakte | Nur die Apps aus Abschnitt 7. Netzwerk für Offline-Apps blockiert |
| **3. Isoliertes Surfen (optional)** | Nur Browser | Keine dauerhaften Konten, keine Kontakte, keine persönlichen Dateien. Sitzung beenden, wenn du fertig bist |

### 5.2 Was Profile leisten und was nicht

- Profile trennen Apps, App-Daten, Schlüssel und die meisten Einstellungen. **Sitzung beenden** (Ein-/Aus-Menü oder Benutzerwechsel) entfernt die Schlüssel des Profils vollständig aus dem Speicher und versetzt es in den Ruhezustand. Für das Owner-Profil geht das nur per Neustart. **[Offiziell]**
- **Profile erzeugen keine Anonymität.** Alle Profile teilen Hardware, SIM, IMEI, IP-Adresse und deine Gewohnheiten. Eine wiederverwendete Rufnummer, E-Mail-Adresse, ein Name, Kontakt, eine Datei oder ein Schreibstil verknüpft Identitäten wieder. **[Empfehlung]**
- **WLAN und Bluetooth können Profile korrelieren.** Dieselben Funkmodule und dieselben Netze werden von allen Profilen genutzt.
- **Ein in einem Profil eingerichtetes VPN löst nicht automatisch jedes Netzwerk-Leck-Szenario.** Jedes Profil hat eine eigene VPN-Konfiguration, während Private DNS global ist. **[Offiziell]** Prüfe das Verhalten pro Profil (Checkliste in Abschnitt 13).
- **Verschiebe sensible Daten nicht beiläufig zwischen Profilen.** Meide geteilten Speicher, geteilte Zwischenablage und profilübergreifende Benachrichtigungen.
- **Jedes Profil hat eine eigene Sperrmethode; gib jedem Profil ein eigenes starkes Geheimnis.** Ein schwaches Geheimnis in einem Profil untergräbt dieses Kompartiment. Profile können unterschiedliche Entsperrmethoden haben **[Offiziell]**; die Empfehlung ist eine **[Empfehlung]**.
- GrapheneOS hebt das Limit auf 31 Zweitprofile plus Gast an, und Zweitprofile lassen sich so einstellen, dass sie nicht im Hintergrund laufen. **[Offiziell]** Nutze so wenige wie nötig.

### 5.3 Verbleibende Risiken

Profile sind Fächer für Daten, nicht für Identität. Für eine Rolle mit hohem Risiko sind **ein separates Gerät, eine separate SIM/eSIM und ein getrenntes Netzwerknutzungsmuster** die realistische Grenze. Profiltrennung allein ist Kompartimentierung, keine vollständige Grenze. **[Empfehlung]**

---

## 6. Sandboxed Google Play

- **Installiere Sandboxed Google Play auf einem Cryptophone nicht standardmäßig.**
- Installiere es **nur**, wenn eine bestimmte benötigte App anders nicht funktioniert und du die Google-Abhängigkeit akzeptierst.
- Falls installiert, **isoliere es in einem separaten Profil**, nie im Owner-Profil. Die offizielle Anleitung nennt die Installation im Owner-Profil „den einfachsten Weg“, aber sie ist weniger isoliert. **[Offiziell]** **[Empfehlung]**
- **Melde dich nie mit einem privaten Google-Konto an.** Ein Google-Konto verknüpft das Profil mit einer Identität bei Google. Die Anmeldung ist optional, außer du brauchst Installationen über den Play Store, In-App-Käufe oder kontoabhängige Funktionen. **[Offiziell]** Beim Anlegen eines Kontos wird häufig eine Telefonnummern-Verifizierung verlangt. **[Empfehlung]**
- Ein separates Profil begrenzt den Datenzugriff, verhindert aber nicht, dass Google das Konto über IP-Adresse, Geräteeigenschaften, Zeitpunkte oder Kontoaktivität korreliert. **[Empfehlung]**
- Wer **Google Play services** aus dem App Store installiert, installiert Google Play-Dienste und Google Play Store zusammen; beide laufen als normale Sandbox-Apps ohne Sonderrechte. **[Offiziell]**
- Bevorzuge Apps, die Google Play nicht benötigen.

**Verbleibendes Risiko:** Auch in einem separaten Profil sieht Google wahrscheinlich die über dieses Profil installierten Apps und die empfangenen Geräteinformationen. **[Empfehlung]**

---

## 7. Apps

### 7.1 Regeln

- Jede App braucht einen dokumentierten Zweck, eine Quelle und eine Berechtigungsliste.
- Bevorzuge quelloffene, aktiv gepflegte Apps.
- Installiere nur aus diesen Quellen, in dieser Rangfolge: dem **GrapheneOS App Store**; der **offiziellen, verifizierten Quelle des Entwicklers** (Signatur prüfen); **Accrescent** (im GrapheneOS App Store verfügbar; in der Alpha-Phase **[Extern]**); und **F-Droid** nur als Ausweichlösung für Apps, die es anderswo nicht gibt. Nutze weder den Aurora Store noch ein anderes Google-Play-Frontend.
- Prüfe Herausgeber und Signatur, wo möglich (z. B. einen veröffentlichten Fingerabdruck des Signaturzertifikats).
- Keine Beta-, modifizierten, gecrackten oder „Privacy-Fork“-Apps ohne triftigen Grund.
- Prüfe nach der Installation die Berechtigungen; entferne Apps, die du nicht mehr brauchst.

### 7.2 Hinweise zu den Quellen

| Quelle | Hinweis |
|---|---|
| **GrapheneOS App Store** | Verteilt eigene GrapheneOS-Apps und optional Sandboxed Google Play **[Offiziell]** |
| **Accrescent** | App Store mit Fokus auf Sicherheit und Datenschutz, derzeit in der Alpha-Phase **[Extern]**. Seine eigene Seite sagt, er lasse sich aus dem GrapheneOS App Store herunterladen, „der empfohlene Weg für GrapheneOS-Nutzer“ **[Extern]**. Er aktualisiert Apps automatisch, unbeaufsichtigt und ohne Sonderrechte ab Android 12 und braucht kein Konto **[Extern]**. Das GrapheneOS-App-Repository enthält ihn (Paket `app.accrescent.client`) **[Offiziell]** |
| **F-Droid** | Quelloffene Apps. Apps ohne Reproducible-Build-Einrichtung werden mit App-eigenen F-Droid-Schlüsseln signiert; bei vom Entwickler signierten, reproduzierbaren Apps veröffentlicht F-Droid eine Version nur, wenn sein Build mit dem des Entwicklers übereinstimmt **[Extern]** (F-Droid-Dokumentation). Updates können dem Entwickler hinterherhinken |
| **Offizielle Quelle des Entwicklers** | Prüfe den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal. Verfolge Updates selbst |

**Woher Signal kommt:** Signal wird über Google Play und als direkte APK unter signal.org/android/apk verteilt, die den Fingerabdruck des Signaturzertifikats veröffentlicht **[Extern]**; es ist nicht im Hauptrepository von F-Droid **[Extern]** und nicht im GrapheneOS-App-Repository **[Offiziell]**. Ob Accrescent es anbietet, ist **[Prüfen]** (Accrescent veröffentlicht keine App-Liste). Musst du eine APK von der Seite des Entwicklers installieren, prüfe das Signaturzertifikat, gib „Unbekannte Apps installieren“ nur einer App (dem genutzten Browser oder Dateimanager) und entziehe es danach wieder. Die manuelle APK-Installation erfordert für Updates ein erneutes Herunterladen und eine erneute Signaturprüfung; sie bietet keine automatischen Updates (signal.org/android/apk, die den SHA-256-Fingerabdruck und eine apksigner-Prüfung nennt) **[Extern]**. Erteile die Berechtigung für jedes neue Release erneut; sonst läuft das Gerät mit veralteter Software. Dasselbe gilt für jede App, die nicht in deinen gewählten Stores liegt. **[Empfehlung]**

> ⚠️ Lade niemals von zufälligen APK-Seiten. Root (Magisk), LSPosed und Xposed entfernen das Sicherheitsmodell.

### 7.3 Pflichtkategorien

| Kategorie | Wahl | Warum | Verbleibendes Risiko |
|---|---|---|---|
| **Browser** | **Vanadium** (eingebaut) | Gehärtetes Chromium, auch die System-WebView **[Offiziell]** | Verbirgt weder deine IP noch verhindert es von allein Fingerprinting |
| **Sicherer Messenger** | **Signal** | Ende-zu-Ende-verschlüsselt, geprüft, weit verbreitet. Die Registrierung erfordert eine Rufnummer; Benutzernamen können deine Nummer vor anderen Nutzern verbergen, heben die Pflicht aber nicht auf. **[Extern]** (EFF; Signal-Blogbeitrag zu Rufnummern-Datenschutz und Benutzernamen) | Die Registrierung per Rufnummer bindet das Konto an eine SIM; Metadaten bleiben sichtbar; das Gerät der Gegenseite kann den Chat kompromittieren |
| **Passwortmanager** | **KeePassDX** (GPL-3.0, lokale Datenbank) **[Extern]** | Kein Cloud-Konto nötig; lokale Datenbank | Eine gestohlene Datenbank mit schwachem Master-Geheimnis; nur die Android-App-Sandbox |
| **2FA/Authenticator** | **Aegis** (GPL-3.0) **[Extern]** | Quelloffen, verschlüsselter Tresor | Ein verlorener Tresor ohne Backup; ein kompromittiertes Telefon verrät Codes |
| **Sichere Notizen** | **Einträge in der KeePassDX-Datenbank** | Keine zusätzliche App und kein zusätzliches Konto | Dieselbe Einzelschwachstelle wie die Passwortdatenbank (ein einziger Ausfallpunkt) |
| **VPN-Client, nur wenn begründet** | Offizielle **Mullvad**-App oder die offizielle WireGuard-App **[Offiziell]** | Die zwei Apps, die die GrapheneOS-FAQ empfiehlt; Mullvads App ist quelloffen (GPL-3.0) **[Extern]** | Vertrauen verschiebt sich zum Anbieter; die Wahl hängt von Rechtsordnung, Logging, Zahlung und Bedrohungsmodell ab |
| **Dateiübertragung, nur wenn begründet** | Dateien bevorzugt über den Ende-zu-Ende-verschlüsselten Messenger senden. Keine zusätzliche App | Weniger Apps | Datei-Metadaten (EXIF, Dokumenteigenschaften) vorher entfernen |

### 7.4 Optionale Kategorien

| Kategorie | Wahl | Hinweise |
|---|---|---|
| **Verschlüsselte Cloud/Speicher** | **Cryptomator** **[Extern]** | Doppelt lizenziert (GPLv3 und kommerziell) **[Extern]**. Google Drive wird in den Varianten für den Google Play Store und den APK Store unterstützt, nicht aber in den F-Droid-Varianten (proprietäre Abhängigkeiten), und der Haupt-Build von F-Droid unterstützt außerdem keine Clouds, die einen API-Schlüssel brauchen **[Extern]**; ob der Accrescent-Build Google Drive unterstützt, ist **[Prüfen]** (die Cryptomator-Dokumentation sagt es nicht). Nur die APK-Store-Variante hat einen eingebauten automatischen Updater; die Varianten für Play Store, F-Droid und Accrescent haben keinen oder aktualisieren anders, über ihre Stores **[Extern]**. Alle Varianten sind kostenlos mit schreibgeschütztem Tresorzugriff; Schreiben erfordert einen kostenpflichtigen Lizenzschlüssel **[Extern]**. Verschlüsselung verbirgt nicht, dass du Cloud-Speicher nutzt |
| **Karten, nur bei Bedarf** | **Organic Maps** (Apache-2.0) **[Extern]** | Funktioniert offline. Laut README ist das Projekt weit von finanzieller Tragfähigkeit entfernt; prüfe den Pflegestatus, bevor du dich darauf verlässt |
| **PDF-/Dokumentleser, nur bei Bedarf** | Eingebauter **PDF-Betrachter** **[Offiziell]** | Netzwerk blockieren; Dokumente enthalten Metadaten |
| **Tor Browser, nur bei Bedarf** | **Tor Browser für Android** vom Tor Project **[Extern]** | Siehe Abschnitt 9; das GrapheneOS-Projekt sagt, seine Sicherheit sei im Vergleich zu Vanadium schwach und Tor mache Nutzer zu einem interessanteren Ziel **[Offiziell]** |

Ausdrücklich **nicht** empfohlen: weitere Messenger, weitere Browser, soziale Apps, cloudsynchronisierte Notiz-Apps, die ein Konto brauchen, und jede „Privacy“-App ohne dokumentierten Bedarf.

**Verbleibendes Risiko:** Jede App ist zusätzliches Vertrauen und zusätzliche Angriffsfläche. Die sicherste Liste ist die kürzeste.

### 7.5 App-Store-Vergleich

Jeder der folgenden Stores installiert Apps in die normale App-Sandbox. Die Unterschiede liegen darin, ob ein Konto nötig ist, wie Updates ankommen und wem du vertrauen musst. Aussagen zu Stores von Drittanbietern sind mit **[Extern]** markiert und stammen aus der jeweiligen Projektdokumentation; die Empfehlungen sind die Einschätzung dieses Leitfadens.

| Store | Konto nötig? | Google-Abhängigkeit | Update-Mechanismus | App-Auswahl (Umfang, Qualität) | Sicherheitsmodell | Empfehlung: Alltag / Cryptophone |
|---|---|---|---|---|---|---|
| **GrapheneOS App Store** | In der GrapheneOS-Dokumentation wird kein Konto als Voraussetzung genannt **[Offiziell]** | Keine für den Store selbst; er kann zusätzlich Sandboxed Google Play installieren, das optional ist **[Offiziell]** | Aktualisiert die Apps aus seinem Repository im Hintergrund, einschließlich der Komponenten von Sandboxed Google Play **[Offiziell]** | Klein: eigene GrapheneOS-Apps (zum Beispiel Kamera, PDF-Betrachter, Auditor, Vanadium), die Komponenten von Sandboxed Google Play und einige weitere wie der Accrescent-Client **[Offiziell]** | Erstanbieter-App-Repository und -Client des GrapheneOS-Projekts, in das Betriebssystem integriert **[Offiziell]** | Alltag: erste Wahl. Cryptophone: erste Wahl; Sandboxed Google Play nur installieren, wenn eine benötigte App sonst nicht funktioniert (Abschnitt 6) **[Empfehlung]** |
| **Accrescent** | Kein Konto nötig **[Extern]** | Vom Projekt keine genannt **[Extern]** | Automatische, unbeaufsichtigte Updates ohne Sonderrechte ab Android 12 **[Extern]** | Kleiner, kuratierter Katalog; das Projekt befindet sich in der Alpha-Phase **[Extern]** | Pinning des App-Signaturschlüssels bei der Erstinstallation, signierte Repository-Metadaten und kein Remote-APK-Signieren, sodass Entwickler ihre Signaturschlüssel behalten **[Extern]** | Alltag: für die Apps nutzen, die er führt. Cryptophone: ebenso. Den Client aus dem GrapheneOS App Store installieren, wie es die Seite von Accrescent für GrapheneOS-Nutzer empfiehlt **[Extern]**. In der Quellenreihenfolge von 7.1 steht er nur wegen der Alpha-Phase unter verifizierten Entwickler-Releases **[Empfehlung]** |
| **F-Droid** | Kein Konto nötig; F-Droid sagt, es verfolge nicht, was du installierst **[Extern]** | Keine Google-Abhängigkeit genannt; ein unabhängiges Repository freier und quelloffener Apps **[Extern]** | Über den F-Droid-Client; die Geschwindigkeit hängt von der App ab, denn F-Droid baut nach eigenem Zeitplan, und manche Apps sind veraltet oder hinken dem Entwickler hinterher **[Empfehlung]** | Großer Katalog freier und quelloffener Apps; Qualität und Update-Tempo schwanken je App und Repository **[Empfehlung]** | Apps werden vor der Aufnahme auf Sicherheitsprobleme geprüft **[Extern]**. Bei Apps mit reproduzierbaren Builds veröffentlicht F-Droid die Signatur des Entwicklers, nachdem es den Build geprüft hat; andere Apps werden mit F-Droids eigenen Schlüsseln signiert **[Extern]** | Alltag: Ausweichlösung für Apps, die die obigen Stores nicht führen; prüfen, ob die App gepflegt wird. Cryptophone: nur als Ausweichlösung (Regel in 7.1) **[Empfehlung]** |
| **Aurora Store** | Ja, ein Google-Konto ist nötig. Standardmäßig holt er geteilte Konto-Zugangsdaten vom Dienst von Aurora Store (geteilte Dummy-Konten, die über Token-Dispenser ausgegeben werden); du kannst dich auch mit deinem persönlichen Google-Konto anmelden **[Offiziell]** | Vollständig: Er ist ein alternatives Frontend des Google Play Stores **[Offiziell]** | Aktualisiert die Play-Apps, die er installiert hat. GrapheneOS akzeptiert Updates von Google Play-Diensten, Google Services Framework und Google Play Store nur von seinem eigenen App Store oder vom Play Store selbst, nutze Aurora dafür also nicht **[Offiziell]** | Der gesamte Play-Katalog, überwiegend Closed Source **[Empfehlung]** | Von Entwicklern signierte Play-Apps, aber die Installationen laufen über Google unter einem geteilten oder einem persönlichen Konto. Geteilte Dummy-Konten sind keine Anonymität: Du verlässt dich auf den Dispenser-Dienst, das Konto teilen sich viele andere Nutzer, und Google kann Geräteinformationen und Installationen weiterhin korrelieren; ein persönliches Konto bindet die Installationen an dich **[Empfehlung]** | Alltag: letzter Ausweg, nur in einem separaten Profil und nie mit deinem Haupt-Google-Konto. Cryptophone: nicht nutzen **[Empfehlung]** |
| **Obtainium** | Kein Store-Konto; es liest die eigenen Release-Seiten der Entwickler (zum Beispiel GitHub, GitLab oder F-Droid) **[Extern]** | Keine, sofern die App selbst Google nicht braucht | Prüft die von dir eingerichteten Release-Seiten, benachrichtigt dich über neue Releases und installiert sie **[Extern]**; es ist kein Store mit eigener Prüfung | Alle Apps, die auf unterstützten Release-Seiten APKs veröffentlichen; jede Quelle wählst und richtest du selbst ein | Nur so stark wie dein Vertrauen in jede Quelle und deine Prüfung: Es macht ein unsigniertes oder kompromittiertes Release nicht sicher. Obtainium selbst veröffentlicht einen Fingerabdruck des Signaturzertifikats und einen PGP-Schlüssel zur Prüfung (Obtainium-README, Abschnitt „Installation“) **[Extern]**; sein Quelltext liegt auf GitHub (<https://github.com/ImranR98/Obtainium>) | Alltag: optionale Hilfe für Apps, die nur als APK verteilt werden und die die obigen Stores nicht führen. Cryptophone: nicht standardmäßig; es fügt eine App mit der Berechtigung „Unbekannte Apps installieren“ und Netzwerkzugriff hinzu, nutze es also nur bei dokumentiertem Bedarf und prüfe jede Quelle **[Empfehlung]** |
| **Manueller APK-Download** | Kein Store-Konto; die Seite des Entwicklers entscheidet | Keine, sofern die App selbst Google nicht braucht | Keine automatischen Updates: Jedes Update erfordert ein manuelles erneutes Herunterladen und eine Signaturprüfung (bei Signal nennt signal.org/android/apk den SHA-256-Fingerabdruck und eine apksigner-Prüfung) **[Extern]** | Was der Entwickler veröffentlicht; nicht jede App bietet eine APK | Hängt ganz von deiner Prüfung ab: Vergleiche den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal, gib „Unbekannte Apps installieren“ nur einer App und entziehe es danach wieder **[Empfehlung]** | Alltag: nur, wenn eine App sonst nirgends erhältlich ist. Cryptophone: nur für anderswo nicht erhältliche Apps (zum Beispiel Signal); Signatur prüfen und von Hand aktualisieren **[Empfehlung]** |

**Verbleibendes Risiko:** Der gewählte Store ändert, wer erfährt, welche Apps du installierst, und wie schnell Korrekturen dich erreichen. Er macht eine App nicht vertrauenswürdig, und kein Anmeldemodus eines Google-basierten Stores macht dich anonym.

---

## 8. Kommunikations-OPSEC

- **Nutze Ende-zu-Ende-verschlüsselte Nachrichten.** Prüfe, wer noch **Metadaten** sieht: Kontaktgraph, Zeitpunkte, IP-Adresse, Rufnummer.
- **Verifiziere Sicherheitsnummern oder Sicherheitsschlüssel**, wo die App das unterstützt. Die EFF beschreibt den Vergleich der Ziffern oder des QR-Codes persönlich oder telefonisch und das anschließende Markieren des Kontakts als verifiziert. **[Extern]** Eine geänderte Nummer bedeutet meist ein neues Telefon oder eine Neuinstallation (Signal-Blog), bestätige es aber über einen anderen Kanal. **[Extern]**
- **Glaube „verschlüsselt“-Versprechen nicht blind.** Frage, was verschlüsselt ist, zwischen wem, und was der Anbieter weiterhin weiß.
- **Verwende Rufnummern nicht über Identitäten hinweg wieder.**
- **Füge keine Kontakte aus deinem privaten Leben** zu einer sensiblen Identität hinzu.
- **Bespreche keine operativen Details in Gruppenchats.** Größere Gruppen bedeuten mehr Geräte, die etwas preisgeben können.
- **Verschwindende Nachrichten sind nur eine zusätzliche Kontrolle.** Signal sagt, sie seien „nicht für Situationen, in denen dein Kontakt dein Gegner ist“, und ein Empfänger könne den Bildschirm fotografieren. **[Extern]** Signal-Backups schließen nur Einmal-Ansichts-Nachrichten und Nachrichten aus, die innerhalb von 24 Stunden verschwinden, sodass Nachrichten mit längeren Timern in einem Backup landen können **[Extern]**; nutze kurze Timer oder auf diesem Gerät keine Backups.
- **Das Gerät der anderen Person kann die Unterhaltung kompromittieren.** Ende-zu-Ende-Verschlüsselung schützt den Transport, nicht die Endpunkte.
- **Mache keine Screenshots sensibler Unterhaltungen.** Leite sensibles Material nicht beiläufig weiter.
- **Entferne Metadaten** (EXIF, Dokumenteigenschaften), bevor du Dateien teilst.

**Verbleibendes Risiko:** Ein kompromittierter Endpunkt, ein Screenshot, eine weitergeleitete Nachricht oder ein Beobachter mit Verkehrsanalyse hebelt den Schutz der Inhalte oder der Tatsache der Kommunikation aus.

---

## 9. Netzwerk-OPSEC

### 9.1 Mobilfunknetz

- Eine SIM oder eSIM identifiziert dich gegenüber dem Netzbetreiber. Der Betreiber weiß, welche Funkzellen dein Telefon wann nutzt; laut EFF gibt es keine Möglichkeit, sich dieser Verfolgung zu entziehen, solange das Telefon eingeschaltet ist **[Extern]**, und das Netz beobachtet SIM und Gerät gemeinsam **[Extern]**.
- **Identitätsverknüpfung über den Netzbetreiber:** Wer dieses Gerät zusammen mit dem privaten Telefon zu denselben Zeiten und an denselben Orten mitführt oder einschaltet, zeigt dieselben Funkzellen; gemeinsamer Kauf von SIM und Gerät oder rückverfolgbare Zahlung, Aufladungen sowie SIM-Registrierungs- und Ausweispflichten (länderspezifisch) können die Leitung mit dir verknüpfen. Die IMEI bleibt beim SIM-Wechsel gleich. Die Prämisse, dass Funkzellen Telefone orten, beschreibt die Freedom of the Press Foundation. **[Extern]** Die Verknüpfungsszenarien sind eine **[Empfehlung]**.
- Eine eSIM hat eine eigene Kennung und verlangt bei der Aktivierung oft ein Konto, einen Ausweis oder eine Zahlung. **[Empfehlung]**
- Anrufe, SMS und VoLTE sind Dienste des Netzbetreibers; ein VPN deckt sie nicht ab.
- Der LTE-only-Modus verringert die Ausnutzung von altem Funkmodul-Code aus der Ferne. Er ersetzt keine Ende-zu-Ende-verschlüsselten Anrufe und Nachrichten. **[Offiziell]**
- Die EFF berichtet, dass das Abschalten von 2G vor manchen Cell-Site-Simulatoren schützen kann; konkrete Belege für deren Einsatz bei Protesten habe sie nicht gesehen. **[Extern]** Behaupte nicht mehr.
- **Der Flugmodus macht ein Telefon nicht ortungssicher.** Die Freedom of the Press Foundation weist darauf hin, dass er Standortdienste womöglich nicht blockiert, und die EFF, dass Apps GPS-Daten speichern und später senden können; das Ausschalten ist der stärkste verfügbare Schritt (FPF: „the best technical step“). Kein Softwarezustand ist ein Beweis, und ein ausgeschaltetes Telefon kann dort geortet worden sein, wo es zuletzt eingeschaltet war. **[Extern]**
- **Nur WLAN** (keine SIM) entfernt die SIM-basierte Verbindung zu einem Netzbetreiber, nicht aber IP- oder WLAN-Exposition. Ein Telefon ohne SIM kann dort, wo die nationalen Regeln es erlauben, weiterhin Notrufe absetzen (Android verlangt, dass Notrufnummern ohne SIM funktionieren) **[Extern]**; ob die IMEI dem Netz dann sichtbar ist, ist **[Prüfen]**. Bei einem solchen Gerät muss WLAN notgedrungen an sein (Lockerung von Regel 11), und manche Dienste verlangen bei der Registrierung eine Rufnummer.

### 9.2 Öffentliches WLAN und Captive Portals

- Öffentliches WLAN setzt deinen Verkehr dem Betreiber aus und zeigt deine IP. Nutze es nur für Verkehr, den der Betreiber sehen darf; das gilt auch für Updates und App-Installationen, und meide dein Heim-WLAN, wenn Verknüpfung eine Rolle spielt (Abschnitt 9.5). **[Empfehlung]**
- **Captive Portals** verlangen womöglich Rufnummer oder E-Mail-Adresse. **[Empfehlung]** Die EFF warnt (Artikel von 2017), sie ähnelten einem Man-in-the-Middle, trainierten Nutzer, Zertifikatswarnungen zu ignorieren, und könnten Aktivität an ein Login oder eine Identität binden. **[Extern]** Bei aktivem **Verbindungen ohne VPN blockieren** lässt sich ein Portal-Login nicht abschließen; hebe die Sperre nur vorübergehend auf, wenn du das in Kauf nimmst, oder meide das Portal. **[Empfehlung]**
- Videoüberwachung, Zahlungsbelege und Standortmuster können eine Person weiterhin einem Ort zuordnen.
- Ein VPN verbirgt Ziele und Inhalte vor dem lokalen Netz, nicht die Tatsache, dass ein VPN genutzt wird.

### 9.3 VPN, Tor, DNS

| Werkzeug | Hilft bei | Hilft nicht bei |
|---|---|---|
| **VPN** | Nicht vertrauenswürdigem lokalem Netz oder Provider; verbirgt deine IP vor Websites | Dem VPN-Anbieter, der den Verkehr sieht; Funkzellen-Ortung; Konten, in die du dich einloggst; Anrufen und SMS. „A VPN is not a tool for anonymity“; „If you are interested in increased anonymity, Tor is a better solution than a VPN“ **[Extern]** |
| **Tor Browser** | Verbirgt deine IP vor Websites durch Mehrfach-Routing | Anmeldung oder Preisgabe deines Namens hebelt es aus („they know who you are“); Tor schützt nur Apps, die dafür konfiguriert sind; Der Tor Browser rundet Fenstergrößen, um Fingerprinting zu begrenzen, und Größenänderungen schwächen das; behalte daher die Standardfenstergröße bei (**[Empfehlung]**); installiere keine zusätzlichen Add-ons und nutze Tor nicht mit anderen Browsern **[Extern]**. Auf dem Handy nennt das Projekt seine Sicherheit schwach **[Offiziell]** |
| **Private DNS** | Opportunistischer oder authentifizierter DNS-Verschlüsselung | Kein Ersatz für Tor oder ein VPN; bei aktivem VPN aus **[Offiziell]** |

**Tor ist nicht für alles geeignet.** Es ist langsam, fingerprintbar und macht keine App außerhalb des Browsers anonym. Das Tor Project bietet Tor VPN (Beta) an, um andere Apps umzuleiten, und sagt, die Beta sei „nicht für sensible Aktivitäten“ gedacht **[Extern]**; Orbot ist eine App des Guardian Project. Ein GrapheneOS-Maintainer schrieb 2020 im Issue-Tracker des Projekts, Orbot sei schlecht umgesetzt und gepflegt und das Projekt werde es weder forken noch bündeln **[Offiziell]**; FAQ und Usage-Seiten nennen keine Tor-App, und die Haltung des Projekts zu Tor VPN ist **[Prüfen]** (in den geprüften Quellen nicht genannt).

### 9.4 Bluetooth und Geräte in der Nähe

- Lass Bluetooth aus. Tracker und Beacons in der Nähe können ein Gerät protokollieren, das sich bemerkbar macht. **[Empfehlung]**
- Koppele dieses Gerät nicht mit Zubehör, das mit deiner persönlichen Identität verbunden ist.

### 9.5 Identitäten über das Netz nie vermischen

Melde dich auf diesem Gerät nicht in privaten Konten an, öffne keine privaten Links und nutze nicht dasselbe Heim-WLAN für die sensible und deine private Identität, wenn Verknüpfung eine Rolle spielt.

**Verbleibendes Risiko:** Netzbetreiber, WLAN-Betreiber, VPN-Anbieter und Zielserver sehen jeweils einen Ausschnitt. Kein Werkzeug in diesem Abschnitt beseitigt alle auf einmal.

---

## Behavioral OPSEC / Verhaltens-OPSEC

Die Einstellungen in Abschnitt 4 schützen das Gerät. Dieser Abschnitt behandelt, was du damit tust, denn Identitäten werden meist durch Gewohnheiten verknüpft, nicht durch technische Schwächen. Jede Empfehlung unten nennt ihre Grenze, und keine macht dich anonym. Quellen sind die GrapheneOS-Dokumentation **[Offiziell]**, genannte externe Primärquellen wie EFF Surveillance Self-Defense, Freedom of the Press Foundation und Tor Project **[Extern]** (siehe Abschnitt „Nützliche Webseiten“) sowie die Einschätzung dieses Leitfadens **[Empfehlung]**. Alles Unbestätigte ist **[Prüfen]**.

### SIM-/eSIM-Disziplin

| Situation | Tun | Warum | Grenze |
|---|---|---|---|
| Konnektivität wählen | Nutze für diese Identität eine eigene SIM oder eSIM oder bleibe bei reinem WLAN, wenn du ohne Anrufe, SMS und mobile Daten auskommst **[Empfehlung]** | Eine eigene Leitung ist nicht mit deinem normalen Telefon verknüpft; reines WLAN entfernt die SIM-basierte Verbindung zu einem Netzbetreiber | Eine SIM bindet die Leitung weiterhin an einen Netzbetreiber sowie an Registrierungs- und Zahlungsdaten. Reines WLAN zeigt weiterhin deine IP-Adresse und die genutzten WLAN-Netze, und manche Dienste verlangen bei der Registrierung eine Rufnummer |
| Dieselbe SIM oder eSIM für mehrere Identitäten | Niemals (siehe Regel 5 der Geräterichtlinie) | Eine SIM ist eine IMSI und eine Nummer beim Netzbetreiber; jede Identität, die sie nutzt, lässt sich vom Netzbetreiber und von jedem, der die Nummer kennt, verknüpfen **[Empfehlung]** | Auch getrennte SIMs lassen sich über die übrigen Punkte dieses Abschnitts verknüpfen |
| IMSI/IMEI-Paarung | Wechsle die SIM nicht zwischen Telefonen und setze keine alte SIM in ein neues Telefon | Das Netz beobachtet SIM und Gerät gemeinsam, daher bietet das Umstecken einer SIM in ein anderes Gerät nur minimalen Schutz (EFF) **[Extern]** | Eine bereits protokollierte Paarung lässt sich nicht rückgängig machen; eine neue SIM in einem alten Telefon verknüpft genauso |
| eSIM | Behandle eine eSIM wie eine SIM | Eine eSIM hat eine EID, die ihre eUICC-Hardware identifiziert (Android-Dokumentation) **[Extern]**; die Aktivierung braucht oft ein Konto, einen Ausweis oder eine Zahlung, sie ist also nicht anonymer **[Empfehlung]** **[Prüfen]** (keine Primärquelle für den Teil zu Konto, Ausweis oder Zahlung gefunden). Die eSIM-Unterstützung ist in GrapheneOS standardmäßig aus **[Offiziell]** | Ein Duress-Wipe entfernt auch installierte eSIM-Profile **[Offiziell]**; ein erneuter Download hängt vom Netzbetreiber ab |
| SIM entfernen oder deaktivieren | Entferne die SIM oder deaktiviere die eSIM, wenn du kein Mobilfunknetz brauchst und die Verbindung zum Netzbetreiber vermeiden willst | Beendet die SIM-basierte Anmeldung im Netz **[Empfehlung]** | Notrufe können ohne SIM funktionieren, wo die nationalen Regeln es erlauben **[Extern]**; ob die IMEI dem Netz dann sichtbar ist, ist **[Prüfen]**; WLAN- und IP-Exposition bleiben |
| Prepaid- oder „anonyme“ SIM | Kenne die Grenzen, bevor du dich darauf verlässt | Prepaid verringert nur Vertrags- und Abrechnungsspuren | Die meisten Länder verlangen für den Kauf einer Prepaid-SIM einen Ausweis (EFF) **[Extern]**; die genauen Regeln sind länderspezifisch **[Prüfen]**; Kauf mit Karte, gemeinsamer Kauf mit dem Telefon, Aufladen mit rückverfolgbarer Zahlung und gemeinsames Mitführen mit dem privaten Telefon hinterlassen jeweils Spuren **[Empfehlung]** |
| Rufnummer | Verwende deine private Nummer nie für eine sensible Identität | Die Nummer verknüpft Konten, auch dein Messenger-Konto | Signal verlangt bei der Registrierung eine Nummer; Benutzernamen verbergen sie nur vor anderen Nutzern **[Extern]** |

### Wann du das Telefon ausschalten solltest

**BFU und AFU.** Before First Unlock (BFU) ist der Zustand nach dem Start bis zum ersten Entsperren: Die Daten ruhen, und die Profilschlüssel liegen nicht im Speicher. Nach dem ersten Entsperren (After First Unlock, AFU) liegen die Schlüssel im Speicher, und es liegt mehr Angriffsfläche offen. Das Auto-Reboot von GrapheneOS versetzt ein gesperrtes Gerät nach einer festgelegten Zeit in den verschlüsselten Zustand vor dem ersten Entsperren (BFU) zurück und greift nicht, solange das Gerät schon in BFU ist. **[Offiziell]**

| Wann | Tun | Warum | Grenze |
|---|---|---|---|
| Vor sensiblen Orten oder Treffen | Schalte das Telefon vollständig aus, bevor du ankommst, nicht erst an der Tür **[Empfehlung]** | Ein ausgeschaltetes Telefon erzeugt keine neue Funkaktivität und keine neue Standortspur | Der Netzbetreiber und andere Beobachter sehen weiterhin, wo und wann das Telefon offline ging, und die Gewohnheit, am selben Ort auszuschalten, ist selbst ein Signal **[Empfehlung]** |
| Vor Grenzen und riskanten Kontrollstellen | Schalte vollständig aus und starte das Telefon erst an einem Ort, dem du vertraust **[Empfehlung]**. Das EFF-Material zur US-Grenze nennt dasselbe **[Extern]** (auf die USA bezogen, siehe Abschnitt 10) | Ein vollständig ausgeschaltetes Gerät befindet sich in BFU | Verhindert keine Durchsuchung des Geräts; die Regeln unterscheiden sich je Land **[Prüfen]** |
| Wenn es nicht aktiv gebraucht wird | Lass es ausgeschaltet | Weniger Standortspur, weniger Exposition | Im ausgeschalteten Zustand erhältst du keine Nachrichten oder Benachrichtigungen; wende die Regel nicht an, wenn du erreichbar sein musst |
| Auto-Reboot | Lass es an (Abschnitt 4.1) | Versetzt ein ungenutztes Gerät auch dann in BFU zurück, wenn du es vergisst | Es ist nur eine Teilmaßnahme: Es hilft nicht bei einer Beschlagnahme, die vor Ablauf des Timers geschieht, und ersetzt kein manuelles Ausschalten **[Empfehlung]** |

**Ausgeschaltet heißt nicht „nicht ortbar“.** Die Freedom of the Press Foundation nennt das Ausschalten des Geräts den besten technischen Schritt gegen Standortverfolgung **[Extern]**. Es kann bereits vorhandene Standortverläufe nicht rückgängig machen. Die FPF weist darauf hin, dass in seltenen Fällen WLAN- und Bluetooth-Signale auch bei ausgeschaltetem Gerät weiter ausgesendet werden können **[Extern]**, und die EFF, dass Schadsoftware ein Ausschalten vortäuschen könnte **[Extern]**. Der Flugmodus ist schwächer: Er blockiert Standortdienste womöglich nicht, und Apps können Standortdaten speichern und später senden **[Extern]**.

**Faraday-Beutel.** Ein Beutel kann nützlich sein, wenn du ein Gerät nicht zurücklassen kannst und Funksignale blockieren willst, solange es darin liegt; die FPF nennt ihn als Option für den strengsten Standortschutz **[Extern]**. Er wiegt dich in falscher Sicherheit, wenn du ihn nicht testest, wenn er nicht vollständig geschlossen ist oder wenn du glaubst, er schütze vor einem kompromittierten Gerät oder behebe schlechte Gewohnheiten. Die FPF nennt keine Grenzen, daher sind die oben genannten Grenzen eine **[Empfehlung]**; die FPF merkt zudem an, dass das Zurücklassen des Geräts die einzig sichere Methode ist **[Extern]**. Er ersetzt das Ausschalten nicht.

### Was du NICHT tun solltest

| Nicht tun | Warum | Grenze |
|---|---|---|
| In alten privaten Konten anmelden (Google, soziale Medien, Banking) | Eine einzige Anmeldung bindet das Gerät an deine echte Identität | Ein neues Konto ist eine neue Spur; neue Konten brauchen weiterhin eine saubere E-Mail-Adresse, Nummer und Zahlungsmethode |
| Benutzernamen, E-Mail-Adressen, Profilbilder oder Wiederherstellungskontakte wiederverwenden | Wiederverwendung ist ein häufiger Weg, Identitäten zu verknüpfen | Schreibstil, Zeitpunkte und Kontakte können Identitäten weiterhin verknüpfen |
| Beiläufig Kontakte mit echtem Namen hinzufügen | Kontaktgraphen identifizieren Personen | Ist ein Kontakt mit echtem Namen nötig, nutze Contact Scopes (Abschnitt 4.3); der Kontakt weiß trotzdem, wer du bist |
| Operative Details in Gruppenchats besprechen | Mehr Mitglieder bedeuten mehr Geräte, die etwas preisgeben können | Ende-zu-Ende-Verschlüsselung schützt nicht vor dem kompromittierten Gerät eines Mitglieds |
| Beiläufig Screenshots machen oder sensibles Material weiterleiten | Kopien bleiben bestehen und wandern aus deiner Kontrolle | Verschwindende Nachrichten verhindern nicht, dass ein Empfänger den Bildschirm fotografiert **[Extern]** |
| Dieselbe Zahlungsmethode für sensible und private Käufe nutzen | Zahlungsdaten verknüpfen Identitäten | Jede Zahlungsmethode hinterlässt eigene Daten; auch Bargeld hat Grenzen (Videoüberwachung, Seriennummern) **[Empfehlung]** |
| Apps „nur zum Ausprobieren“ installieren | Jede App erhöht Vertrauensbedarf und Angriffsfläche (Abschnitt 7) | Deinstallieren macht nicht rückgängig, was die App bereits gesammelt hat |
| Gespeicherte oder private WLAN-Netze behalten oder versteckte Netze beitreten | Versteckte Netze werden beim Scannen deines Telefons ausgesendet **[Offiziell]**; gespeicherte private Netze binden das Gerät an Orte, mit denen du verknüpft bist **[Empfehlung]** | Jedes WLAN zeigt dem Betreiber weiterhin deine IP-Adresse und Zeitpunkte; MAC-Randomisierung verbirgt kein Verhalten |
| Bluetooth-Zubehör nutzen, das mit deinen persönlichen Geräten verbunden ist | Die Kopplung verknüpft Geräteidentitäten | Bluetooth-Beacons und Geräte in der Nähe können ein Gerät, das sich bemerkbar macht, weiterhin beobachten **[Empfehlung]** |
| „Gelöschte“ Daten als Schutz betrachten | Gelöschte Daten können in Backups, Caches und auf Geräten von Empfängern fortbestehen | Die vollständige Speicherverschlüsselung schützt ruhende Daten, nicht Daten, die schon anderswohin kopiert wurden **[Empfehlung]** |

### Tägliche Gewohnheiten

| Gewohnheit | Warum | Grenze |
|---|---|---|
| Das Gerät ausgeschaltet lassen, wenn es nicht gebraucht wird | Weniger Exposition und Standortspur | Du verpasst Nachrichten; wähle ein Intervall, das du durchhältst |
| Eine starke Passphrase statt nur Biometrie (Abschnitt 2) | Widersteht Raten und erzwungener biometrischer Entsperrung | Hilft nicht mehr, sobald das Telefon in deiner Hand entsperrt ist |
| Auto-Reboot eingeschaltet lassen | Versetzt das Gerät in BFU zurück | Nur eine Teilmaßnahme (siehe oben) |
| Regelmäßig nach Updates suchen | Sicherheitskorrekturen gehören zu den wertvollsten Schutzmaßnahmen **[Empfehlung]** | Hält unbekannte Schwachstellen nicht auf |
| Installierte Apps und Berechtigungen wöchentlich prüfen | Erkennt Abweichungen und vergessene Apps | Eine vertrauenswürdige App kann gewährte Rechte trotzdem missbrauchen |
| Verschwindende Nachrichten als zusätzliche Ebene nutzen | Verringert, was auf Geräten zurückbleibt | „Nicht für Situationen, in denen dein Kontakt dein Gegner ist“, und der Empfänger kann den Bildschirm fotografieren **[Extern]** |
| Sicherheitsnummern mit Kontakten verifizieren | Erkennt einen geänderten Schlüssel | Die EFF beschreibt den Vergleich der Ziffern oder des QR-Codes persönlich oder telefonisch **[Extern]**. Eine geänderte Nummer bedeutet meist ein neues Telefon oder eine Neuinstallation (Signal-Blog); bestätige sie über einen anderen Kanal **[Extern]** |
| Das Gerät physisch sichern und nie unbeaufsichtigt lassen | Physischer Zugriff umgeht viele Schutzmaßnahmen | Auch ein gesperrtes, beaufsichtigtes Gerät kann weggenommen werden; betrachte ein Gerät, das außerhalb deiner Kontrolle war, als nicht vertrauenswürdig (Abschnitt 11) |

### Verhalten auf Reisen

Abschnitt 10 enthält die vollständigen Reise- und Grenzdetails. Im Alltag gilt:

- **Entscheide vor der Reise, was auf dem Gerät sein muss.** Entferne den Rest, soweit praktikabel auch Chat- und Browserverläufe **[Extern]** (Reise-Checkliste der EFF von 2025 für Journalisten, auf die USA bezogen). Grenze: Alles, was bleibt, kann bei einer Durchsuchung gelesen werden.
- **Erwäge ein separates Reisegerät oder ein sauberes Profil.** Grenze: Der EFF-Grenzleitfaden von 2017 warnt, dass ungewöhnliche oder geleerte Geräte Verdacht und Nachfragen auslösen können **[Extern]** (auf die USA bezogen), und das Gerät hat trotzdem eine SIM und eine IMEI.
- **Schalte vor Grenzen und Kontrollstellen aus.** Grenze: Es verhindert die Durchsuchung selbst nicht.
- **Grenzdurchsuchungen können stattfinden; nimm nichts mit, was du dir nicht leisten kannst zu verlieren oder gelesen zu wissen.** Die Regeln unterscheiden sich je Land **[Prüfen]**. Grenze: Keine Einstellung macht ein beschlagnahmtes Gerät sicher.
- **Verlasse dich nicht auf versteckte Dateien oder „gelöschte“ Daten.** Grenze: Forensik-Werkzeuge können mehr wiederherstellen, als die meisten Nutzer erwarten **[Empfehlung]**.
- **Halte einen Wiederherstellungsplan für verlorene, beschlagnahmte oder kompromittierte Geräte bereit** (Abschnitt 11), mit Wiederherstellungscodes offline und getrennt vom Gerät. Grenze: Ein Plan hilft nur, wenn du ihn durchspielst.

### Identitätstrennung in der Praxis

- **Ein Gerät entspricht einer Identität, oder es gibt strikt getrennte Profile.** Grenze: Alle Profile teilen Hardware, SIM, IMEI, IP-Adresse und deine Gewohnheiten **[Offiziell]** (Profilisolierung) **[Empfehlung]** (die Grenzen).
- **Vermische nie eine sensible und eine private Identität im selben Profil.** Grenze: Ein Profil trennt Daten, nicht die Person, die es nutzt.
- **Nutze pro Identität eine eigene E-Mail-Adresse, Rufnummer, einen eigenen Benutzernamen und ein eigenes Profilbild.** Grenze: Du musst sie jedes Mal getrennt halten; ein einziger Ausrutscher verknüpft sie.
- **Teile zwischen Identitäten keine Dateien, Zwischenablageinhalte oder Benachrichtigungen.** Grenze: Ein Screenshot oder eine kopierte Zeile genügt, um die Grenze zu überschreiten.
- **Metadaten können Identitäten auch bei technischer Trennung korrelieren.** Zeitpunkte, Standort, Kontakte und Schreibstil sind Signale **[Empfehlung]**; wer sich bei Tor in einem Konto anmeldet, verrät der Seite, wer er ist **[Extern]**.

**Verbleibendes Risiko:** Verhalten ist das schwächste Glied: Es erfordert tägliche Disziplin, und ein einziger Fehler kann Monate der Trennung zunichtemachen. Für eine Rolle mit hohem Risiko sind ein separates Gerät, eine separate SIM oder eSIM und ein getrenntes Netzwerknutzungsmuster die realistische Grenze; dieser Abschnitt verringert die Exposition, er beseitigt sie nicht.

---

## 10. Reisen und physische Sicherheit

Das ist keine Rechtsberatung. Regeln zu Durchsuchung, Beschlagnahme und erzwungener Entsperrung unterscheiden sich je Land und ändern sich. **[Prüfen]** Die Regeln jedes Landes, in das du einreist oder durch das du reist. Das hier zitierte EFF-Grenzmaterial ist nur eine US-Grundlage; die Grenzhinweise von EFF SSD und FPF gelten nur für die USA, und keine Primärquelle im Prüfumfang deckt andere Länder ab.

### 10.1 Vor der Reise

- **Daten minimieren.** Entscheide, was auf dem Gerät sein muss, und entferne den Rest, soweit praktikabel auch Chat- und Browserverläufe. **[Extern]** (Reise-Checkliste der EFF für Journalisten, auf die USA bezogen)
- **Unnötige Apps entfernen.**
- **Nutze ein Reisegerät oder ein sauberes Profil**, falls angemessen; nimm keine sensiblen Daten mit, die du dir nicht leisten kannst zu verlieren oder gelesen zu wissen. Der EFF-Grenzleitfaden von 2017 warnt, dass ungewöhnliche oder geleerte Geräte Verdacht und Nachfragen auslösen können. **[Extern]** (auf die USA bezogen)
- **Aktualisieren und neu starten.** Kurzes Auto-Reboot-Intervall setzen.
- **Sichere** nur, was du brauchst, verschlüsselt, und bewahre das Backup an anderer Stelle auf.
- **Wiederherstellungscodes** bleiben offline, verschlüsselt und getrennt vom Gerät.

### 10.2 An Grenzen und Kontrollstellen

- **Schalte das Gerät vor der Kontrolle vollständig aus**; die EFF merkt an, dass ein vollständig heruntergefahrenes Gerät die Festplattenverschlüsselung wiederherstellt. **[Extern]** (auf die USA bezogene Checkliste)
- **Starke Authentifizierung.** Lange, unvorhersehbare alphanumerische Geheimnisse werden empfohlen; die EFF-Checkliste von 2025 rät, vorab zu entscheiden, ob du entsperrst, und es in dem Fall selbst einzugeben und anwesend zu bleiben (auf die USA bezogen). **[Extern]**
- **Biometrie:** Die EFF sagt, im Protestkontext bestehe weniger Schutz gegen erzwungenes Entsperren per Gesicht oder Fingerabdruck als gegen erzwungene Herausgabe eines Passworts. **[Extern]** Lass die Biometrie ausgeschaltet. Rechtsordnungsabhängig. **[Prüfen]**
- **Kenne die Realität von Grenzdurchsuchungen:** In den USA kann Nicht-Staatsbürgern, die eine Durchsuchung verweigern, die Einreise verweigert werden (EFF-Checkliste; auf die USA bezogen). **[Extern]**
- Nach der Richtlinie der US-Grenzbehörde CBP dürfen Beamte nur auf dem Gerät gespeicherte Daten durchsuchen, nicht Live-Cloud-Inhalte (auf die USA bezogen; andere Länder weichen ab). Die EFF-Checkliste von 2025 sagt, Beamte müssten das Gerät in den Flugmodus versetzen oder anderweitig trennen; die aktuelle CBP-Richtlinie zur Grenzdurchsuchung ist Nr. 3340-049B vom 28.01.2026 (<https://www.cbp.gov/document/directives/cbp-directive-no-3340-049b-border-search-electronic-devices>), und die EFF bezweifelt, dass die Praxis immer der Richtlinie entspricht. **[Extern]** **[Prüfen]** (nur Titel und Datum der Richtlinie ließen sich bestätigen; ihr Text ist ein gescanntes PDF und war nicht lesbar) Der Flugmodus schützt keine bereits auf dem Gerät liegenden Daten und macht das Telefon nicht ortungssicher (Abschnitt 9.1).
- **Duress/Löschen:** Verlasse dich nicht darauf. Das Löschen von Daten während einer erzwungenen Entsperrung kann in manchen Rechtsordnungen als Behinderung gewertet werden, und die Verweigerung eines Passcodes kann in manchen Rechtsordnungen selbst eine Straftat sein. **[Prüfen]** Hole zuerst lokalen Rechtsrat ein.

### 10.3 Physische Maßnahmen

- **Verlasse dich nicht auf versteckte Dateien oder „gelöschte“ Daten** als Schutz.
- **Faraday-Beutel:** Die Freedom of the Press Foundation nennt sie als Option für den strengsten Standortschutz, wenn du ein Gerät nicht zurücklassen kannst. **[Extern]** Die FPF stellt ihn als letzte Möglichkeit dar und nennt keine Grenzen; ob ein Beutel wirkt, lässt sich kaum selbst prüfen. **[Empfehlung]** Ein Faraday-Beutel behebt keine OPSEC-Fehler; er blockiert nur Funksignale, solange das Gerät darin liegt.
- Meide öffentliche USB-Ladeanschlüsse; nutze dein eigenes Ladegerät und Kabel.
- Lass das Gerät nie unbeaufsichtigt. War es außerhalb deiner Kontrolle, betrachte es als nicht vertrauenswürdig und prüfe die Auditor-Attestierung. **[Empfehlung]**

**Verbleibendes Risiko:** Ein entschlossener Gegner mit physischer Kontrolle über ein entsperrtes oder nach dem ersten Entsperren befindliches Gerät kann trotzdem Erfolg haben. Reiseratschläge verringern die Exposition; sie garantieren keine Sicherheit.

---

## 11. Reaktion auf Vorfälle

Für jedes Szenario: Sofortmaßnahmen, was als kompromittiert gilt, was zu rotieren ist, was zu unterlassen ist und wann das Gerät nicht mehr genutzt werden sollte. Es handelt sich um **[Empfehlung]**, sofern nicht anders angegeben.

| Szenario | Sofortmaßnahmen | Als kompromittiert annehmen | Rotieren | Nicht tun | Gerät nicht mehr nutzen, wenn |
|---|---|---|---|---|---|
| **Gerät verloren** | Wenn möglich ausschalten; Zeit und Ort notieren; vertraute Kontakte auf anderem Weg informieren | Alles darauf, wenn das Geheimnis schwach oder das Gerät entsperrt war | Konten und Sitzungen, die darauf aktiv waren | Die Nummer des verlorenen Geräts nicht zum „Testen“ anrufen oder anschreiben; den Netzbetreiber bitten, die SIM zu sperren (eine SIM-PIN hilft); nicht annehmen, es sei gelöscht worden | es nicht zurückkommt oder nach unbekanntem Zugriff zurückkommt |
| **Gerät gestohlen** | Wie oben; ggf. melden | Alles darauf, auch zwischengespeicherte Nachrichten | Messenger-Sitzungen, Passwörter, 2FA-Seeds, Wiederherstellungscodes, die darauf lagen | Keine Vergeltung, keinen Kontakt zum Dieb | Immer (ersetzen) |
| **Verdacht auf Schadsoftware** | Sensible Nutzung stoppen; neu starten und aktualisieren; installierte Apps und Berechtigungen prüfen; saubere Neuinstallation erwägen | Das Profil und jedes darauf eingegebene oder angezeigte Geheimnis | Alles, was auf dem Gerät genutzt wurde | Nicht an Ort und Stelle „säubern“ und weiter nutzen | eine Neuinstallation die Symptome nicht beseitigt |
| **Verdächtige App** | Deinstallieren; Berechtigungen entziehen; prüfen, worauf sie zugegriffen hat | Daten, die die App erreichen konnte (Netzwerk, Kontakte, Speicher) | Zugangsdaten, die während der Installation eingegeben wurden | Nicht „zum Test“ neu installieren | sie weitreichenden Zugriff hatte, den du nicht ausschließen kannst |
| **Kontokompromittierung** | Überall abmelden; Passwort und 2FA von einem sauberen Gerät ändern; Sitzungen und verknüpfte Geräte widerrufen | Das Konto, seine Kontakte, sein Verlauf | Passwort, Wiederherstellungsdaten, 2FA-Seed | Das alte Passwort nicht wiederverwenden; den Wiederherstellungskontakt des Kontos nicht wiederverwenden | das Konto nicht wiederhergestellt werden kann |
| **SIM/eSIM-Kompromittierung** | Netzbetreiber kontaktieren (nach SIM-PIN und einer Sperre gegen Rufnummernmitnahme/SIM-Swap fragen); von einer Nummernübernahme ausgehen; Kontakte über einen anderen Kanal neu verifizieren; Signals Registrierungssperre (Registration Lock) erwägen **[Extern]** (eine PIN für die erneute Registrierung; Signal kann die PIN weder zurücksetzen noch wiederherstellen, und wer sie bei aktivierter Registrierungssperre vergisst, kann bis zu 7 Tage ausgesperrt sein; die Registrierungssperre läuft nach 7 Tagen Inaktivität ab; eine erneute Registrierung kann statt SMS einen Token plus die Signal-PIN nutzen, und Tokens werden durch eine neue Registrierung oder die Kontolöschung ungültig **[Extern]**) | Die Rufnummer und alles, was per SMS verifiziert wurde | Konten, die die Nummer für Wiederherstellung oder 2FA nutzen | Danach nicht auf SMS-2FA verlassen | du die Nummer nicht zurückerhältst |
| **Physische Beschlagnahme** | Wo das Recht es erlaubt, kannst du Antworten verweigern; Rechtshilfe suchen **[Prüfen]** für dein Land; festhalten, was geschah | Das Gerät und alles darauf, auch wenn es zurückgegeben wird | Alle Konten und Geheimnisse, die darauf waren | Das Gerät nicht ohne vollständiges erneutes Flashen über den offiziellen Installer (Entsperren, Flashen, Sperren) weiterverwenden. Bei ausgeschalteter OEM-Entsperrung setzt das ein Gerät voraus, das noch startet und die Wiederaktivierung erlaubt; ist das nicht möglich, betrachte es als dauerhaft nicht vertrauenswürdig und ersetze es. Nie nach einem fehlgeschlagenen oder unvollständigen Flash sperren | Immer, außer du kannst die Integrität prüfen (Auditor, saubere Neuinstallation) und akzeptierst das Risiko |
| **Versehentliche Identitätsverknüpfung** | Stoppen; die verknüpfte Identität nicht mehr nutzen; auflisten, was offengelegt wurde | Die betroffene Identität und ihre Kontakte | Benutzernamen, E-Mail, Rufnummer, wo möglich | Daten nicht so löschen oder vernichten, dass es in deiner Rechtsordnung rechtswidrig sein kann; vorher Rechtsrat einholen **[Prüfen]** | die Verknüpfung nicht aufgelöst werden kann |

> ⚠️ Nutze den Duress-Wipe nicht als allgemeines Werkzeug der Vorfallsreaktion. Er ist unumkehrbar. **[Offiziell]**

**Verbleibendes Risiko:** Du merkst womöglich nicht, dass ein Vorfall stattgefunden hat. Behandle unerklärliches Verhalten als Vorfall.

---

## Useful websites / Nützliche Webseiten

Nur offizielle oder renommierte gemeinnützige Quellen. Vertrauensstufen sind die Einschätzung dieses Leitfadens.

| Name | URL | Zweck | Wann nutzen | Vertrauen | Warnung |
|---|---|---|---|---|---|
| GrapheneOS | <https://grapheneos.org/> | Offizielle Dokumentation: Installation, Nutzung, Features, FAQ, Releases | Vor jeder Installation oder Änderung | Am höchsten für GrapheneOS | Menüs ändern sich je Version |
| GrapheneOS-Diskussionsforum | <https://discuss.grapheneos.org/> | Offizielles Forum für längere Beiträge, von der Kontaktseite verlinkt | Fragen, die die Doku nicht beantwortet | Hoch, aber Beiträge sind Nutzerinhalte | Keine verbindliche Aussage, sofern nicht vom Projekt |
| Tor Project | <https://www.torproject.org/>, <https://support.torproject.org/tor-browser/features/fingerprinting-protections/>, <https://support.torproject.org/tor-browser/security/using-tb-safely/> und <https://support.torproject.org/tor-browser/security/using-tor-with-other-browsers/> | Dokumentation und Support zum Tor Browser | Vor der Nutzung von Tor | Hoch | Tor schützt nicht vor dem, was du durch Anmeldung preisgibst |
| Signal | <https://signal.org/>, <https://signal.org/blog/phone-number-privacy-usernames/>, <https://signal.org/android/apk/>, <https://support.signal.org/hc/en-us/articles/360007059792-Signal-PIN> und <https://support.signal.org/hc/en-us/articles/5440120029082-Re-registering-using-your-Signal-PIN> | Dokumentation, Blog und Support-Artikel zum Messenger | Bevor du dich auf Signal-Funktionen verlässt | Hoch für Signal-Verhalten | Registrierung erfordert eine Nummer; Signal kann deine PIN weder zurücksetzen noch wiederherstellen |
| EFF Surveillance Self-Defense | <https://ssd.eff.org/> | Bedrohungsmodellierung („Your Security Plan“), Passwörter, Signal, VPNs, Proteste, Telefone | Planung und Lernen | Hoch (gemeinnützig) | Oft auf die USA bezogen; das VPN-Modul sagt, es könne für kein VPN bürgen |
| Freedom of the Press Foundation | <https://freedom.press/digisec/> und <https://freedom.press/digisec/guides/> | Schulungen und Leitfäden zur digitalen Sicherheit für Journalisten | Quellenschutz, Standortprivatsphäre | Hoch (gemeinnützig) | Leitfäden sind unterschiedlich alt; Datum prüfen |
| Reporter ohne Grenzen (RSF) | <https://rsf.org/en/digital-security-lab> und <https://resources.rsf.org/digital-security-and-spyware-guide/> | Digital Security Lab von Reporter ohne Grenzen (forensische Unterstützung für Journalisten) und sein Digital Security and Spyware Guide (veröffentlicht am 17.12.2025) | Kontext und Sicherheit für Journalisten | Hoch (gemeinnützig) | RSF nennt ungefähre Menüpfade, die je nach Android-Version und Hersteller abweichen, und gibt keine länderspezifische Rechtsberatung |
| Have I Been Pwned | <https://haveibeenpwned.com/> | Prüfen, ob eine E-Mail-Adresse in bekannten Datenlecks auftaucht | Nach einem Verdacht auf Kontokompromittierung | Renommiert | Du übermittelst eine E-Mail-Adresse an Dritte; von einem anderen Gerät und mit einer Adresse, deren Offenlegung du akzeptierst |
| Accrescent | <https://accrescent.app/> | App Store für Android | Bewertung von App-Quellen | Renommiert, in Alpha | In der Alpha-Phase; im GrapheneOS App Store verfügbar |
| F-Droid | <https://f-droid.org/>, <https://f-droid.org/en/about/> und <https://f-droid.org/docs/FAQ_-_App_Developers/> | Quelloffenes App-Repository | App-Beschaffung | Renommiert | Das Signaturmodell hängt von der Reproducible-Build-Verifizierung ab |
| Aegis Authenticator | <https://github.com/beemdevelopment/Aegis> | Offizielles Repository (GPL-3.0) | Installieren und prüfen | Offizielle Projektseite | Signaturzertifikat prüfen |
| KeePassDX | <https://github.com/Kunzisoft/KeePassDX> und <https://www.keepassdx.com/> | Offizielles Repository und offizielle Seite (GPL-3.0) | Installieren und prüfen | Offizielle Projektseite | Kostenlose und Pro-Version bei Google Play |
| Mullvad VPN | <https://mullvad.net/> und <https://github.com/mullvad/mullvadvpn-app> | Offizielle App und Quelltext | Nur wenn ein VPN begründet ist | Offiziell; von der GrapheneOS-FAQ empfohlen | Ein VPN ist keine Anonymität |
| Cryptomator | <https://cryptomator.org/android/>, <https://github.com/cryptomator/android> und <https://docs.cryptomator.org/android/setup/> | Offizielle App-Seiten | Optionaler verschlüsselter Speicher | Offiziell | Kanal und Lizenz unterscheiden sich; prüfen |
| Organic Maps | <https://organicmaps.app/> und <https://github.com/organicmaps/organicmaps> | Offline-Karten | Optional | Offiziell | Das Projekt beschreibt seine Finanzierung selbst als prekär |
| Tor-Browser-Download | <https://download.torproject.org/> | Offizieller Download des Tor Browsers für Android | Nur wenn Tor begründet ist | Offiziell | Keine Add-ons installieren und Tor nicht mit anderen Browsern nutzen |
| privacygear.nl GrapheneOS-Härtungsleitfaden | <https://privacygear.nl/en/guides/grapheneos-hardening-guide/> | Einstellungs-Anleitung mit Menüpfaden (Lockdown, NFC, Memory Tagging) | Gegenprüfung von Menüpfaden | Sekundärquelle (geprüft am 05.11.2026, GrapheneOS 2026110200); keine offizielle GrapheneOS-Dokumentation | Pfade variieren je nach Version und Android-Version; es empfiehlt Orbot für Tor auf App-Ebene, was ein GrapheneOS-Maintainer 2020 kritisiert hat |

Bewusst ausgeschlossen: VPN-Affiliate-Listen, Verkäufer „anonymer Telefone“, Seiten mit gecrackten Apps, zufällige Telegram-Kanäle, Influencer-Blogs als Primärquellen und jedes Werkzeug, das Vertrauen in einen unbekannten Dritten verlangt.

---

## 13. Checklisten

### Ersteinrichtung des Cryptophones
- [ ] Unterstütztes, empfohlenes Pixel (8. Generation oder neuer)
- [ ] Offizielles GrapheneOS über Web-Installer oder CLI-Anleitung installiert
- [ ] Bootloader **erst nach** erfolgreichem, verifiziertem Flash gesperrt
- [ ] Schalter zur OEM-Entsperrung auf dem letzten Einrichtungsbildschirm angehakt gelassen
- [ ] Verified-Boot-Schlüssel-Hash geprüft; Auditor genutzt, wenn möglich
- [ ] Updates installiert, Stable-Kanal
- [ ] Lange zufällige Passphrase oder lange zufällige PIN; Biometrie aus; PIN-Scrambling an
- [ ] Auto-Reboot gesetzt; USB-C eingeschränkt
- [ ] Bluetooth, NFC und Standort aus; WLAN aus, außer beim Aktualisieren oder Installieren von Apps
- [ ] Debugging aus
- [ ] Profile angelegt: Owner, sichere Kommunikation, optional Surfen
- [ ] App-Liste mit dokumentierten Zwecken angelegt

### Vor der ersten sensiblen Nutzung
- [ ] Nur frische Konten; keine privaten Daten verwendet
- [ ] Entscheidung über separate SIM/eSIM oder nur WLAN getroffen
- [ ] Sicherheitsnummern mit jedem Kontakt verifiziert
- [ ] Benachrichtigungen blenden Inhalte aus
- [ ] Netzwerk-Berechtigung für Offline-Apps blockiert
- [ ] Backup-Richtlinie festgelegt; Wiederherstellungscodes offline gelagert
- [ ] Private DNS aus, wenn ein VPN genutzt wird; VPN-Kill-Switch getestet

### Wöchentliche Wartung
- [ ] Updates installiert und neu gestartet
- [ ] Installierte Apps und Berechtigungen prüfen
- [ ] Ungenutzte Apps entfernen
- [ ] App-Liste mit den dokumentierten Zwecken abgleichen
- [ ] Backups und Wiederherstellung erneut testen (monatlich genügt)

### Vor Reisen
- [ ] Daten minimieren; unnötige Apps und Verläufe entfernen
- [ ] Aktualisieren und neu starten; kurzes Auto-Reboot setzen
- [ ] Reisegerät oder sauberes Profil entscheiden
- [ ] Über Biometrie entscheiden (aus) und Lockdown kennen
- [ ] Lokale Regeln zu Gerätedurchsuchung und erzwungener Entsperrung kennen **[Prüfen]**
- [ ] Wiederherstellungscodes offline und getrennt
- [ ] Eigenes Ladegerät und Kabel

### Nach der Installation einer App
- [ ] Quelle verifiziert (App Store, Entwicklersignatur oder als Ausweichlösung Accrescent/F-Droid)
- [ ] Zweck, Quelle und Berechtigungen dokumentiert
- [ ] Unnötige Berechtigungen verweigert; Contact Scopes und Storage Scopes nutzen
- [ ] Netzwerk blockieren, wenn sie offline funktioniert
- [ ] Sensoren-Berechtigung verweigert, wenn nicht nötig
- [ ] Im richtigen Profil abgelegt

### Vor der Verbindung mit öffentlichem WLAN
- [ ] Darf der Betreiber diesen Verkehr sehen?
- [ ] VPN-Entscheidung getroffen (und Private DNS aus, falls genutzt)
- [ ] Keine Anmeldungen in privaten Konten
- [ ] Captive Portal: keine echte Rufnummer und keine echte E-Mail eingeben
- [ ] Danach trennen und das Netzwerk vergessen

### Wenn das Gerät verloren geht oder gestohlen wird
- [ ] Wenn möglich ausschalten
- [ ] Vertraute Kontakte auf anderem Weg informieren
- [ ] Passwörter, 2FA-Seeds und Wiederherstellungscodes rotieren, die darauf lagen
- [ ] Sicherheitsnummern der Kontakte nach dem Ersatzgerät neu verifizieren
- [ ] Ein wiedergefundenes Gerät bis zur Neuinstallation als nicht vertrauenswürdig behandeln

### Bei Verdacht auf Identitätskompromittierung
- [ ] Die verknüpfte Identität nicht mehr nutzen
- [ ] Genau auflisten, was offengelegt wurde
- [ ] Benutzernamen, E-Mail und Nummern rotieren, wo möglich
- [ ] Kontakte über einen getrennten Kanal neu verifizieren
- [ ] Rat einholen, wenn die Kompromittierung rechtliche oder sicherheitsrelevante Folgen hat

---

## 14. Anti-Muster

| Behauptung | Realistische Fassung |
|---|---|
| „Mehr Privacy-Apps = sicherer“ | Jede App erhöht Vertrauensbedarf und Angriffsfläche. Die sicherste Liste ist die kürzeste |
| „VPN = anonym“ | Ein VPN verschiebt das Vertrauen zum Anbieter. EFF: „A VPN is not a tool for anonymity“ **[Extern]** |
| „Tor = für alles sicher“ | Tor schützt nur dafür konfigurierte Apps, und Anmeldung oder Preisgabe von Details hebelt es aus **[Extern]**. Das Projekt nennt die Sicherheit des Tor Browsers auf Android schwach **[Offiziell]** |
| „GrapheneOS = nicht verfolgbar“ | Netzbetreiber, WLAN-Betreiber und Dienste sehen weiterhin Ausschnitte deiner Aktivität |
| „Gelöschte Daten sind weg“ | Gelöschte Daten können in Backups, Caches und auf Geräten von Empfängern fortbestehen |
| „Ein verschlüsselter Messenger schützt vor einem kompromittierten Telefon“ | Ende-zu-Ende-Verschlüsselung schützt den Transport, nicht die Endpunkte |
| „Ein zweites Profil macht mich anonym“ | Profile teilen Hardware, SIM, IP und deine Gewohnheiten. **[Empfehlung]** |
| „Der Flugmodus macht ein Telefon ortungssicher“ | Er blockiert Standortdienste womöglich nicht, und Apps können gespeicherte Daten später senden; Ausschalten ist der stärkste verfügbare Schritt **[Extern]** |
| „Ein Faraday-Beutel löst OPSEC“ | Er blockiert Funk, solange er geschlossen ist; er behebt weder Konten noch Gewohnheiten noch ein kompromittiertes Gerät **[Empfehlung]** |
| „Ein Wegwerf-Telefon ist automatisch anonym“ | Die EFF nennt Bedingungen, damit ein Wegwerf-Telefon überhaupt wirkt (keine Wiederverwendung von SIM oder Gerät, nicht zusammen mit dem normalen Telefon mitgeführt, keine Anrufe an dieselben Personen) **[Extern]**; Standort- und Nummernkorrelation bleiben **[Empfehlung]** |

---

## 15. Unverzichtbar vs. optional, und Prüfstatus

### Unverzichtbar

- Offizielle Installation, **Bootloader nach verifiziertem Flash gesperrt**, OEM-Entsperrung deaktiviert
- Sofortige Updates, Stable-Kanal
- Langes Geheimnis, keine Biometrie, Auto-Reboot, USB-C eingeschränkt
- Winzige dokumentierte App-Liste; Netzwerk-Berechtigung für Offline-Apps blockiert
- Kein Google Play standardmäßig; separate SIM/eSIM oder nur WLAN; kein wiederverwendetes Identitätsmaterial
- Minimale, verschlüsselte, offline gelagerte Backups; Vorfallsplan

### Optional

- LTE-only-Modus, VPN, Tor Browser, Cryptomator, Organic Maps, Duress, Lockdown-Gewohnheit, ein Reisegerät

### Wogegen das Setup schützt

Gelegenheitsdiebstahl, viele Exploit-Klassen, bösartige Apps (durch die Sandbox), Raten, auch forensisch (durch das Secure Element und ein starkes Geheimnis), USB-Angriffe auf ein gesperrtes Telefon, ein feindliches lokales Netz und viel übermäßiges Sammeln durch Apps.

### Wogegen es nicht schützt

Alles in Abschnitt 1 Genannte sowie einen kompromittierten Endpunkt auf der Gegenseite, Verkehrsanalyse und deine eigenen Fehler.

### Prüfstatus

| Punkt | Status |
|---|---|
| GrapheneOS-Installation, Entsperren/Sperren, Löschvorgänge, Grenzen des Secure Elements, Auto-Reboot, USB-C-Modi, Scopes, Berechtigungen, Private-DNS- und VPN-Hinweise, LTE-only, eSIM, Vanadium-Verhalten, Accrescent und PDF-Betrachter im App-Repository, Einstellung zur Zwischenablage im Private Space, Fehlen einer Fernlöschung | Gegen die offiziellen Seiten geprüft **[Offiziell]** |
| EFF (einschließlich der Grenz-Checkliste von 2025), Tor Project, FPF (einschließlich Signalen bei ausgeschaltetem Gerät), RSF (Digital Security and Spyware Guide), Signal-Blog und Support-Artikel (einschließlich Backups, Sicherheitsnummern, Signal-PIN, Registrierungssperre und APK-Seite), HIBP, App-Lizenzen und -Quellen | Stichprobenartig gegen die genannten Primärquellen geprüft; Lockdown, der NFC-Pfad und der Memory-Tagging-Pfad stützen sich auf eine Sekundärquelle (privacygear.nl) **[Extern]** |
| Tor VPN (Haltung von GrapheneOS); genaue Menüpfade für Bluetooth-/WLAN-Auto-Aus und die Einstellung zur Zwischenablage im Private Space; Signal bei Accrescent; ob die eSIM-Aktivierung ein Konto, einen Ausweis oder eine Zahlung verlangt; IMEI-Sichtbarkeit eines Telefons ohne SIM; der Text der CBP-Direktive 3340-049B; Grenz- und Rechtsregeln außerhalb der USA | **[Prüfen]** |

*Mit der aktuellen offiziellen Dokumentation abgleichen.*
