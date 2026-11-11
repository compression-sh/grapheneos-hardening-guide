# GrapheneOS-Cryptophone-Leitfaden (Deutsch)

> **Was das ist:** eine maximal gehärtete GrapheneOS-Konfiguration mit nur einem Zweck, für sensible Kommunikation und Recherche. Sie ist strenger und einfacher als der Alltags-Leitfaden ([daily-driver-guide-de.md](daily-driver-guide-de.md)), den sie nicht ersetzt.
>
> **Was das nicht ist:** ein Weg zu Anonymität oder Unknackbarkeit. Sie verringert Angriffsfläche, Metadaten-Exposition, Identitätsverknüpfung und die Folgen einer Kompromittierung. Sie überwindet weder eine kompromittierte Lieferkette, einen kompromittierten Computer, manipulierte Hardware, körperlichen Zwang, eine vertrauenswürdige, aber kompromittierte App, einen entschlossenen Gegner mit Gerätezugriff, Metadaten von Netzbetreibern und Netzen noch menschliche Fehler.
>
> **Stand:** erstellt am 05.11.2026. GrapheneOS-Aussagen verweisen auf primäre GrapheneOS-Dokumentation oder verlinkten GrapheneOS-Projektquelltext. Genannte externe Quellen unterscheiden eigene Primärdokumentation/eigenen Code von sekundären Leitfäden. Offene Unsicherheiten stehen im Text; Menünamen ändern sich zwischen Versionen.
>
> **Tags:** [**Offiziell**](#tag-official) = GrapheneOS-Dokumentation, Projektquelltext oder klar zugeordnete Projektaussagen. [**Extern**](#tag-external) = eine genannte Nicht-GrapheneOS-Quelle (je nach Angabe primär oder sekundär). [**Empfehlung**](#tag-advice) = Einschätzung dieses Leitfadens. [**Prüfen**](#tag-verify) = unbestätigte Aussage; folge dem Link für Details und Einschränkungen.
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
- [12. Useful websites / Nützliche Webseiten](#12-useful-websites--nützliche-webseiten)
- [13. Checklisten](#13-checklisten)
- [14. Anti-Muster](#14-anti-muster)
- [15. Unverzichtbar vs. optional, und Prüfstatus](#15-unverzichtbar-vs-optional-und-prüfstatus)

[Tag-Legende](#tag-legend)

---

<a id="tag-legend"></a>
## Tag-Legende

Tags unterscheiden Herkunft (GrapheneOS oder extern) und Evidenzart (Primärdokumentation, Projektquelltext, datierte Projektaussage, Sekundärquelle oder unbestätigt). Quellen- und Empfehlungsmarkierungen verlinken die Legende; bei unbestätigten Aussagen verlinken Prüfmarkierungen das jeweilige offene Thema.

| Markierung | Bedeutung |
|---|---|
| <a id="tag-official"></a>**[Offiziell]** | GrapheneOS-Herkunft: Primärdokumentation, Projektquelltext oder klar zugeordnete Aussagen von Projektkonten oder Maintainern. Quellenart nennen, Aussagen datieren und Quelltextrevisionen möglichst festhalten. Ein Quellentag ist kein Praxistest und keine Garantie für aktuelles Verhalten. |
| <a id="tag-advice"></a>**[Empfehlung]** | Empfehlung dieses Leitfadens bzw. allgemeine Sicherheitspraxis; keine harte Tatsache und keine offizielle Aussage von GrapheneOS. |
| <a id="tag-external"></a>**[Extern]** | Nicht-GrapheneOS-Herkunft, keine Evidenzrangfolge: eigene Projektdokumentation/eigener Code ist primär für die eigenen Aussagen; ein Drittanbieter-Leitfaden ist sekundär. Quelle und Evidenzart nennen; Extern kann daher zugleich primär sein. |
| <a id="tag-verify"></a>**[Prüfen]** | Unbestätigte Aussage; folge dem Link für Details und Einschränkungen. |

**Offene Prüfthemen** (Kategorien, keine einzelnen Aussagen; Links führen zu den Gründen):

- [SIM-Registrierungsregeln und Neuvergabe virtueller Nummern](#verify-sim-rules)
- [Rechtliche, Grenz- und Zwangsentsperrungs-Regeln je Land](#verify-legal)
- [Versionsabhängige Pfade und ungeprüftes Build-Verhalten](#verify-menu-paths)
- [Sichtbarkeit der IMEI eines Geräts ohne SIM](#verify-imei)
- [eSIM-/Daten-eSIM-Aktivierung: Konto-, Ausweis- oder Zahlungspflichten](#verify-esim)

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
| Kompromittierte Lieferkette oder manipulierte Hardware | Hardware lässt sich über die Attestierung hinaus nicht prüfen; Auditor prüft Hardware, Firmware und Betriebssystem, aber nicht jede App [**Offiziell**](#tag-official) |
| Kompromittierter Computer zum Installieren oder Sichern | Ein Angreifer, der über einen kompromittierten Flash-Computer ein bösartiges Betriebssystem aufgespielt hat, lässt sich danach möglicherweise durch Verified Boot und Attestierung erkennen [**Empfehlung**](#tag-advice), sofern du den angezeigten Schlüssel-Hash auf einem getrennten, vertrauenswürdigen Gerät mit der offiziellen Liste vergleichst und Auditor von einem anderen Gerät aus gekoppelt hast; die Installationsseite auf einem kompromittierten Computer kann beliebige Inhalte zeigen. [**Empfehlung**](#tag-advice) Ein kompromittierter Computer, den du auch für sensible Arbeit nutzt, ist ein eigenes Problem |
| Körperlicher Zwang | Keine Softwareeinstellung ändert das |
| Schadsoftware über eine vertrauenswürdige, aber kompromittierte App | Die App-Sandbox begrenzt den Schaden, beseitigt aber nicht das Vertrauen in eine selbst gewählte App |
| Entschlossener Gegner mit Gerätezugriff | Erhöht den Aufwand, garantiert keinen Schutz, besonders im entsperrten Zustand oder nach dem ersten Entsperren |
| Metadaten von Netzbetreiber und Netz | Bei Mobilfunkverbindung sieht der Betreiber Teilnehmer-/Gerätekennungen, Funkzellen und Zeitpunkte. Der Flugmodus deaktiviert das Mobilfunkradio; andere Ortungs- und Korrelationsrisiken bleiben [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#cellular-tracking>) |
| Menschliche Fehler | Der häufigste Ausfall |

**Verbleibendes Risiko dieses Abschnitts:** Das Bedrohungsmodell selbst kann falsch sein. Prüfe es neu, sobald sich deine Rolle oder dein Aufenthaltsort ändert. Siehe das EFF-Modul „Your Security Plan“ (unter Nützliche Webseiten aufgeführt).

---

## 2. Strikte Geräterichtlinie

Das sind Regeln, keine Vorschläge. Jede Regel hat einen Grund; wenn du eine nicht einhalten kannst, wisse, worauf du verzichtest.

Ein Werkzeug schützt dich nicht, wenn du es falsch beschaffst oder einrichtest. Ein mit deiner echten Karte bezahltes VPN, eine mit deinem Ausweis aktivierte eSIM oder ein mit deiner echten Rufnummer registriertes Konto können die neue Identität wieder mit dir verknüpfen. Die Regeln unten behandeln nicht nur, welche Werkzeuge du nutzt, sondern auch, wie du sie beschaffst und einrichtest. [**Empfehlung**](#tag-advice)

1. **Ein Zweck.** Das Gerät dient sensibler Kommunikation und Recherche, sonst nichts.
2. **Keine App ohne dokumentierten Grund.** Führe eine kurze Liste: App, Quelle, Zweck, gewährte Berechtigungen, Datum. Entferne Apps, die du nicht mehr brauchst.
3. **Kein wiederverwendetes Identitätsmaterial.** Verwende keine privaten Konten, Benutzernamen, E-Mail-Adressen, Rufnummern, Profilbilder oder Wiederherstellungskontakte erneut. Lege neue Konten auf dem Gerät selbst an, mit einer neuen E-Mail-Adresse, die nicht an deine persönliche Wiederherstellungsadresse oder -nummer gebunden ist. Verlangt ein Dienst eine Rufnummer, kann diese Nummer die Konten miteinander und mit dir verknüpfen (siehe [„Eine separate Leitung einrichten“](#eine-separate-leitung-einrichten)). [**Empfehlung**](#tag-advice)
4. **Keine Kontakte mit echtem Namen**, außer sie sind operativ nötig, und dann nur der betreffende Kontakt (Contact Scopes, Abschnitt 4).
5. **Eigene SIM/eSIM.** Nutze nicht die SIM oder eSIM deines normalen Telefons, außer dein Bedrohungsmodell nimmt die Verknüpfung ausdrücklich in Kauf. Stecke keine SIM zwischen diesem und einem anderen Gerät um: Netzbetreiber können IMSI/IMEI-Paare protokollieren, sodass eine neue SIM im selben Telefon oder eine alte SIM in einem neuen Telefon Identitäten verknüpfen kann (siehe 9.1). Vermeide außerdem, dieses Gerät zusammen mit deinem privaten Telefon mitzuführen oder einzuschalten (gleiche Zeiten, gleiche Orte), SIM und Gerät gemeinsam oder mit rückverfolgbarer Zahlung zu kaufen und mit einem verknüpften Zahlungsmittel aufzuladen. Regeln zur SIM-Registrierung und Ausweispflicht sind länderspezifisch. Setze eine SIM-PIN. [**Empfehlung**](#tag-advice) <a id="verify-sim-rules"></a>[**Prüfen**](#verify-sim-rules) Die Regeln deines Landes.
6. **Keine privaten Zahlungsmittel** für alles, was zu dieser Identität gehört.
7. **Keine Biometrie**, wenn dein Bedrohungsmodell Zwang, Beschlagnahme oder erzwungenes Entsperren einschließt. Die EFF weist darauf hin, dass im von ihr beschriebenen Protestkontext weniger Schutz gegen erzwungenes Entsperren per Gesicht oder Fingerabdruck besteht als gegen erzwungene Herausgabe eines Passworts. [**Extern**](#tag-external) Ob und wo beides erzwungen werden kann, hängt von der Rechtsordnung ab; hole Rechtsrat ein. <a id="verify-legal"></a>[**Prüfen**](#verify-legal) GrapheneOS erlaubt nur 5 Fingerabdruckversuche insgesamt (Stock-Android erlaubt 20 mit Verzögerungen). [**Offiziell**](#tag-official)
8. **Starkes Geheimnis.** Nutze eine lange zufällige alphanumerische Passphrase oder eine lange zufällige PIN. Abwägung: Das Secure Element begrenzt Versuche auf insgesamt 20 mit steigenden Wartezeiten, was laut Projekt selbst bei einer zufälligen 6-stelligen PIN ein hohes Schutzniveau bietet. [**Offiziell**](#tag-official) Eine längere Passphrase (bis 128 Zeichen; Diceware wird unterstützt [**Offiziell**](#tag-official)) bleibt selbst gegen einen Angreifer stark, der die Versuchsbegrenzung des Secure Elements umgeht, kostet aber Tippaufwand und erhöht die Gefahr des Mitlesens. [**Empfehlung**](#tag-advice) **Empfohlen:** eine Diceware-Passphrase oder eine zufällige PIN mit 8 oder mehr Ziffern, wenn eine Passphrase unpraktikabel ist. [**Empfehlung**](#tag-advice)
9. **Auto-Reboot an** (Abschnitt 4).
10. **USB-C-Port eingeschränkt** (Abschnitt 4).
11. **Funkmodule standardmäßig aus:** Bluetooth, WLAN, NFC und Standort aus, solange sie nicht gebraucht werden.
12. **Updates sofort.**
13. **Backups minimal, verschlüsselt, offline** (Abschnitt 4).
14. **Nichts auf dem Gerät, dessen Verlust oder Offenlegung du nicht verkraften kannst.**

**Verbleibendes Risiko:** Die Richtlinie wirkt nur, wenn sie täglich befolgt wird. Eine einzige Wiederverwendung eines alten Benutzernamens oder einer Rufnummer kann Monate der Trennung zunichtemachen.

---

## 3. Geräteeinrichtung

### 3.1 Regeln für Hardware und Software

- **Nur unterstützte Pixel-Geräte**, GrapheneOS empfiehlt ausdrücklich Pixel 8 oder neuer, weil der Hersteller mindestens sieben Jahre Support ab dem Marktstart des jeweiligen Modells bietet und diese Geräte Hardware Memory Tagging unterstützen. Prüfe vor dem Kauf die aktuelle Liste unterstützter Geräte; dieses Minimum garantiert nicht sieben verbleibende Jahre zum Kaufzeitpunkt. [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#supported-devices>, <https://grapheneos.org/faq#recommended-devices>). Kaufe kein Pixel 6 oder 6 Pro mehr: Ihr OEM-Mindestsupport endete im Oktober 2026. Pixel-Varianten von Netzbetreibern erlauben das Entsperren des Bootloaders womöglich nicht; kaufe ein freies Gerät aus dem Handel. Das Aktivieren der OEM-Entsperrung kann bei manchen Varianten Internetzugang erfordern. [**Offiziell**](#tag-official)
- **Nur offizielles GrapheneOS**, installiert mit dem offiziellen **Web-Installer** (<https://grapheneos.org/install/web>) oder der **CLI-Anleitung** (<https://grapheneos.org/install/cli>). Folge der gewählten Anleitung buchstabengetreu, ohne Schritte auszulassen, umzuordnen oder hinzuzufügen. [**Offiziell**](#tag-official)
- **Verboten:** Drittanbieter-Recovery, Custom-ROMs, Root, Magisk, Xposed, LSPosed, veränderte Systemkomponenten, „Privacy-ROMs“ und Verschleierungswerkzeuge. Root oder Systemänderungen können die Integrität des Betriebssystems oder Sandbox-Grenzen untergraben [**Empfehlung**](#tag-advice). Gewöhnliche App-Stores deaktivieren nicht allein durch ihre Installation Verified Boot oder die App-Sandbox; Sandboxed Google Play läuft auf GrapheneOS als reguläre Apps ohne Sonderrechte [**Offiziell**](#tag-official) (<https://grapheneos.org/features#sandboxed-google-play>; <https://grapheneos.org/usage#sandboxed-google-play>). APK-Quellen außerhalb der erlaubten Liste bleiben wegen Lieferketten- und Update-Risiken verboten, nicht weil jeder Store Betriebssystemschutz entfernt [**Empfehlung**](#tag-advice).
- Kaufe und installiere das Gerät möglichst selbst. Das Projekt empfiehlt keine Firmen, die vorinstallierte Geräte verkaufen. [**Offiziell**](#tag-official) Kauftricks machen das Gerät nicht anonym; Händler können Videoaufnahmen, IMEI-Daten und Zahlungsdaten speichern. [**Empfehlung**](#tag-advice)

### 3.2 Ablauf der Installation

> ⚠️ **Das Entsperren und das Sperren des Bootloaders löschen jeweils alle Daten.** Sichere vorher alles, was auf dem Gerät liegt; ein gebrauchtes Gerät wird gelöscht, die Installation löscht es.

1. Starte das Stock-Android, aktualisiere es, aktiviere die Entwickleroptionen (**Einstellungen → Über das Telefon → Build-Nummer**) und aktiviere unter **Einstellungen → System → Entwickleroptionen** die **OEM-Entsperrung**. Beim Pixel 6a zuerst per OTA auf Juni 2022 oder neuer aktualisieren und auf Werkseinstellungen zurücksetzen. [**Offiziell**](#tag-official)
2. Starte in das Bootloader-Interface: Halte beim Start die **Leiser-Taste** gedrückt, bis das rote Dreieck und „Fastboot Mode“ erscheinen. Wähle „Start“ nicht aus. [**Offiziell**](#tag-official)
3. **Entsperre** den Bootloader (Schaltfläche im Web-Installer oder `fastboot flashing unlock`) und bestätige am Gerät. Das löscht das Gerät. [**Offiziell**](#tag-official)
4. **Flashen** (Web-Installer **Flash release**, oder CLI: Image-Signatur mit `ssh-keygen -Y verify` anhand von `allowed_signers` prüfen, entpacken, `flash-all` ausführen). Bediene das Gerät nicht, bis es fertig ist. [**Offiziell**](#tag-official)
5. **Sperre den Bootloader erst, nachdem der offizielle Installer/Flasher erfolgreiches Flashen gemeldet hat (bei der CLI zusätzlich nach der Signaturprüfung in Schritt 4).** Sperre ihn dann (Schaltfläche im Web-Installer oder `fastboot flashing lock`) und bestätige am Gerät. **Das Sperren löscht erneut alle Daten.** [**Offiziell**](#tag-official)

> ⚠️ **Schlagen Verifizierung oder Flashen fehl oder sind sie unvollständig, sperre den Bootloader nicht.** Lass ihn entsperrt und flashe erneut; das Gerät startet womöglich nicht, bis ein verifiziertes GrapheneOS-Image erfolgreich geflasht wurde. Ein Sperren mit fehlendem, unvollständigem oder ungültigem Betriebssystem kann das Gerät unwiederbringlich machen, weil die OEM-Entsperrung nur aus einem startenden Betriebssystem wieder aktiviert werden kann. Lade das Image erneut herunter, verifiziere es erneut, wiederhole die Installation oder frage in den offiziellen GrapheneOS-Supportkanälen nach. [**Empfehlung**](#tag-advice)

6. Lass bei der Ersteinrichtung den Schalter **OEM-Entsperrung deaktivieren** auf dem letzten Bildschirm **angehakt** (Standard). [**Offiziell**](#tag-official)
7. **Installation überprüfen.** Erwarte den gelben Startbildschirm-Hinweis; vergleiche den angezeigten Verified-Boot-Schlüssel-Hash mit der Liste auf der Installationsseite. Bei der Einrichtung darf keine Warnung „Bootloader nicht gesperrt“ erscheinen. Erscheint sie, ist die Installation unvollständig; sperre jetzt nur, wenn das ursprüngliche Flashen und Verifizieren erfolgreich abgeschlossen wurde, andernfalls nicht sperren und erneut flashen (siehe die Warnung oben). [**Offiziell**](#tag-official) Vergleiche zuerst den Schlüssel-Hash (auf einem getrennten, vertrauenswürdigen Gerät mit der offiziellen Liste), koppele dann **Auditor** von einem zweiten Android-Gerät aus und nutze erst danach das Gerät. Der Vergleich erfolgt nach dem Sperren und ist die abschließende Prüfung. Koppele Auditor für Kontinuität möglichst früh nach der Installation, bevor das Gerät deine Kontrolle verlässt; diese Reihenfolge ist eine Autorenempfehlung [**Empfehlung**](#tag-advice). Auch eine spätere Erstprüfung prüft unterstützte Eigenschaften von Hardware, Firmware und Betriebssystem, hat aber keine vorherige Kopplungs-Baseline und behält die Grenzen des anfänglichen Vertrauensaufbaus: Geleakte Attestierungsschlüssel oder ein geeignetes Proxy-Gerät können die Erstprüfung umgehen [**Offiziell**](#tag-official) (<https://grapheneos.org/install/web#verifying-installation>; <https://attestation.app/about>).
8. **Sofort aktualisieren** und beim Stable-Kanal bleiben. [**Offiziell**](#tag-official)
9. USB-Debugging und drahtloses Debugging ausschalten. [**Empfehlung**](#tag-advice)

**Verbleibendes Risiko:** Die Installationsseite und dein Computer sind Komponenten, denen du vertrauen musst. Die CLI-Methode mit Signaturprüfung verringert das Vertrauen in die Web-Infrastruktur des Projekts, nicht aber in deinen Computer oder die Hardware. Nutze einen Computer, dem du vertraust und den du nicht für die sensible Arbeit selbst verwendest.

---

## 4. Härtungseinstellungen

Menünamen und Build-Verhalten ändern sich zwischen Versionen. <a id="verify-menu-paths"></a>[**Prüfen**](#verify-menu-paths) Diese Kategorie umfasst versionsabhängige Pfade und ungeprüftes Verhalten: NFC-Auto-Aus-Verfügbarkeit, Captive-Portal-Verhalten bei VPN-Blockierung und, soweit behandelt, Sentry-Kompatibilität, Tor-Android-Fenster und Accrescent-Lizenzen. Die konkrete Unsicherheit steht neben dem jeweiligen Marker.

Für jede Einstellung: der empfohlene Cryptophone-Wert, warum, wogegen sie schützt, wogegen sie **nicht** schützt, und die Komforteinbuße.

### 4.1 Gerätezugang

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Bildschirmsperre** (Einstellungen → Sicherheit & Datenschutz → Gerät entsperren) [**Offiziell**](#tag-official) | Lange zufällige Passphrase (Diceware) oder zufällige PIN mit 8+ Ziffern; keine Biometrie | Starker praktischer Schutz gegen Raten; beseitigt den Angriffsweg erzwungener Biometrie | Raten, auch forensisch; Mitlesen mit Scrambling | Zwang, ein in deiner Hand entsperrtes Gerät, Schadsoftware im entsperrten Zustand | Hoch: häufiges Eintippen des Geheimnisses |
| **Sperrzeit** | Kurz, z. B. 30-60 s bei einer Passphrase oder 15-30 s bei einer kurzen PIN; wähle eine, die du durchhältst. Sofort sperren per Ein-/Aus-Taste | Verkürzt das entsperrte Zeitfenster | Gelegenheitszugriff auf ein unbeaufsichtigtes Telefon | Ein Angreifer, der es im entsperrten Zustand greift | Häufiges Neu-Entsperren; eine so kurze Zeit, dass du dein Geheimnis schwächst, ist kontraproduktiv |
| **PIN-Scrambling** | An, wenn du eine PIN nutzt | Erschwert das Beobachten der PIN; gilt für Sperrbildschirm und SIM-PIN [**Offiziell**](#tag-official) | Mitlesen, Fingerspuren | Kameras, die das Drücken auf der durchmischten Tastatur sehen | Langsamere Eingabe |
| **Biometrie** | Aus | Siehe Richtlinie Regel 7 | Erzwungene Entsperrung per Fingerabdruck oder Gesicht | Erzwungene Herausgabe der Passphrase (rechtsordnungsabhängig) | Weniger Komfort |
| **Lockdown** (Ein-/Aus-Menü) | Kennen: Drücke Ein-/Aus-Taste + Lauter und tippe dann auf Lockdown. Android kann Lockdown auch im Ein-/Aus-Menü anzeigen, nachdem du Einstellungen → Display → Erweitert → Sperrbildschirm-Anzeige → Lockdown-Option anzeigen aktiviert hast. Bis zum nächsten Entsperren deaktiviert es Benachrichtigungen auf dem Sperrbildschirm, die Entsperrung per Fingerabdruck/Gesicht und Extend Unlock [**Extern**](#tag-external) (Google Android-Hilfe: <https://support.google.com/android/answer/9075927?hl=en>). Lockdown ist nicht dasselbe wie Ausschalten oder die Rückkehr des Geräts in den BFU-Zustand. Bei ausgeschalteter Biometrie bringt es wenig; die Handlung vor Kontrollen ist das Ausschalten [**Empfehlung**](#tag-advice) | Schaltet biometrische und Smart-Entsperrung schnell ab | Kurzfristige biometrische Entsperrung | Alles andere | Ein zusätzlicher Schritt |
| **Auto-Reboot** (Exploit-Schutz) | 4 Stunden auf Reisen, 8-12 Stunden für ein täglich mitgeführtes Telefon [**Empfehlung**](#tag-advice); offizieller Standard ist 18 h, Bereich 10 Min. bis 72 h [**Offiziell**](#tag-official) | Jedes Sperren startet den Countdown; erfolgreiches Entsperren eines beliebigen Profils hebt ihn auf. Bei Ablauf startet das gesperrte Gerät neu und versetzt Daten in den Ruhezustand (BFU, Before First Unlock; siehe Verhaltens-OPSEC). Keine wiederholten Neustarts in BFU [**Offiziell**](#tag-official) (<https://grapheneos.org/features#auto-reboot>) | Forensische Extraktion eines Geräts im Zustand nach dem ersten Entsperren | Beschlagnahme während der Nutzung, ein schwaches Geheimnis oder ein kompromittiertes Secure Element | Nach jedem Neustart muss zuerst das Owner-Profil, dann das Kommunikationsprofil entsperrt werden; bis dahin kommen keine Nachrichten oder Benachrichtigungen an. Wähle ein Intervall, das du durchhältst |
| **USB-C-Port** (Exploit-Schutz [**Offiziell**](#tag-official); die Usage-Seite schreibt für das übergeordnete Menü auch „Security & privacy“) | Mindestens Nur Laden, wenn gesperrt beibehalten. Wenn nie USB-Daten nötig sind, je nach benötigter Nutzbarkeit Nur Laden oder Aus wählen [**Empfehlung**](#tag-advice). Aus deaktiviert bei gestartetem Betriebssystem neben Daten auch das Laden. Die Funktion gilt nicht im ausgeschalteten Zustand, im Firmware-Fastboot oder in den Modi Charging, Recovery und Fastbootd [**Offiziell**](#tag-official) (<https://grapheneos.org/features#usb-c-port-and-pogo-pins-control>). | Blockiert neue USB-Verbindungen nach dem Sperren | USB-Angriffe auf ein gesperrtes Telefon | Angriffe im entsperrten Zustand oder über andere Funkwege | Keine Dateiübertragung im gesperrten Zustand |
| **Memory Tagging (MTE)** (Exploit-Schutz; Pixel 8 und neuer) | Auf unterstützter Pixel-8-Hardware oder neuer unter Einstellungen → Sicherheit & Datenschutz → Exploit-Schutz „Memory tagging → Enable by default“ setzen [**Offiziell**](#tag-official) (Settings-Quelltext von GrapheneOS: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/values/strings_app_exploit_protection.xml>). GrapheneOS nutzt Memory Tagging bereits für kompatible Basissystem-Komponenten und bekannte kompatible Apps; dies aktiviert es für weitere Drittanbieter-Apps. Inkompatible Apps können abstürzen, nutze also eine App-Ausnahme nur bei Bedarf. Laut GrapheneOS-FAQ wird die Mullvad-App auf GrapheneOS mit Hardware-Memory-Tagging getestet; bei der offiziellen WireGuard-App werden mit aktiviertem MTE ungültige Speicherzugriffe erkannt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Bei standardmäßig aktiviertem MTE Mullvad bevorzugen. Wenn WireGuard zwingend nötig ist, die aktuelle Kompatibilität prüfen und nur bei Bedarf eine App-spezifische Ausnahme verwenden; MTE niemals global deaktivieren [**Empfehlung**](#tag-advice). | GrapheneOS nutzt Hardware-Memory-Tagging bereits für das Basissystem und bekannte kompatible Apps und bietet die Option, es für alle Apps zu verwenden [**Offiziell**](#tag-official) (grapheneos.org/features#exploit-mitigations) | Ausnutzung von Speicherfehlern in Apps (Pufferüberläufe, Use-after-free) | Logikfehler, ein kompromittiertes System oder Hardware und alles, was kein Speicherfehler ist | Schlecht programmierte Apps können abstürzen |
| **Duress-PIN/-Passwort** (Gerät entsperren, Owner-Profil) [**Offiziell**](#tag-official) | Optional; bewusst entscheiden (Abschnitt 10). Erfordert PIN und Passwort; die Eingabe der echten Zugangsdaten hat Vorrang, dann erfolgt kein Löschen [**Offiziell**](#tag-official) | Löscht Gerät und eSIMs unwiderruflich bei Eingabe; keine allgemeine Schutzmaßnahme gegen Beschlagnahme | Einen Gegner, der Zugangsdaten in das laufende Gerät eingibt | Extraktion ohne Eingabe der Zugangsdaten, ein bereits erstelltes Datenabbild oder rechtliche Folgen | Risiko eines versehentlichen, unumkehrbaren Löschens |

### 4.2 Funkmodule, Standort und Sensoren

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Bluetooth** | Aus; nur für ein bestimmtes Zubehör einschalten; die Zeitüberschreitung „Turn off Bluetooth automatically“ nutzen (Bezeichnung aus dem Settings-Quelltext von GrapheneOS) [**Offiziell**](#tag-official); Pfad: Einstellungen → Sicherheit & Datenschutz → Exploit-Schutz (manche GrapheneOS-Abschnitte kürzen das übergeordnete Menü zu „Sicherheit“ ab) enthält „Turn off Bluetooth automatically“ [**Offiziell**](#tag-official) (Settings-Quelltext von GrapheneOS: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/exploit_protection_settings.xml>) | Verringert Angriffsfläche in der Nähe und Tracking über Geräte in der Umgebung | Angriffe aus der Nähe, passives Tracking durch Bluetooth-Beacons | Einen Beacon, der ein Gerät sieht, bei dem Bluetooth an blieb | Standardmäßig kein drahtloses Zubehör |
| **WLAN** | Aus, solange nicht genutzt; MAC-Randomisierung pro Verbindung bleibt an (Standard) [**Offiziell**](#tag-official); keine versteckten Netzwerke verbinden, sie verringern die Privatsphäre [**Offiziell**](#tag-official) | Begrenzt passives Tracking und Gefahr durch Fremd-Hotspots | Passives Tracking per MAC, Fremd-Hotspots | Den WLAN-Betreiber, der Verkehr und IP sieht | Manuelles Umschalten |
| **WLAN- und Bluetooth-Scanning** (Einstellungen → Standort → Standortdienste) [**Offiziell**](#tag-official) | Aus (Standard) | Scanning läuft auch bei „ausgeschalteten“ Funkmodulen | Funkmodule, die im Hintergrund aktiv bleiben | n/a | Langsamere Ortung |
| **Standort** | Standardmäßig aus; „nur bei Nutzung“ für einen konkreten Bedarf | Verringert die Standortspur | Apps und SDKs, die Standort sammeln | Netz-Standort durch den Netzbetreiber | Karten brauchen manuelles Einschalten |
| **NFC** | Aus (Einstellungen → Verbundene Geräte → Verbindungseinstellungen → NFC [**Offiziell**](#tag-official) (<https://grapheneos.org/releases#2026050400>); die Verfügbarkeit von NFC-Auto-Aus ist gesondert [**Prüfen**](#verify-menu-paths)) | Entfernt einen Eingang aus der Nähe | Angriffe aus der Nähe | n/a | Kein kontaktloses Bezahlen (hier ohnehin unerwünscht) |
| **Mobilfunk-Typ** (Einstellungen → Netzwerk & Internet → SIMs → SIM → Bevorzugter Netzwerktyp) [**Offiziell**](#tag-official) | Nur LTE, wenn dein Netzbetreiber damit zuverlässig funktioniert | Schaltet 2G-, 3G- und 5G-Codepfade ab und verringert die Angriffsfläche für Remote-Exploits [**Offiziell**](#tag-official) | Remote-Ausnutzung über alten Funkmodul-Code | Abhören von Anrufen und SMS, Metadaten des Netzbetreibers, Ortung durch den Netzbetreiber. Laut Projekt keine Vertraulichkeitsfunktion [**Offiziell**](#tag-official) | Kein Rückfall bei schlechter Abdeckung; herkömmliche Sprachanrufe funktionieren nur mit VoLTE oder WLAN-Telefonie [**Offiziell**](#tag-official) |
| **SUPL** (Einstellungen → Standort) [**Offiziell**](#tag-official) | GrapheneOS-Proxy beibehalten oder Aus | Vermeidet den Standard-SUPL-Server des Netzbetreibers | Preisgabe eines groben Standorts an den SUPL-Server des Netzbetreibers | Funkzellen-Ortung durch den Netzbetreiber | Langsamerer GNSS-Fix bei Aus |
| **eSIM-Unterstützung** (Einstellungen → Netzwerk & Internet) [**Offiziell**](#tag-official) | Aus, solange du keine eSIM nutzt | Standardmäßig deaktiviert; die Verwaltung von eSIMs braucht proprietäre Google-Funktionen, aber nicht Google Play | n/a | Eine eSIM hat eine eigene Kennung, und die Aktivierung kann ein Konto oder einen Ausweis verlangen | Zusätzlicher Schritt zum Einschalten bei Bedarf |
| **Kamera und Mikrofon** | Standardmäßig verweigern; pro Nutzung gewähren („nur diesmal“ / „bei Nutzung“) | Begrenzt Missbrauch von Kamera und Mikrofon | Heimliche Aufnahme durch Apps | Ein kompromittiertes Betriebssystem oder Hardware | Rückfrage jedes Mal |
| **Sensoren-Berechtigung** (Einstellungen → Sicherheit & Datenschutz → Weitere Sicherheit & Datenschutz) [**Offiziell**](#tag-official) | Für neu installierte Apps standardmäßig deaktivieren | Liefert Nullwerte für Beschleunigungssensor, Gyroskop, Kompass und weitere | Sensorbasiertes Fingerprinting und Seitenkanäle | Andere verdeckte Kanäle | Einzelne Apps verhalten sich womöglich merkwürdig |

### 4.3 Berechtigungen und Daten

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **App-Berechtigungen** | Das Minimum gewähren; nach jeder Installation prüfen | Kleinerer Schadensradius | Übermäßiges Sammeln durch Apps | Eine vertrauenswürdige App, die gewährte Daten missbraucht | Gelegentliche Fehlfunktionen |
| **Netzwerk-Berechtigung** [**Offiziell**](#tag-official) | Für jede App blockieren, die offline funktioniert (Notizen, PDF, Authenticator, Passwortmanager) | Die App sieht „Netz aus“; blockiert auch Localhost-Nutzung zwischen Profilen | Telemetrie und Datenabfluss offline arbeitender Werkzeuge | Daten, die über einen anderen erlaubten Weg abfließen | Synchronisierende Apps synchronisieren nicht mehr |
| **Contact Scopes** [**Offiziell**](#tag-official) | Für jede App an, die Kontakte verlangt; nur den einen Kontakt, die Gruppe oder die nötigen Daten freigeben; Schreibzugriff ist blockiert | Die App sieht standardmäßig eine leere Kontaktliste | Hochladen des gesamten Adressbuchs | Einen Kontakt, den du freigegeben hast | Manuelles Freigeben |
| **Storage Scopes** [**Offiziell**](#tag-official) | Für jede App an, die Speicherzugriff verlangt; nur nötige Dateien oder Ordner freigeben | Begrenzt die Dateiexposition | Durchsuchen des gesamten Speichers | Dateien, die du freigegeben hast | Manuelles Freigeben |
| **Zwischenablage** | Bei der Standard-Zwischenablage die aktuell fokussierte App und die konfigurierte Standardtastatur berücksichtigen; Geheimnisse möglichst nicht kopieren; wo möglich die Autofill-Funktion des Passwortmanagers nutzen. Das Sperren der Zwischenablage zum/vom übergeordneten Profil gibt es für den Private Space in neueren Versionen (Release-Notes 05/2025) [**Offiziell**](#tag-official): Einstellungen → Sicherheit & Datenschutz → Private Space → System → Cross-profile shared clipboard → Disallowed (Settings-Quelltext von GrapheneOS: <https://github.com/GrapheneOS/platform_packages_apps_Settings/blob/b6ef57550748eb6f54ebab4914c6e630a20fd07a/res/xml/private_space_settings.xml>). Der Private Space ist nicht Teil des Profilmodells dieses Leitfadens. Kopiere Geheimnisse nicht in die Standard-Zwischenablage. Nach den Standardregeln können nur die aktuell fokussierte App und die konfigurierte Standardtastatur Zwischenablage-Inhalte lesen [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#clipboard>). Secure Paste ergänzt eine App-bezogene Beschränkung mit globalem Standard und App-spezifischen Ausnahmen: Ist sie für eine App aktiviert, blockiert sie das Lesen fremder Inhalte; von der App selbst gesetzte Inhalte bleiben lesbar. Prüfe die Kompatibilität pro App [**Offiziell**](#tag-official) (<https://grapheneos.org/features#secure-paste>) | Lesezugriff für Fokus-App/Standardtastatur; Secure Paste beschränkt zusätzlich fremde Inhalte | Preisgabe von Geheimnissen über die Zwischenablage | Keylogger oder eine kompromittierte Tastatur | Neu tippen |
| **Benachrichtigungen** | Sensible Inhalte auf dem Sperrbildschirm ausblenden; keine Nachrichtenvorschau | Ein gesperrtes Telefon soll nichts verraten | Mitlesen, Blick auf ein gesperrtes Telefon | Benachrichtigungen, die Text anzeigen dürfen | Weniger auf einen Blick |
| **Screenshots** | Nie für sensibles Material; Screenshots werden gespeichert und womöglich gesichert | Screenshots bleiben bestehen und wandern weiter | Lokale Rückstände | Einen Empfänger, der seinen eigenen Bildschirm fotografiert | Gewohnheitsänderung |

### 4.4 Browser, DNS, VPN, Updates, Backups, Verlust

| Einstellung | Empfohlener Wert | Warum | Schützt vor | Schützt nicht vor | Komforteinbuße |
|---|---|---|---|---|---|
| **Browser** | **Vanadium** im isolierten Browsing-Profil. JavaScript-JIT ist standardmäßig aus, mit Umschalter pro Website; Erweiterungen sind bewusst nicht geplant [**Offiziell**](#tag-official). So lassen. [**Empfehlung**](#tag-advice) | Laut Projekt die stärkste Sandbox unter gängigen mobilen Browsern [**Offiziell**](#tag-official); weniger Plugins bedeuten weniger Fingerprinting | Viele Browser-Exploits, erweiterungsbasiertes Tracking | IP-basiertes Tracking, Anmeldung in Konten, Fingerprinting durch Websites | Manche Seiten gehen mit JIT aus kaputt |
| **Private DNS** (Einstellungen → Netzwerk & Internet → Private DNS) | **Automatisch** (Standard), wenn kein VPN genutzt wird. Private DNS ist global. Keinen Private-DNS-Hostnamen zusammen mit einem VPN konfigurieren; sobald irgendein Zweitprofil ein VPN nutzt, Private DNS global vollständig auf Aus stellen, wie GrapheneOS ausdrücklich empfiehlt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Dieser Leitfaden empfiehlt zusätzlich als strengere Autorenregel Aus bei jedem VPN [**Empfehlung**](#tag-advice). | Automatisch liefert opportunistisches DNS-over-TLS; ein Hostname erzwingt authentifiziertes DoT. Private DNS ist jedoch global; VPN-Einstellungen gelten jedoch pro Profil, daher wirken beide schlecht zusammen; die Version 07/2025 behob zwei VPN-Lecks [**Offiziell**](#tag-official) | Einen passiven lokalen Mithörer (Automatik-Modus); aktive Angreifer können den Rückfall erzwingen [**Offiziell**](#tag-official) | Domains, die über TLS-SNI durchsickern, Ziel-IPs, den DNS-Anbieter, der deine Anfragen sieht. Kein Ersatz für Tor oder ein VPN [**Offiziell**](#tag-official) | Keine im Automatik-Modus |
| **VPN** | Nur nutzen, wenn du die adressierte Bedrohung benennen kannst (nicht vertrauenswürdiges lokales Netz oder Provider). Nutze die offizielle Mullvad- oder WireGuard-App, wie es die GrapheneOS-FAQ empfiehlt [**Offiziell**](#tag-official). **Always-on-VPN** und **Verbindungen ohne VPN blockieren** aktivieren. Wähle und bezahle das VPN so, dass es nicht mit deiner echten Identität verknüpft wird: Ein mit deiner persönlichen Karte bezahltes oder mit deiner Haupt-E-Mail-Adresse registriertes Konto kann das VPN an dich binden. [**Empfehlung**](#tag-advice) Laut GrapheneOS-FAQ wird die Mullvad-App auf GrapheneOS mit Hardware-Memory-Tagging getestet; bei der offiziellen WireGuard-App werden mit aktiviertem MTE ungültige Speicherzugriffe erkannt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Bei standardmäßig aktiviertem MTE Mullvad bevorzugen. Wenn WireGuard zwingend nötig ist, die aktuelle Kompatibilität prüfen und nur bei Bedarf eine App-spezifische Ausnahme verwenden; MTE niemals global deaktivieren [**Empfehlung**](#tag-advice). | Verbirgt Ziele und Inhalte vor lokalem Netz und Provider; verbirgt deine IP vor Websites | Einen feindlichen WLAN-Betreiber oder Provider | Den VPN-Anbieter, der den Verkehr sieht (Vertrauen verschiebt sich), Konten, in die du dich einloggst, Funkzellen-Ortung, Anrufe und SMS. EFF: „A VPN is not a tool for anonymity“ [**Extern**](#tag-external) | Einrichtung und Konfiguration pro Profil |
| **Updates** | System-Updater an, **Stable**-Kanal, zum Abschluss neu starten [**Offiziell**](#tag-official) | Sicherheitskorrekturen gehören zu den wertvollsten Schutzmaßnahmen | Bekannte Schwachstellen | Unbekannte (Zero-Day-)Schwachstellen | Gelegentliche Neustarts |
| **Backups** | **Standardmäßig kein vollständiges Geräte-Backup.** Nur sichern: eine verschlüsselte Kopie der Passwortmanager-Datenbank, einen verschlüsselten Authenticator-Export und Wiederherstellungscodes offline, getrennt vom Gerät | Backups sind eine zusätzliche Kopie, die ein Gegner beschlagnahmen kann | Verlust des Geräts = Verlust des Zugangs | Ein kompromittiertes Sicherungsmedium | Neuaufbau nach Verlust |
| **Seedvault** (eingebautes Backup) | Für das sensible Profil nicht nutzen, sofern nicht nötig. Falls doch, ein lokal gespeichertes verschlüsseltes Ziel. Das Projekt plant einen Ersatz, weil Seedvault upstream von einer Gruppe übernommen wurde, die seine Ziele nicht teilt [**Offiziell**](#tag-official) | Vermeidet eine Cloud-Kopie | Cloud-Exposition von Gerätedaten | Ein beschlagnahmtes Backup-Laufwerk | n/a |
| **Geräteverlust/Diebstahl** | Gehe davon aus, dass es bei einem Gegner liegt, bis das Gegenteil bewiesen ist (Abschnitt 11). In den offiziellen Features-, Usage- und FAQ-Seiten ist keine Fernlösch-Funktion beschrieben [**Offiziell**](#tag-official); Duress wirkt nur lokal | Auf den schlimmsten Fall planen | n/a | n/a | n/a |

**Verbleibende Risiken dieses Abschnitts:** Jede Einstellung ist eine Abmilderung, keine Garantie. Einstellungen, die auf dem Secure Element oder dem Betriebssystem selbst beruhen, versagen, wenn eines davon kompromittiert ist. Ein strenges Setup, das du aus Bequemlichkeit umgehst, ist schlechter als ein etwas lockereres, das du einhältst.

---

### 4.5 Anti-Forensik-Apps: Wasted, Sentry und warum GrapheneOS Duress besser ist

Dieser Abschnitt ergänzt die Duress-Zeile in Abschnitt 4.1. Er ersetzt sie nicht.

**Was sie sind.**

| App | Was sie tut | Quelle |
|---|---|---|
| **Wasted** | Sperrt das Gerät und löscht es optional (Zurücksetzen auf Werkseinstellungen) bei einem Auslöser: PanicKit, Kachel oder Verknüpfung, eine Nachricht mit einem geheimen Code, ein Gerät, das eine festgelegte Zeit nicht entsperrt wurde, eine USB-Datenverbindung im gesperrten Zustand, der Start einer gefälschten Messenger-App oder ein Duress-Passwort, das in der Begleit-App „Duress“ eingegeben wird [**Extern**](#tag-external) | Wasted-README, <https://github.com/x13a/Wasted>; F-Droid, <https://f-droid.org/packages/me.lucky.wasted/> |
| **Sentry** | Eine „winzige App zur Durchsetzung von Sicherheitsrichtlinien“: begrenzt fehlgeschlagene Passworteingaben, kann USB-Datenverbindungen und den abgesicherten Start deaktivieren und meldet fehlgeschlagene Versuche. Dasselbe Entwicklerkonto (x13a); das Wasted-README verweist dafür auf „Basissicherheit“ [**Extern**](#tag-external) | Sentry-README, <https://github.com/x13a/Sentry> |

**Voraussetzungen und Grenzen.** Wasted nutzt Device Admin zum Sperren oder Zurücksetzen auf Werkseinstellungen, kann stattdessen einen Trigger-Broadcast senden und funktioniert mit Einschränkungen in einem Arbeitsprofil, indem es dieses Profil statt des ganzen Geräts löscht. Die optionale Begleit-App „Duress“ ist von GrapheneOS Duress getrennt. Sentrys README nennt Android 12, USB HAL 1.3 und Device Owner als Voraussetzungen für USB-Daten, keine Beschränkung nur auf Android 12. Die heutige Kompatibilität ist ungeprüft [**Prüfen**](#verify-menu-paths); das Deaktivieren des abgesicherten Starts erfordert Device Owner. Beide READMEs nennen Einschränkungen im abgesicherten Modus und geplante Architekturänderungen [**Extern**](#tag-external) (<https://raw.githubusercontent.com/x13a/Wasted/main/README.md>, <https://github.com/x13a/Sentry/blob/e4f80a737129ac9a2e42b9f988c132fd24caa40d/README.md>).

Beide sind Open Source unter GPL-3 [**Extern**](#tag-external). Sie wurden in der GrapheneOS-Community viel diskutiert; diese Beliebtheit ist kein Beleg dafür, dass sie heute sicher nutzbar sind [**Empfehlung**](#tag-advice).

**Warum sie nicht empfohlen werden.**

| Grund | Detail | Einschränkung |
|---|---|---|
| Von Forensik-Firmen ausgenutzt | GrapheneOS führte die Ausnutzung in einer Aussage vom Juni 2024 auf unterbrechbares Löschen über Device Admin zurück: Forensik-Firmen haben Apps wie Wasted und Sentry gegen Nutzer ausgenutzt, und GrapheneOS hat das im Rahmen seiner Duress-PIN/-Passwort-Funktion behoben und gemeldet, sodass Google es in ganz Android behoben hat; es wurde für diese Prüfung nicht unabhängig reproduziert (<https://x.com/GrapheneOS/status/1801294115407106186>; ein Social-Media-Beitrag, keine Dokumentation auf grapheneos.org) [**Offiziell**](#tag-official) | Die übrigen Gründe gelten auch ohne diese Aussage |
| Zuverlässigkeit | Ein Forennutzer berichtet, dass sie seit etwa Android 15 nicht mehr zuverlässig sind, besonders über längere Zeiträume, weil die Timer nicht immer automatisch starten, da sie auf Foreground Services beruhen (<https://discuss.grapheneos.org/d/28627-wasted-sentry>; ein Community-Bericht, keine offizielle Aussage und kein Test) [**Extern**](#tag-external) [**Empfehlung**](#tag-advice). Der Android-15-Zuverlässigkeitsbefund ist ein einzelner Community-Bericht; keines der READMEs erwähnt Android 15. F-Droid listet Wasted 1.5.10 als vorgeschlagen, hinzugefügt am 02.09.2022; die Repository-Aktivität belegt nicht die aktuelle Zuverlässigkeit des Releases. Beide READMEs sagen, dass die Architektur neu gestaltet wird, weil Google die DevicePolicyManager-API geändert hat [**Extern**](#tag-external) | Eine App, deren Verhalten von Hintergrunddiensten abhängt, kann genau dann stillschweigend ausfallen, wenn du sie brauchst |
| Sensible Berechtigungen | Wasted: Device Admin, Foreground Service und Receive Boot Completed (Wasted-README). Sentry: Device Admin, Device Owner (per ADB gesetzt), Notification Listener und Query-All-Packages (Sentry-README) [**Extern**](#tag-external) | Jede davon ist eine privilegierte Komponente auf einem Gerät, das nur eine winzige App-Liste haben soll (Abschnitt 7) |
| Angriffsfläche | Drittanbieter-Code mit hohen Rechten vergrößert die Angriffsfläche ohne verlässlichen Vorteil gegenüber der eingebauten Funktion [**Empfehlung**](#tag-advice) | Open Source macht eine App mit diesen Rechten nicht von selbst sicher |

**Warum GrapheneOS Duress besser ist.**

| Eigenschaft | Duress | Einschränkung |
|---|---|---|
| In das Betriebssystem eingebaut | Keine Drittanbieter-App, die installiert, aktualisiert oder der vertraut werden muss [**Offiziell**](#tag-official) | Es bleibt eine OS-Funktion, die du bewusst konfigurieren musst (Abschnitt 4.1) |
| Löschung | Unumkehrbar; entfernt auch installierte eSIMs [**Offiziell**](#tag-official) | Unumkehrbar heißt unumkehrbar, auch nach versehentlichem Auslösen |
| Zugangsdaten | Erfordert sowohl PIN als auch Passwort; die Eingabe der echten Zugangsdaten hat Vorrang, daher erfolgt keine Löschung [**Offiziell**](#tag-official) | Hilft nur, wenn die Duress-Zugangsdaten am eingeschalteten Gerät in eine Geräte-PIN- oder Passwortabfrage eingegeben werden, auch am Sperrbildschirm. |
| Berechtigungen und Angriffsfläche | Keine zusätzlichen App-Berechtigungen und keine zusätzliche App-Angriffsfläche [**Empfehlung**](#tag-advice) | Kein Beweis, dass es keine Fehler gibt |
| Neustart, Unterbrechung, wo es akzeptiert wird | Die Löschung benötigt keinen Neustart und kann nicht unterbrochen werden; die Eingabe der Duress-PIN/des Duress-Passworts als Gerätezugangsdaten auf dem Sperrbildschirm oder in einer OS-Abfrage nach Gerätezugangsdaten löscht das Gerät unwiderruflich, einschließlich installierter eSIMs. Die Duress-PIN funktioniert auch als PIN der Zwei-Faktor-Fingerabdruck-Entsperrung, aktuell aber nicht als SIM-PIN. Passende echte Entsperrdaten haben Vorrang und löschen nicht [**Offiziell**](#tag-official) (GrapheneOS-Seite „Features“, <https://grapheneos.org/features>) | Einmal ausgelöst, gibt es kein Zurück, auch nicht nach versehentlicher Eingabe [**Empfehlung**](#tag-advice) |

**Rechtlicher und ethischer Hinweis.** Eine Duress-PIN zum Löschen eines Geräts bei einer rechtmäßigen Kontrolle oder einer erzwungenen Entsperrung zu nutzen, kann ernste rechtliche Folgen haben, zum Beispiel Anklagen wegen Behinderung der Justiz in den USA [**Empfehlung**](#tag-advice). Die Regeln unterscheiden sich je nach Land (Abschnitt 10.2). Das Löschen von Daten nach einer rechtlichen Aufforderung oder in Erwartung einer Durchsuchung ist die riskanteste Handlung. Hole lokalen Rechtsrat ein, bevor du dich auf eine Duress- oder Löschfunktion verlässt. Duress ist keine „Freikarte“: Es vernichtet deine eigenen Daten und kann wie die Vernichtung von Beweismitteln wirken.

**Empfehlung.** Installiere Wasted oder Sentry nicht auf einem Cryptophone [**Empfehlung**](#tag-advice). Sie stehen absichtlich in keiner App-Liste dieses Leitfadens. Wenn dein Bedrohungsmodell es rechtfertigt, nutze stattdessen die eingebaute Duress-PIN/das Duress-Passwort [**Offiziell**](#tag-official) und akzeptiere den Kompromiss: Einmal ausgelöst, lässt sich die Löschung nicht rückgängig machen.

---

## 5. Profile und Kompartimente

### 5.1 Empfohlene minimale Struktur

| Profil | Inhalt | Regeln |
|---|---|---|
| **1. Owner** | Nur Systemverwaltung: Updates, App Store, Einstellungen | Keine sozialen Apps, keine privaten Konten, kein Surfen, wenn es nicht nötig ist. Das Owner-Profil speichert sensible systemweite Daten und muss nach einem Neustart zuerst entsperrt werden [**Offiziell**](#tag-official) |
| **2. Sichere Kommunikation** | Signal (oder ein anderer geeigneter Messenger), Authenticator, Passwortmanager, sichere Notizen, minimale Kontakte | Nur die Apps aus Abschnitt 7. Netzwerk für Offline-Apps blockiert |
| **3. Isoliertes Surfen (optional)** | Nur Browser | Keine dauerhaften Konten, keine Kontakte, keine persönlichen Dateien. Sitzung beenden, wenn du fertig bist |

### 5.2 Was Profile leisten und was nicht

- Profile trennen Apps, App-Daten, Schlüssel und die meisten Einstellungen. **Sitzung beenden** (Ein-/Aus-Menü oder Benutzerwechsel) entfernt die Schlüssel des Profils vollständig aus dem Speicher und versetzt es in den Ruhezustand. Für das Owner-Profil geht das nur per Neustart. [**Offiziell**](#tag-official)
- **Profile garantieren keine Anonymität.** Sie teilen zugrunde liegende Hardware und Netzzugang; profilbezogene VPNs sind möglich, daher können Ausgangs-IP-Adressen verschieden sein [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Gewohnheiten und wiederverwendete Telefonnummern, E-Mails, Namen, Kontakte, Dateien oder Schreibstile können Identitäten weiterhin verknüpfen [**Empfehlung**](#tag-advice).
- **WLAN und Bluetooth können Profile korrelieren.** Dieselben Funkmodule und dieselben Netze werden von allen Profilen genutzt.
- **Ein in einem Profil eingerichtetes VPN löst nicht automatisch jedes Netzwerk-Leck-Szenario.** Jedes Profil hat eine eigene VPN-Konfiguration, während Private DNS global ist. [**Offiziell**](#tag-official) Prüfe das Verhalten pro Profil (Checkliste in Abschnitt 13).
- **Verschiebe sensible Daten nicht beiläufig zwischen Profilen.** Meide geteilten Speicher, geteilte Zwischenablage und profilübergreifende Benachrichtigungen.
- **Jedes Profil hat eine eigene Sperrmethode; gib jedem Profil ein eigenes starkes Geheimnis.** Ein schwaches Geheimnis in einem Profil untergräbt dieses Kompartiment. Profile können unterschiedliche Entsperrmethoden haben [**Offiziell**](#tag-official). Ein eigenes starkes Passwort pro Profil ist eine Empfehlung dieses Leitfadens [**Empfehlung**](#tag-advice).
- GrapheneOS hebt das Limit auf 31 Zweitprofile plus Gast an, und Zweitprofile lassen sich so einstellen, dass sie nicht im Hintergrund laufen. [**Offiziell**](#tag-official) Nutze so wenige wie nötig.

### 5.3 Verbleibende Risiken

Profile sind Fächer für Daten, nicht für Identität. Für eine Rolle mit hohem Risiko sind **ein separates Gerät, eine separate SIM/eSIM und ein getrenntes Netzwerknutzungsmuster** die realistische Grenze. Profiltrennung allein ist Kompartimentierung, keine vollständige Grenze. [**Empfehlung**](#tag-advice)

---

## 6. Sandboxed Google Play

- **Installiere Sandboxed Google Play auf einem Cryptophone nicht standardmäßig.**
- Installiere es **nur**, wenn eine bestimmte benötigte App anders nicht funktioniert und du die Google-Abhängigkeit akzeptierst.
- Falls installiert, **isoliere es in einem separaten Profil**, nie im Owner-Profil. Die offizielle Anleitung nennt die Installation im Owner-Profil „den einfachsten Weg“, aber sie ist weniger isoliert. [**Offiziell**](#tag-official) [**Empfehlung**](#tag-advice)
- **Melde dich nie mit einem privaten Google-Konto an.** Ein Google-Konto verknüpft das Profil mit einer Identität bei Google. Die Anmeldung ist optional, außer du brauchst Installationen über den Play Store, In-App-Käufe oder kontoabhängige Funktionen. [**Offiziell**](#tag-official) Beim Anlegen eines Kontos wird häufig eine Telefonnummern-Verifizierung verlangt. [**Empfehlung**](#tag-advice)
- Ein separates Profil begrenzt den Datenzugriff, verhindert aber nicht, dass Google das Konto über IP-Adresse, Geräteeigenschaften, Zeitpunkte oder Kontoaktivität korreliert. [**Empfehlung**](#tag-advice)
- Wer **Google Play services** aus dem App Store installiert, installiert Google Play-Dienste und Google Play Store zusammen; beide laufen als normale Sandbox-Apps ohne Sonderrechte. [**Offiziell**](#tag-official)
- Bevorzuge Apps, die Google Play nicht benötigen.

**Verbleibendes Risiko:** Auch in einem separaten Profil sieht Google wahrscheinlich die über dieses Profil installierten Apps und die empfangenen Geräteinformationen. [**Empfehlung**](#tag-advice)

---

## 7. Apps

### 7.1 Regeln

- Jede App braucht einen dokumentierten Zweck, eine Quelle und eine Berechtigungsliste.
- Bevorzuge quelloffene, aktiv gepflegte Apps.
- Installiere nur aus diesen Quellen, in dieser Rangfolge: dem **GrapheneOS App Store**; der **offiziellen, verifizierten Quelle des Entwicklers** (Signatur prüfen); **Accrescent** (als Mirror in GrapheneOS-Repository-Metadaten geführt [**Offiziell**](#tag-official) (Projektquelltext: <https://github.com/GrapheneOS/apps.grapheneos.org/blob/c8e2b3fb21c420db7d4bab32ce3dd7e42afe7ea9/apps/packages/app.accrescent.client/common-props.toml>); laut eigener Primärquelle in der Alpha-Phase [**Extern**](#tag-external) (<https://accrescent.app/>)); und **F-Droid** nur als Ausweichlösung für Apps, die es anderswo nicht gibt. Nutze weder den Aurora Store noch andere Drittanbieter-Google-Play-Frontends. Sandboxed Google Play selbst ist nur als begründete Ausnahme nach [Abschnitt 6](#6-sandboxed-google-play) erlaubt [**Empfehlung**](#tag-advice).
- Prüfe Herausgeber und Signatur, wo möglich (z. B. einen veröffentlichten Fingerabdruck des Signaturzertifikats).
- Keine Beta-, modifizierten, gecrackten oder „Privacy-Fork“-Apps ohne triftigen Grund.
- Prüfe nach der Installation die Berechtigungen; entferne Apps, die du nicht mehr brauchst.

### 7.2 Hinweise zu den Quellen

| Quelle | Hinweis |
|---|---|
| **GrapheneOS App Store** | Verteilt eigene GrapheneOS-Apps und optional Sandboxed Google Play [**Offiziell**](#tag-official) |
| **Accrescent** | App Store mit Fokus auf Sicherheit und Datenschutz, derzeit in der Alpha-Phase [**Extern**](#tag-external). Seine eigene Seite sagt, er lasse sich aus dem GrapheneOS App Store herunterladen, „der empfohlene Weg für GrapheneOS-Nutzer“ [**Extern**](#tag-external). Er aktualisiert Apps automatisch, unbeaufsichtigt und ohne Sonderrechte ab Android 12 und braucht kein Konto [**Extern**](#tag-external). Das GrapheneOS-App-Repository enthält ihn (Paket `app.accrescent.client`) [**Offiziell**](#tag-official) |
| **F-Droid** | Quelloffene Apps. Apps ohne Reproducible-Build-Einrichtung werden mit App-eigenen F-Droid-Schlüsseln signiert; bei vom Entwickler signierten, reproduzierbaren Apps veröffentlicht F-Droid eine Version nur, wenn sein Build mit dem des Entwicklers übereinstimmt [**Extern**](#tag-external) (F-Droid-Dokumentation). Updates können dem Entwickler hinterherhinken |
| **Offizielle Quelle des Entwicklers** | Den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal prüfen. Einen vorhandenen App-eigenen Updater nutzen und dessen Installationshinweise und Berechtigungen prüfen; andernfalls Updates selbst verfolgen. Der Website-Build von Signal hat einen eigenen Update-Mechanismus (siehe den quellengestützten Signal-Hinweis unten) [**Empfehlung**](#tag-advice) |

**Woher Signal kommt:** Signal wird als direkte Website-APK unter signal.org/android/apk verteilt, die den Fingerabdruck des Signaturzertifikats veröffentlicht, und über Google Play (Signals eigene Primärdokumentation); es ist nicht im Hauptrepository von F-Droid [**Extern**](#tag-external) und nicht im GrapheneOS-App-Repository [**Offiziell**](#tag-official). Signal ist im am 6. November 2026 geprüften Repository-Katalog von Accrescent nicht gelistet (Zeitstempel des Katalogs: 25. Februar 2026; die Verfügbarkeit kann sich ändern) [**Extern**](#tag-external) (<https://repo.accrescent.app/repodata.1.json>). Eine verifizierte Entwickler-APK kann wegen der No-Play-Richtlinie dieses Leitfadens erforderlich sein, obwohl Signal auch über Google Play verfügbar ist. Zuerst die verifizierte Website-APK von Signal nutzen; Sandboxed Google Play ist nur als begründete Ausweichlösung nach [Abschnitt 6](#6-sandboxed-google-play) erlaubt. Andere Drittanbieter-Play-Frontends bleiben ausgeschlossen [**Empfehlung**](#tag-advice). Das Repository bei Verfügbarkeitsänderungen erneut prüfen. Für die Erstinstallation den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal prüfen; „Unbekannte Apps installieren“ nur dem gewählten Dateimanager, nicht dem Browser, erlauben und nach der Installation wieder entziehen. Diese Erstinstallationsberechtigung ist von den Rechten eines App-eigenen Updaters zu unterscheiden; dessen Installationshinweise und Berechtigungen separat prüfen [**Empfehlung**](#tag-advice). Der Website-Build von Signal prüft und lädt Updates selbst. Den Installationshinweisen folgen und die Updater-Berechtigungen separat prüfen; keine stille, unbeaufsichtigte Installation voraussetzen. Im zitierten Projektquellstand gibt `shouldAutoUpdate()` im Installer `false` zurück (Update-Job: <https://github.com/signalapp/Signal-Android/blob/a74583b01e260944f699c4da03ba4e8ce04de32b/app/src/main/java/org/thoughtcrime/securesms/jobs/ApkUpdateJob.kt>; Installer: <https://github.com/signalapp/Signal-Android/blob/a74583b01e260944f699c4da03ba4e8ce04de32b/app/src/main/java/org/thoughtcrime/securesms/apkupdate/ApkUpdateInstaller.kt>). Das ist Quelltextbeleg, kein Test einer ausgelieferten APK. Signals eigene APK-Dokumentation (Primärquelle) veröffentlicht den Fingerabdruck des Signaturzertifikats zur Erstprüfung (<https://signal.org/android/apk/>). Andere Entwickler-APKs ohne eigenen Updater können manuelle Update-Verfolgung und Downloads erfordern.

> ⚠️ Lade nicht von zufälligen APK-Seiten: Das Risiko liegt in der App-Lieferkette und den Updates, nicht in der automatischen Entfernung von Verified Boot oder Sandbox durch eine gewöhnliche APK. Root (Magisk), LSPosed und Xposed sind Systemeingriffe, die Betriebssystemintegrität oder Sandbox-Grenzen untergraben können und nach diesem Leitfaden verboten sind [**Empfehlung**](#tag-advice).

### 7.3 Pflichtkategorien

| Kategorie | Wahl | Warum | Verbleibendes Risiko |
|---|---|---|---|
| **Browser** | **Vanadium** (eingebaut) | Gehärtetes Chromium, auch die System-WebView [**Offiziell**](#tag-official) | Verbirgt weder deine IP noch verhindert es von allein Fingerprinting |
| **Sicherer Messenger** | **Signal** | Ende-zu-Ende-verschlüsselt, geprüft, weit verbreitet. Die Registrierung erfordert eine Rufnummer; Benutzernamen können deine Nummer vor anderen Nutzern verbergen, heben die Pflicht aber nicht auf. [**Extern**](#tag-external) (EFF; Signal-Blogbeitrag zu Rufnummern-Datenschutz und Benutzernamen) | Die Registrierung per Rufnummer bindet das Konto an eine SIM; Metadaten bleiben sichtbar; das Gerät der Gegenseite kann den Chat kompromittieren |
| **Passwortmanager** | **KeePassDX** (GPL-3.0, lokale Datenbank) [**Extern**](#tag-external) | Kein Cloud-Konto nötig; lokale Datenbank | Eine gestohlene Datenbank mit schwachem Master-Geheimnis; nur die Android-App-Sandbox |
| **2FA/Authenticator** | **Aegis** (GPL-3.0) [**Extern**](#tag-external) | Quelloffen, verschlüsselter Tresor | Ein verlorener Tresor ohne Backup; ein kompromittiertes Telefon verrät Codes |
| **Sichere Notizen** | **Einträge in der KeePassDX-Datenbank** | Keine zusätzliche App und kein zusätzliches Konto | Dieselbe Einzelschwachstelle wie die Passwortdatenbank (ein einziger Ausfallpunkt) |
| **VPN-Client, nur wenn begründet** | Offizielle **Mullvad**-App oder die offizielle WireGuard-App [**Offiziell**](#tag-official) | Die zwei Apps, die die GrapheneOS-FAQ empfiehlt; Mullvads App ist quelloffen (GPL-3.0) [**Extern**](#tag-external). Laut GrapheneOS-FAQ wird die Mullvad-App auf GrapheneOS mit Hardware-Memory-Tagging getestet; bei der offiziellen WireGuard-App werden mit aktiviertem MTE ungültige Speicherzugriffe erkannt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Bei standardmäßig aktiviertem MTE Mullvad bevorzugen. Wenn WireGuard zwingend nötig ist, die aktuelle Kompatibilität prüfen und nur bei Bedarf eine App-spezifische Ausnahme verwenden; MTE niemals global deaktivieren [**Empfehlung**](#tag-advice). | Vertrauen verschiebt sich zum Anbieter; die Wahl hängt von Rechtsordnung, Logging, Zahlung und Bedrohungsmodell ab |
| **Dateiübertragung, nur wenn begründet** | Dateien bevorzugt über den Ende-zu-Ende-verschlüsselten Messenger senden. Keine zusätzliche App | Weniger Apps | Datei-Metadaten (EXIF, Dokumenteigenschaften) vorher entfernen |

### 7.4 Optionale Kategorien

| Kategorie | Wahl | Hinweise |
|---|---|---|
| **Verschlüsselte Cloud/Speicher** | **Cryptomator** [**Extern**](#tag-external) | Doppelt lizenziert (GPLv3 und kommerziell). Google Drive wird in den Varianten für den Google Play Store und den APK Store unterstützt, nicht aber in den F-Droid-Varianten (proprietäre Abhängigkeiten), und der Haupt-Build von F-Droid unterstützt außerdem keine Clouds, die einen API-Schlüssel brauchen. Der geprüfte Projektquelltext im zitierten Stand schließt Google Drive für die Varianten `fdroid` und `accrescent` aus; das ist keine Prüfung der ausgelieferten Builds. Nutze eine geeignete APK-Store- oder Play-Variante, wenn Google Drive ausdrücklich nötig ist (<https://github.com/cryptomator/android/blob/96cf59bdbd8de451f16f166217df3d7d39e36bd4/util/src/main/java/org/cryptomator/util/FlavorConfig.kt>). Nur die APK-Store-Variante hat einen eingebauten automatischen Updater; die Varianten für Play Store, F-Droid und Accrescent haben keinen oder aktualisieren anders, über ihre Stores. Laut Cryptomators eigener Einrichtungsdokumentation (Primärquelle) hängen Preise und Freischaltung vom Vertriebskanal ab: Play Full wird vorab bezahlt und bietet vollen Zugriff; Freemium nutzt einen In-App-Kauf, während für APK Store und F-Droid die Lizenzierung laut Einrichtungsdokumentation gilt. Tresore eines Hubs mit aktiver Lizenz bleiben ohne separaten In-App-Kauf oder Lizenzschlüssel beschreibbar (<https://docs.cryptomator.org/android/setup/>). Widerspruch zwischen Dokumentation und Quelltext bei Accrescent: Die Einrichtungsdokumentation verlangt einen Lizenzschlüssel (<https://docs.cryptomator.org/android/setup/>), während der geprüfte `FlavorConfig` am zitierten Stand und am Tag `2.1.0` / `main` (geprüft am 11. November 2026) Accrescent weiterhin als Premium-Variante mit umgangener Lizenzdurchsetzung einstuft (<https://github.com/cryptomator/android/blob/96cf59bdbd8de451f16f166217df3d7d39e36bd4/util/src/main/java/org/cryptomator/util/FlavorConfig.kt>). Auf dem Standardzweig `develop` entfernt Commit `54642f10` / PR #673 (13.–14. Oktober 2026, „Fix Accrescent license handling“) Accrescent aus `isPremiumFlavor` und ergänzt Tests, wonach Accrescent für Schreibzugriff eine Lizenz braucht; dieser Fix war beim Prüfen nicht in Tag `2.1.0` / `main`. Das Lizenzverhalten der ausgelieferten Accrescent-Version wurde nicht geprüft [**Prüfen**](#verify-menu-paths); diese Version vor der Nutzung prüfen und keinen kostenlosen Vollzugriff voraussetzen [**Empfehlung**](#tag-advice). Verschlüsselung verbirgt nicht, dass du Cloud-Speicher nutzt |
| **Karten, nur bei Bedarf** | **Organic Maps** (Apache-2.0) [**Extern**](#tag-external) | Funktioniert offline. Laut README ist das Projekt weit von finanzieller Tragfähigkeit entfernt; prüfe den Pflegestatus, bevor du dich darauf verlässt |
| **PDF-/Dokumentleser, nur bei Bedarf** | Eingebauter **PDF-Betrachter** [**Offiziell**](#tag-official) | Netzwerk blockieren; Dokumente enthalten Metadaten |
| **Tor Browser, nur bei Bedarf** | **Tor Browser für Android** vom Tor Project [**Extern**](#tag-external) | Siehe Abschnitt 9; das GrapheneOS-Projekt sagt, seine Sicherheit sei im Vergleich zu Vanadium schwach und Tor mache Nutzer zu einem interessanteren Ziel [**Offiziell**](#tag-official) |

Ausdrücklich **nicht** empfohlen: weitere Messenger, weitere Browser, soziale Apps, cloudsynchronisierte Notiz-Apps, die ein Konto brauchen, und jede „Privacy“-App ohne dokumentierten Bedarf.

**Verbleibendes Risiko:** Jede App ist zusätzliches Vertrauen und zusätzliche Angriffsfläche. Die sicherste Liste ist die kürzeste.

### 7.5 App-Store-Vergleich

Jeder der folgenden Stores installiert Apps in die normale App-Sandbox. Die Unterschiede liegen darin, ob ein Konto nötig ist, wie Updates ankommen und wem du vertrauen musst. Aussagen zu Stores von Drittanbietern sind mit [**Extern**](#tag-external) markiert und stammen aus der jeweiligen Projektdokumentation; die Empfehlungen sind die Einschätzung dieses Leitfadens.

| Store | Konto nötig? | Google-Abhängigkeit | Update-Mechanismus | App-Auswahl (Umfang, Qualität) | Sicherheitsmodell | Empfehlung: Alltag / Cryptophone |
|---|---|---|---|---|---|---|
| **GrapheneOS App Store** | In der GrapheneOS-Dokumentation wird kein Konto als Voraussetzung genannt [**Offiziell**](#tag-official) | Keine für den Store selbst; er kann zusätzlich Sandboxed Google Play installieren, das optional ist [**Offiziell**](#tag-official) | Aktualisiert die Apps aus seinem Repository im Hintergrund, einschließlich der Komponenten von Sandboxed Google Play [**Offiziell**](#tag-official) | Klein: eigene GrapheneOS-Apps (zum Beispiel Kamera, PDF-Betrachter, Auditor, Vanadium), die Komponenten von Sandboxed Google Play und einige weitere wie der Accrescent-Client [**Offiziell**](#tag-official) | Das App-Repository von GrapheneOS und sein Client, vom GrapheneOS-Projekt gepflegt und in das Betriebssystem integriert [**Offiziell**](#tag-official) | Alltag: erste Wahl. Cryptophone: erste Wahl; Sandboxed Google Play nur installieren, wenn eine benötigte App sonst nicht funktioniert ([Abschnitt 6](#6-sandboxed-google-play)) [**Empfehlung**](#tag-advice) |
| **Accrescent** | Kein Konto nötig [**Extern**](#tag-external) | Vom Projekt keine genannt [**Extern**](#tag-external) | Automatische, unbeaufsichtigte Updates ohne Sonderrechte ab Android 12 [**Extern**](#tag-external) | Kleiner, kuratierter Katalog; das Projekt befindet sich in der Alpha-Phase [**Extern**](#tag-external) | Pinning des App-Signaturschlüssels bei der Erstinstallation, signierte Repository-Metadaten und kein Remote-APK-Signieren, sodass Entwickler ihre Signaturschlüssel behalten [**Extern**](#tag-external) | Alltag: für die Apps nutzen, die er führt. Cryptophone: ebenso. Den Client aus dem GrapheneOS App Store installieren, wie es die Seite von Accrescent für GrapheneOS-Nutzer empfiehlt [**Extern**](#tag-external). In der Quellenreihenfolge von 7.1 steht er nur wegen der Alpha-Phase unter verifizierten Entwickler-Releases [**Empfehlung**](#tag-advice) |
| **F-Droid** | Kein Konto nötig; F-Droid sagt, es verfolge nicht, was du installierst [**Extern**](#tag-external) | Keine Google-Abhängigkeit genannt; ein unabhängiges Repository freier und quelloffener Apps [**Extern**](#tag-external) | Über den F-Droid-Client; die Geschwindigkeit hängt von der App ab, denn F-Droid baut nach eigenem Zeitplan, und manche Apps sind veraltet oder hinken dem Entwickler hinterher [**Empfehlung**](#tag-advice) | Großer Katalog freier und quelloffener Apps; Qualität und Update-Tempo schwanken je App und Repository [**Empfehlung**](#tag-advice) | Apps werden vor der Aufnahme auf Sicherheitsprobleme geprüft [**Extern**](#tag-external). Bei Apps mit reproduzierbaren Builds veröffentlicht F-Droid die Signatur des Entwicklers, nachdem es den Build geprüft hat; andere Apps werden mit F-Droids eigenen Schlüsseln signiert [**Extern**](#tag-external) | Alltag: Ausweichlösung für Apps, die die obigen Stores nicht führen; prüfen, ob die App gepflegt wird. Cryptophone: nur als Ausweichlösung (Regel in 7.1) [**Empfehlung**](#tag-advice) |
| **Aurora Store** | Ja, ein Google-Konto ist nötig. Standardmäßig holt er geteilte Konto-Zugangsdaten vom Dienst von Aurora Store (geteilte Dummy-Konten, die über Token-Dispenser ausgegeben werden); du kannst dich auch mit deinem persönlichen Google-Konto anmelden [**Offiziell**](#tag-official) | Vollständig: Er ist ein alternatives Frontend des Google Play Stores [**Offiziell**](#tag-official) | Aktualisiert die Play-Apps, die er installiert hat. GrapheneOS akzeptiert Updates von Google Play-Diensten, Google Services Framework und Google Play Store nur von seinem eigenen App Store oder vom Play Store selbst, nutze Aurora dafür also nicht [**Offiziell**](#tag-official) | Der für das gewählte Konto und Gerät angezeigte Play-Katalog, einschließlich Kompatibilitäts- und Verteilungsbeschränkungen; die meisten gelisteten Apps sind Closed Source [**Empfehlung**](#tag-advice) | Von Entwicklern signierte Play-Apps, aber die Installationen laufen über Google unter einem geteilten oder einem persönlichen Konto. Geteilte Dummy-Konten sind keine Anonymität: Du verlässt dich auf den Dispenser-Dienst, das Konto teilen sich viele andere Nutzer, und Google kann Geräteinformationen und Installationen weiterhin korrelieren; ein persönliches Konto bindet die Installationen an dich [**Empfehlung**](#tag-advice) | Alltag: letzter Ausweg, nur in einem separaten Profil und nie mit deinem Haupt-Google-Konto. Cryptophone: nicht nutzen [**Empfehlung**](#tag-advice) |
| **Obtainium** | Kein Store-Konto; Obtainium kann konfigurierte Release-Quellen verfolgen. Manche unterstützten Quellen werden vom Entwickler kontrolliert (zum Beispiel ein GitHub- oder GitLab-Release des Entwicklers); andere sind Mirrors oder Aggregatoren. Bewerte jede konfigurierte Quelle einzeln und bevorzuge vom Entwickler kontrollierte URLs im Vertrauensmodell dieses Leitfadens [**Extern**](#tag-external) | Keine, sofern die App selbst Google nicht braucht | Prüft die von dir eingerichteten Release-Seiten, benachrichtigt dich über neue Releases und installiert sie [**Extern**](#tag-external); es ist kein Store mit eigener Prüfung | Alle Apps, die auf unterstützten Release-Seiten APKs veröffentlichen; jede Quelle wählst und richtest du selbst ein. Es unterstützt auch Aggregator- und Mirror-Seiten (zum Beispiel APKPure, Aptoide, Uptodown und APKMirror nur zum Verfolgen) und F-Droid-Repositories von Drittanbietern [**Extern**](#tag-external); APKs von dort werden von Dritten gehostet oder neu verpackt, prüfe also das Signaturzertifikat gegen das des Entwicklers [**Empfehlung**](#tag-advice) | Nur so stark wie dein Vertrauen in jede Quelle und deine Prüfung: Es macht ein unsigniertes oder kompromittiertes Release nicht sicher. Obtainium selbst veröffentlicht einen Fingerabdruck des Signaturzertifikats und einen PGP-Schlüssel zur Prüfung (Obtainium-README, Abschnitt „Installation“) [**Extern**](#tag-external); sein Quelltext liegt auf GitHub (<https://github.com/ImranR98/Obtainium>) | Alltag: optionale Hilfe für Apps, die nur als APK verteilt werden und die die obigen Stores nicht führen. Cryptophone: nicht standardmäßig; es fügt eine App mit der Berechtigung „Unbekannte Apps installieren“ und Netzwerkzugriff hinzu, nutze es also nur bei dokumentiertem Bedarf und prüfe jede Quelle. Richte keine Aggregator- oder Mirror-Quellen ein (APKPure, Aptoide, Uptodown). Die Berechtigung „Unbekannte Apps installieren“ bleibt für Obtainium erteilt und wird nicht nach jeder Installation entzogen [**Empfehlung**](#tag-advice) |
| **Manueller APK-Download** | Kein Store-Konto; die Seite des Entwicklers entscheidet | Keine, sofern die App selbst Google nicht braucht | Der Website-Build von Signal prüft und lädt Updates selbst; folge den Installationshinweisen und prüfe die Updater-Berechtigungen. Andere APKs können manuelle Update-Verfolgung erfordern. Quellenbelege und Einschränkungen stehen in [Abschnitt 7.2](#72-hinweise-zu-den-quellen). | Was der Entwickler veröffentlicht; nicht jede App bietet eine APK | Für die Erstinstallation den Fingerabdruck des Signaturzertifikats oder die Prüfsumme über einen vom Download getrennten Kanal prüfen; „Unbekannte Apps installieren“ nur dem gewählten Dateimanager, nicht dem Browser, erlauben und nach der Installation wieder entziehen. Diese Erstinstallationsberechtigung ist von den Rechten eines App-eigenen Updaters zu unterscheiden; dessen Installationshinweise und Berechtigungen separat prüfen [**Empfehlung**](#tag-advice) | Alltag: Eine verifizierte Entwickler-APK verwenden, wenn eine nötige App im gewählten Store fehlt oder eine andere dokumentierte Quellenanforderung dies begründet. Cryptophone: Eine verifizierte Entwickler-APK kann wegen der No-Play-Richtlinie erforderlich sein, auch wenn eine Play-Version existiert, etwa bei Signal. Bei Signal dem eigenen Updater folgen, statt jeden Download von Hand zu verfolgen [**Empfehlung**](#tag-advice) |

**Verbleibendes Risiko:** Der gewählte Store ändert, wer erfährt, welche Apps du installierst, und wie schnell Korrekturen dich erreichen. Er macht eine App nicht vertrauenswürdig, und kein Anmeldemodus eines Google-basierten Stores macht dich anonym.

---

## 8. Kommunikations-OPSEC

- **Nutze Ende-zu-Ende-verschlüsselte Nachrichten.** Prüfe, wer noch **Metadaten** sieht: Kontaktgraph, Zeitpunkte, IP-Adresse, Rufnummer.
- **Verifiziere Sicherheitsnummern oder Sicherheitsschlüssel**, wo die App das unterstützt. Die EFF beschreibt den Vergleich der Ziffern oder des QR-Codes persönlich oder telefonisch und das anschließende Markieren des Kontakts als verifiziert. [**Extern**](#tag-external) Eine geänderte Nummer bedeutet meist ein neues Telefon oder eine Neuinstallation (Signal-Blog), bestätige es aber über einen anderen Kanal. [**Extern**](#tag-external)
- **Glaube „verschlüsselt“-Versprechen nicht blind.** Frage, was verschlüsselt ist, zwischen wem, und was der Anbieter weiterhin weiß.
- **Verwende Rufnummern nicht über Identitäten hinweg wieder.**
- **Füge keine Kontakte aus deinem privaten Leben** zu einer sensiblen Identität hinzu.
- **Besprich keine operativen Details in Gruppenchats.** Größere Gruppen bedeuten mehr Geräte, die etwas preisgeben können.
- **Verschwindende Nachrichten sind nur eine zusätzliche Kontrolle.** Signal sagt, sie seien „nicht für Situationen, in denen dein Kontakt dein Gegner ist“, und ein Empfänger könne den Bildschirm fotografieren. [**Extern**](#tag-external) Signal-Backups schließen nur Einmal-Ansichts-Nachrichten und Nachrichten aus, die innerhalb von 24 Stunden verschwinden, sodass Nachrichten mit längeren Timern in einem Backup landen können [**Extern**](#tag-external); nutze kurze Timer oder auf diesem Gerät keine Backups.
- **Das Gerät der anderen Person kann die Unterhaltung kompromittieren.** Ende-zu-Ende-Verschlüsselung schützt den Transport, nicht die Endpunkte.
- **Mache keine Screenshots sensibler Unterhaltungen.** Leite sensibles Material nicht beiläufig weiter.
- **Entferne Metadaten** (EXIF, Dokumenteigenschaften), bevor du Dateien teilst.

**Verbleibendes Risiko:** Ein kompromittierter Endpunkt, ein Screenshot, eine weitergeleitete Nachricht oder ein Beobachter mit Verkehrsanalyse hebelt den Schutz der Inhalte oder der Tatsache der Kommunikation aus.

---

## 9. Netzwerk-OPSEC

### 9.1 Mobilfunknetz

- Bei Mobilfunkverbindung identifiziert eine SIM oder eSIM den Anschluss gegenüber dem Betreiber; dieser kann Gerätekennungen, Funkzellen und Zeitpunkte beobachten. Die EFF beschreibt diese Ortung bei eingeschaltetem Telefon, das Signale an ein Betreibernetz sendet, und erklärt, dass das Netz SIM und Gerät gemeinsam beobachtet (Artikel zuletzt geprüft am 29. Oktober 2018; <https://ssd.eff.org/module/problem-mobile-phones>) [**Extern**](#tag-external). Laut GrapheneOS deaktiviert der Flugmodus Mobilfunk-Senden und -Empfangen; WLAN kann separat aktiviert werden, ohne das Mobilfunkradio wieder einzuschalten (<https://grapheneos.org/faq#cellular-tracking>) [**Offiziell**](#tag-official). Andere Ortung über Apps, WLAN und Metadatenkorrelation bleibt möglich; historische Standortaufzeichnungen werden nicht gelöscht [**Empfehlung**](#tag-advice). Die MAC-Adressen-Aussagen des alten EFF-Artikels werden hier nicht auf aktuelles GrapheneOS übertragen.
- **Identitätsverknüpfung über den Netzbetreiber:** Wer dieses Gerät zusammen mit dem privaten Telefon zu denselben Zeiten und an denselben Orten mitführt oder einschaltet, zeigt dieselben Funkzellen; gemeinsamer Kauf von SIM und Gerät oder rückverfolgbare Zahlung, Aufladungen sowie SIM-Registrierungs- und Ausweispflichten (länderspezifisch) können die Leitung mit dir verknüpfen. Die IMEI bleibt beim SIM-Wechsel gleich. Die Prämisse, dass Funkzellen Telefone orten, beschreibt die Freedom of the Press Foundation. [**Extern**](#tag-external) Die Verknüpfungsszenarien sind eine [**Empfehlung**](#tag-advice).
- Eine eSIM hat eine eigene Kennung; die Anforderungen bei der Aktivierung hängen vom Netzbetreiber und vom Land ab. [**Empfehlung**](#tag-advice) [**Prüfen**](#verify-esim)
- Anrufe, SMS und VoLTE sind Dienste des Netzbetreibers; ein VPN deckt sie nicht ab.
- Der LTE-only-Modus verringert die Ausnutzung von altem Funkmodul-Code aus der Ferne. Er ersetzt keine Ende-zu-Ende-verschlüsselten Anrufe und Nachrichten. [**Offiziell**](#tag-official)
- Die EFF berichtet, dass das Abschalten von 2G vor manchen Cell-Site-Simulatoren schützen kann; konkrete Belege für deren Einsatz bei Protesten habe sie nicht gesehen. [**Extern**](#tag-external) Behaupte nicht mehr.
- **Der Flugmodus macht ein Telefon nicht ortungssicher.** Die Freedom of the Press Foundation weist darauf hin, dass er Standortdienste womöglich nicht blockiert, und die EFF, dass Apps GPS-Daten speichern und später senden können; das Ausschalten ist der stärkste verfügbare Schritt (FPF: „the best technical step“). Kein Softwarezustand ist ein Beweis, und ein ausgeschaltetes Telefon kann dort geortet worden sein, wo es zuletzt eingeschaltet war. [**Extern**](#tag-external)
- **Nur WLAN** (keine SIM) entfernt die SIM-basierte Verbindung zu einem Netzbetreiber, nicht aber IP- oder WLAN-Exposition. Ein Telefon ohne SIM kann dort, wo die nationalen Regeln es erlauben, weiterhin Notrufe absetzen (Android verlangt, dass Notrufnummern ohne SIM funktionieren) [**Extern**](#tag-external). Ein Telefon ohne SIM hat keine SIM-basierte Teilnehmeranmeldung, aber ein zugelassener Mobilfunk-Notruf kann dem versorgenden Netz eine Gerätekennung offenlegen; die Kennung hängt von der Zugangstechnologie ab. Die bloße Nutzung von WLAN kontaktiert für sich genommen keinen Mobilfunkanbieter. „Ohne SIM“ verhindert nicht jede Gerätekennung bei einem Notruf, und nicht jedes Netz legt in jeder Konfiguration eine IMEI offen [**Extern**](#tag-external) (3GPP TS 23.167: <https://www.3gpp.org/ftp/specs/PDF/2026-09/Rel-19/23_series/23167-j20.pdf>) <a id="verify-imei"></a>[**Prüfen**](#verify-imei) (wie das für ein bestimmtes Netz gilt, wurde nicht geprüft). Bei einem solchen Gerät muss WLAN notgedrungen an sein (Lockerung von Regel 11), und manche Dienste verlangen bei der Registrierung eine Rufnummer.

### 9.2 Öffentliches WLAN und Captive Portals

- Öffentliches WLAN setzt deinen Verkehr dem Betreiber aus und zeigt deine IP. Nutze es nur für Verkehr, den der Betreiber sehen darf; das gilt auch für Updates und App-Installationen, und meide dein Heim-WLAN, wenn Verknüpfung eine Rolle spielt (Abschnitt 9.5). [**Empfehlung**](#tag-advice)
- **Captive Portals** verlangen womöglich Rufnummer oder E-Mail-Adresse. [**Empfehlung**](#tag-advice) Die EFF warnt (Artikel von 2017), sie ähnelten einem Man-in-the-Middle, trainierten Nutzer, Zertifikatswarnungen zu ignorieren, und könnten Aktivität an ein Login oder eine Identität binden. [**Extern**](#tag-external) Das Anmeldeverhalten bei Captive Portals mit aktivierter Sperre ist hier ungeprüft [**Prüfen**](#verify-menu-paths). Falls die Anmeldung ein vorübergehendes Aufheben der Sperre erfordert, dies nur bei akzeptabler Exposition tun und sie sofort wieder aktivieren oder das Netz meiden [**Empfehlung**](#tag-advice).
- Videoüberwachung, Zahlungsbelege und Standortmuster können eine Person weiterhin einem Ort zuordnen.
- Ein VPN verbirgt Ziele und Inhalte vor dem lokalen Netz, nicht die Tatsache, dass ein VPN genutzt wird.

### 9.3 VPN, Tor, DNS

| Werkzeug | Hilft bei | Hilft nicht bei |
|---|---|---|
| **VPN** | Nicht vertrauenswürdigem lokalem Netz oder Provider; verbirgt deine IP vor Websites | Dem VPN-Anbieter, der den Verkehr sieht; Funkzellen-Ortung; Konten, in die du dich einloggst; Anrufen und SMS. „A VPN is not a tool for anonymity“; „If you are interested in increased anonymity, Tor is a better solution than a VPN“ [**Extern**](#tag-external) |
| **Tor Browser** | Verbirgt deine IP vor Websites durch Mehrfach-Routing | Die Preisgabe deiner Identität kann Aktivitäten dir zuordnen; Tor schützt nur dafür konfigurierte Apps. Die Tor-Dokumentation beschreibt Letterboxing als Schutz auch bei Größenänderungen [**Extern**](#tag-external) (Primärdokumentation: <https://support.torproject.org/tor-browser/features/fingerprinting-protections/>). Standard-Anti-Fingerprinting-Einstellungen beibehalten und keine zusätzlichen Add-ons installieren [**Empfehlung**](#tag-advice) (auch Tor rät von Add-ons ab: <https://support.torproject.org/tor-browser/features/plugins/>). Das ist keine Android-Anweisung zur Fenstergröße; das Android-Fensterverhalten ist hier ungeprüft [**Prüfen**](#verify-menu-paths). GrapheneOS bezeichnet die Sicherheit des Tor Browsers als schwach [**Offiziell**](#tag-official) (<https://grapheneos.org/usage#web-browsing>) |
| **Private DNS** | Opportunistischer oder authentifizierter DNS-Verschlüsselung | Kein Ersatz für Tor oder ein VPN. Private DNS ist global. Keinen Private-DNS-Hostnamen zusammen mit einem VPN konfigurieren; sobald irgendein Zweitprofil ein VPN nutzt, Private DNS global vollständig auf Aus stellen, wie GrapheneOS ausdrücklich empfiehlt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Dieser Leitfaden empfiehlt zusätzlich als strengere Autorenregel Aus bei jedem VPN [**Empfehlung**](#tag-advice). |

**Tor ist nicht für alles geeignet.** Es ist langsam, fingerprintbar und macht keine App außerhalb des Browsers anonym. Das Tor Project bietet Tor VPN (Beta) an, um andere Apps umzuleiten, und warnt, die Beta diene nur zum Testen und sei „nicht für irgendetwas Sensibles“ zu verwenden [**Extern**](#tag-external) (<https://support.torproject.org/tor-vpn/>). Orbot ist eine App des Guardian Project, keine offizielle Tor-Project-App. In einem [Beitrag des offiziellen GrapheneOS-Kontos im GrapheneOS Discussion Forum vom 4. November 2024](https://discuss.grapheneos.org/d/17090-what-is-grapheneos-team-stance-on-orbot/5) empfahl das Projekt, Orbot wegen schlechter Umsetzung und mangelnder Vertrauenswürdigkeit zu meiden, und stellte klar, dass die eigene VPN-App von Tor genutzt werden solle, sobald sie verfügbar sei [**Offiziell**](#tag-official). Ein früherer [Issue-Kommentar vom 1. Mai 2020](https://github.com/GrapheneOS/os-issue-tracker/issues/210#issuecomment-622457418) von Maintainer thestinger kritisierte ebenfalls Orbots Umsetzung und lehnte es ab, Orbot zu forken oder zu bündeln [**Offiziell**](#tag-official). Tor VPN ist inzwischen als Beta verfügbar; die für diesen Leitfaden geprüfte GrapheneOS-Primärdokumentation ergänzt keine spätere Bewertung dieser Beta über die datierte Präferenz für Tors eigene VPN-App gegenüber Orbot hinaus.

### 9.4 Bluetooth und Geräte in der Nähe

- Lass Bluetooth aus. Tracker und Beacons in der Nähe können ein Gerät protokollieren, das sich bemerkbar macht. [**Empfehlung**](#tag-advice)
- Koppele dieses Gerät nicht mit Zubehör, das mit deiner persönlichen Identität verbunden ist.

### 9.5 Identitäten über das Netz nie vermischen

Melde dich auf diesem Gerät nicht in privaten Konten an, öffne keine privaten Links und nutze nicht dasselbe Heim-WLAN für die sensible und deine private Identität, wenn Verknüpfung eine Rolle spielt. Nutze ein WLAN, dem dein privates Telefon nie beitritt, und benutze beide Geräte nicht zu denselben Zeiten und an denselben Orten. [**Empfehlung**](#tag-advice)

**Verbleibendes Risiko:** Netzbetreiber, WLAN-Betreiber, VPN-Anbieter und Zielserver sehen jeweils einen Ausschnitt. Kein Werkzeug in diesem Abschnitt beseitigt alle auf einmal.

---

## Behavioral OPSEC / Verhaltens-OPSEC

Die Einstellungen in Abschnitt 4 schützen das Gerät. Dieser Abschnitt behandelt, was du damit tust, denn Identitäten werden meist durch Gewohnheiten verknüpft, nicht durch technische Schwächen. Jede Empfehlung unten nennt ihre Grenze, und keine macht dich anonym. Quellen sind primäre GrapheneOS-Dokumentation und GrapheneOS-Projektquelltext [**Offiziell**](#tag-official), genannte externe Primärquellen wie EFF Surveillance Self-Defense, Freedom of the Press Foundation und Tor Project [**Extern**](#tag-external) (siehe Abschnitt „Nützliche Webseiten“) sowie die Einschätzung dieses Leitfadens [**Empfehlung**](#tag-advice). Alles Unbestätigte ist [**Prüfen**](#tag-verify).

### SIM-/eSIM-Disziplin

| Situation | Tun | Warum | Grenze |
|---|---|---|---|
| Konnektivität wählen | Nutze für diese Identität eine eigene SIM oder eSIM oder bleibe bei reinem WLAN, wenn du ohne Anrufe, SMS und mobile Daten auskommst [**Empfehlung**](#tag-advice) | Eine eigene Leitung ist nicht mit deinem normalen Telefon verknüpft; reines WLAN entfernt die SIM-basierte Verbindung zu einem Netzbetreiber | Eine SIM bindet die Leitung weiterhin an einen Netzbetreiber sowie an Registrierungs- und Zahlungsdaten. Reines WLAN zeigt weiterhin deine IP-Adresse und die genutzten WLAN-Netze, und manche Dienste verlangen bei der Registrierung eine Rufnummer |
| Dieselbe SIM oder eSIM für mehrere Identitäten | Niemals (siehe Regel 5 der Geräterichtlinie) | Eine SIM ist eine IMSI und eine Nummer beim Netzbetreiber; jede Identität, die sie nutzt, lässt sich vom Netzbetreiber und von jedem, der die Nummer kennt, verknüpfen [**Empfehlung**](#tag-advice) | Auch getrennte SIMs lassen sich über die übrigen Punkte dieses Abschnitts verknüpfen |
| IMSI/IMEI-Paarung | Wechsle die SIM nicht zwischen Telefonen und setze keine alte SIM in ein neues Telefon | Das Netz beobachtet SIM und Gerät gemeinsam, daher bietet das Umstecken einer SIM in ein anderes Gerät nur minimalen Schutz (EFF) [**Extern**](#tag-external) | Eine bereits protokollierte Paarung lässt sich nicht rückgängig machen; eine neue SIM in einem alten Telefon verknüpft genauso |
| eSIM | Behandle eine eSIM wie eine SIM | Eine eSIM hat eine EID, die ihre eUICC-Hardware identifiziert (Android-Dokumentation) [**Extern**](#tag-external); die Anforderungen bei der Aktivierung hängen vom Netzbetreiber und vom Land ab, eine eSIM ist also nicht anonymer [**Empfehlung**](#tag-advice) <a id="verify-esim"></a>[**Prüfen**](#verify-esim) (keine Primärquelle für den Teil zu Konto, Ausweis oder Zahlung gefunden). Die eSIM-Unterstützung ist in GrapheneOS standardmäßig aus [**Offiziell**](#tag-official) | Ein Duress-Wipe entfernt auch installierte eSIM-Profile [**Offiziell**](#tag-official); ein erneuter Download hängt vom Netzbetreiber ab |
| SIM entfernen oder deaktivieren | Entferne die SIM oder deaktiviere die eSIM, wenn du kein Mobilfunknetz brauchst und die Verbindung zum Netzbetreiber vermeiden willst | Beendet die SIM-basierte Anmeldung im Netz [**Empfehlung**](#tag-advice) | Notrufe können ohne SIM funktionieren, wo die nationalen Regeln es erlauben [**Extern**](#tag-external); ein zugelassener Notruf kann dem versorgenden Netz je nach Zugangstechnologie eine Gerätekennung offenlegen [**Extern**](#tag-external) [**Prüfen**](#verify-imei); WLAN- und IP-Exposition bleiben |
| Prepaid- oder „anonyme“ SIM | Kenne die Grenzen, bevor du dich darauf verlässt | Prepaid verringert nur Vertrags- und Abrechnungsspuren | Regeln zur Registrierung und Ausweispflicht bei Prepaid-SIMs unterscheiden sich je nach Land und Netzbetreiber [**Prüfen**](#verify-sim-rules) (keine verlässliche länderübergreifende Quelle gefunden; die EFF-Quelle wurde nicht unabhängig gelesen); Kauf mit Karte, gemeinsamer Kauf mit dem Telefon, Aufladen mit rückverfolgbarer Zahlung und gemeinsames Mitführen mit dem privaten Telefon hinterlassen jeweils Spuren [**Empfehlung**](#tag-advice) |
| Rufnummer | Verwende deine private Nummer nie für eine sensible Identität | Die Nummer verknüpft Konten, auch dein Messenger-Konto | Signal verlangt bei der Registrierung eine Nummer; Benutzernamen verbergen sie nur vor anderen Nutzern [**Extern**](#tag-external) |

### Eine separate Leitung einrichten

Ein Werkzeug auszuwählen genügt nicht; wie du es beschaffst und aktivierst, entscheidet, ob es Identitäten trennt. Die Geräterichtlinie (Regeln 3, 5 und 6) und die Tabelle oben liefern die Grundlagen.

- **Prepaid-SIM:** Kaufe sie ohne Angaben oder Spuren, die über die Registrierungspflicht deines Landes hinausgehen, und registriere und lade sie auf, ohne deine Hauptnummer, deine private E-Mail-Adresse oder ein mit dir verknüpftes Zahlungsmittel. [**Empfehlung**](#tag-advice) [**Prüfen**](#verify-sim-rules)
- **eSIM:** ein herunterladbares Netzbetreiberprofil; ihre EID identifiziert die eUICC-Hardware [**Extern**](#tag-external) (Android-Dokumentation: <https://source.android.com/docs/core/connect/esim-euicc-api>). Meist bekommst du sie über die App oder Website des Netzbetreibers und aktivierst sie mit einem QR- oder Aktivierungscode auf dem Zielgerät. Nutze eine eigene E-Mail-Adresse und, wenn möglich, ein eigenes Zahlungsmittel. Was die Aktivierung verlangt, hängt vom Netzbetreiber und vom Land ab. [**Empfehlung**](#tag-advice) [**Prüfen**](#verify-esim)
- **Reine Daten-eSIM-Tarife:** Manche Anbieter verkaufen sie (laut Anbieterbeschreibung). Dabei wird keine Rufnummer vergeben, aber Anrufe, SMS und Registrierungen per Rufnummer funktionieren dann nicht. [**Empfehlung**](#tag-advice) [**Prüfen**](#verify-esim)
- **Virtuelle oder Zweitnummern (SMS-Miet- oder VoIP-Dienste):** eine andere Kategorie, und nicht anonym. Nummern können geteilt oder wiederverwendet werden, und eine an jemand anderen neu vergebene Nummer kann diesem erlauben, Codes für daran gebundene Konten zu empfangen [**Prüfen**](#verify-sim-rules) (keine Primärquelle zu Neuvergabe-Praktiken gefunden). Ein Dienst kann solche Nummern ablehnen. Die Bedingungen von Signal verlangen, dass du die Rechte an der Nummer hast, mit der du dich registrierst [**Extern**](#tag-external) (<https://signal.org/legal/>). Betrachte ein an eine solche Nummer gebundenes Konto als eines, das du verlieren kannst. [**Empfehlung**](#tag-advice)
- **Eine Nummer ist in jedem Fall eine gemeinsame Kennung:** Der Netzbetreiber kennt die SIM, und ein Dienst, bei dem du dich registrierst, kann die Nummer erhalten. [**Empfehlung**](#tag-advice)

### Wann du das Telefon ausschalten solltest

**BFU und AFU.** Before First Unlock (BFU) ist der Zustand nach dem Start bis zum ersten Entsperren: Die Daten ruhen, und die Profilschlüssel liegen nicht im Speicher. Nach dem ersten Entsperren (After First Unlock, AFU) liegen die Schlüssel im Speicher, und es liegt mehr Angriffsfläche offen. Das Auto-Reboot von GrapheneOS startet den Countdown bei jedem Sperren; erfolgreiches Entsperren eines beliebigen Profils hebt ihn auf. Läuft er ab, startet das gesperrte Gerät neu und versetzt Daten in den Ruhezustand. In BFU greift die Funktion nicht und verursacht dort keine wiederholten Neustarts [**Offiziell**](#tag-official) (<https://grapheneos.org/features#auto-reboot>).

| Wann | Tun | Warum | Grenze |
|---|---|---|---|
| Vor sensiblen Orten oder Treffen | Schalte das Telefon vollständig aus, bevor du ankommst, nicht erst an der Tür [**Empfehlung**](#tag-advice) | Im Normalbetrieb erzeugt ein ausgeschaltetes Telefon keine neue Funkaktivität und keine neue Standortspur (seltene Ausnahmen: siehe den Hinweis zu ausgeschalteten Telefonen unten) | Der Netzbetreiber und andere Beobachter sehen weiterhin, wo und wann das Telefon offline ging, und die Gewohnheit, am selben Ort auszuschalten, ist selbst ein Signal [**Empfehlung**](#tag-advice) |
| Vor Grenzen und riskanten Kontrollstellen | Schalte vollständig aus und starte das Telefon erst an einem Ort, dem du vertraust [**Empfehlung**](#tag-advice). Das EFF-Material zur US-Grenze nennt dasselbe [**Extern**](#tag-external) (auf die USA bezogen, siehe Abschnitt 10) | Ein vollständig ausgeschaltetes Gerät befindet sich in BFU | Verhindert keine Durchsuchung des Geräts; die Regeln unterscheiden sich je Land [**Prüfen**](#verify-legal) |
| Wenn es nicht aktiv gebraucht wird | Lass es ausgeschaltet | Weniger Standortspur, weniger Exposition | Im ausgeschalteten Zustand erhältst du keine Nachrichten oder Benachrichtigungen; wende die Regel nicht an, wenn du erreichbar sein musst |
| Auto-Reboot | Lass es an (Abschnitt 4.1) | Versetzt das Gerät in BFU, wenn es bis zum Ablauf des Countdowns gesperrt bleibt | Erfolgreiches Entsperren eines beliebigen Profils hebt den Countdown auf; keine wiederholten Neustarts in BFU. Nur eine Teilmaßnahme: kein Schutz bei Beschlagnahme vor Ablauf und kein Ersatz für manuelles Ausschalten [**Empfehlung**](#tag-advice) |

**Ausgeschaltet heißt nicht „nicht ortbar“.** Die Freedom of the Press Foundation nennt das Ausschalten des Geräts den besten technischen Schritt gegen Standortverfolgung [**Extern**](#tag-external). Es kann bereits vorhandene Standortverläufe nicht rückgängig machen. Die FPF weist darauf hin, dass in seltenen Fällen WLAN- und Bluetooth-Signale auch bei ausgeschaltetem Gerät weiter ausgesendet werden können [**Extern**](#tag-external), und die EFF, dass Schadsoftware ein Ausschalten vortäuschen könnte [**Extern**](#tag-external). Der Flugmodus ist schwächer: Er blockiert Standortdienste womöglich nicht, und Apps können Standortdaten speichern und später senden [**Extern**](#tag-external).

**Faraday-Beutel.** Ein Beutel kann nützlich sein, wenn du ein Gerät nicht zurücklassen kannst und Funksignale blockieren willst, solange es darin liegt; die FPF nennt ihn als Option für den strengsten Standortschutz [**Extern**](#tag-external). Er wiegt dich in falscher Sicherheit, wenn du ihn nicht testest, wenn er nicht vollständig geschlossen ist oder wenn du glaubst, er schütze vor einem kompromittierten Gerät oder behebe schlechte Gewohnheiten. Die FPF nennt keine Grenzen, daher sind die oben genannten Grenzen eine [**Empfehlung**](#tag-advice); die FPF merkt zudem an, dass das Zurücklassen des Geräts die einzig sichere Methode ist [**Extern**](#tag-external). Er ersetzt das Ausschalten nicht.

### Was du NICHT tun solltest

| Nicht tun | Warum | Grenze |
|---|---|---|
| In alten privaten Konten anmelden (Google, soziale Medien, Banking) | Eine einzige Anmeldung bindet das Gerät an deine echte Identität | Ein neues Konto ist eine neue Spur; neue Konten brauchen weiterhin eine saubere E-Mail-Adresse, Nummer und Zahlungsmethode |
| Benutzernamen, E-Mail-Adressen, Profilbilder oder Wiederherstellungskontakte wiederverwenden | Wiederverwendung ist ein häufiger Weg, Identitäten zu verknüpfen | Schreibstil, Zeitpunkte und Kontakte können Identitäten weiterhin verknüpfen |
| Beiläufig Kontakte mit echtem Namen hinzufügen | Kontaktgraphen identifizieren Personen | Ist ein Kontakt mit echtem Namen nötig, nutze Contact Scopes (Abschnitt 4.3); der Kontakt weiß trotzdem, wer du bist |
| Operative Details in Gruppenchats besprechen | Mehr Mitglieder bedeuten mehr Geräte, die etwas preisgeben können | Ende-zu-Ende-Verschlüsselung schützt nicht vor dem kompromittierten Gerät eines Mitglieds |
| Beiläufig Screenshots machen oder sensibles Material weiterleiten | Kopien bleiben bestehen und wandern aus deiner Kontrolle | Verschwindende Nachrichten verhindern nicht, dass ein Empfänger den Bildschirm fotografiert [**Extern**](#tag-external) |
| Dieselbe Zahlungsmethode für sensible und private Käufe nutzen | Zahlungsdaten verknüpfen Identitäten | Jede Zahlungsmethode hinterlässt eigene Daten; auch Bargeld hat Grenzen (Videoüberwachung, Seriennummern) [**Empfehlung**](#tag-advice) |
| Apps „nur zum Ausprobieren“ installieren | Jede App erhöht Vertrauensbedarf und Angriffsfläche (Abschnitt 7) | Deinstallieren macht nicht rückgängig, was die App bereits gesammelt hat |
| Gespeicherte oder private WLAN-Netze behalten oder versteckten Netzen beitreten | Beim Suchen nach gespeicherten versteckten WLANs sendet das Telefon deren Netzwerknamen aus. [**Offiziell**](#tag-official) Gespeicherte private Netze binden das Gerät an Orte, mit denen du verknüpft bist [**Empfehlung**](#tag-advice) | Jedes WLAN zeigt dem Betreiber weiterhin deine IP-Adresse und Zeitpunkte; MAC-Randomisierung verbirgt kein Verhalten |
| Bluetooth-Zubehör nutzen, das mit deinen persönlichen Geräten verbunden ist | Die Kopplung verknüpft Geräteidentitäten | Bluetooth-Beacons und Geräte in der Nähe können ein Gerät, das sich bemerkbar macht, weiterhin beobachten [**Empfehlung**](#tag-advice) |
| „Gelöschte“ Daten als Schutz betrachten | Gelöschte Daten können in Backups, Caches und auf Geräten von Empfängern fortbestehen | Die vollständige Speicherverschlüsselung schützt ruhende Daten, nicht Daten, die schon anderswohin kopiert wurden [**Empfehlung**](#tag-advice) |

### Tägliche Gewohnheiten

| Gewohnheit | Warum | Grenze |
|---|---|---|
| Das Gerät ausgeschaltet lassen, wenn es nicht gebraucht wird | Weniger Exposition und Standortspur | Du verpasst Nachrichten; wähle ein Intervall, das du durchhältst |
| Eine starke Passphrase statt nur Biometrie (Abschnitt 2) | Widersteht Raten und erzwungener biometrischer Entsperrung | Hilft nicht mehr, sobald das Telefon in deiner Hand entsperrt ist |
| Auto-Reboot eingeschaltet lassen | Versetzt Daten bei Ablauf des gesperrten Countdowns in BFU; erfolgreiches Entsperren eines beliebigen Profils hebt ihn auf; keine wiederholten Neustarts in BFU | Nur eine Teilmaßnahme (siehe oben) |
| Regelmäßig nach Updates suchen | Sicherheitskorrekturen gehören zu den wertvollsten Schutzmaßnahmen [**Empfehlung**](#tag-advice) | Hält unbekannte Schwachstellen nicht auf |
| Installierte Apps und Berechtigungen wöchentlich prüfen | Erkennt Abweichungen und vergessene Apps | Eine vertrauenswürdige App kann gewährte Rechte trotzdem missbrauchen |
| Verschwindende Nachrichten als zusätzliche Ebene nutzen | Verringert, was auf Geräten zurückbleibt | „Nicht für Situationen, in denen dein Kontakt dein Gegner ist“, und der Empfänger kann den Bildschirm fotografieren [**Extern**](#tag-external) |
| Sicherheitsnummern mit Kontakten verifizieren | Erkennt einen geänderten Schlüssel | Die EFF beschreibt den Vergleich der Ziffern oder des QR-Codes persönlich oder telefonisch [**Extern**](#tag-external). Eine geänderte Nummer bedeutet meist ein neues Telefon oder eine Neuinstallation (Signal-Blog); bestätige sie über einen anderen Kanal [**Extern**](#tag-external) |
| Das Gerät physisch sichern und nie unbeaufsichtigt lassen | Physischer Zugriff umgeht viele Schutzmaßnahmen | Auch ein gesperrtes, beaufsichtigtes Gerät kann weggenommen werden; betrachte ein Gerät, das außerhalb deiner Kontrolle war, als nicht vertrauenswürdig (Abschnitt 11) |

### Verhalten auf Reisen

Abschnitt 10 enthält die vollständigen Reise- und Grenzdetails. Im Alltag gilt:

- **Entscheide vor der Reise, was auf dem Gerät sein muss.** Entferne den Rest, soweit praktikabel auch Chat- und Browserverläufe [**Extern**](#tag-external) (Reise-Checkliste der EFF von 2025 für Journalisten, auf die USA bezogen). Grenze: Alles, was bleibt, kann bei einer Durchsuchung gelesen werden.
- **Erwäge ein separates Reisegerät oder ein sauberes Profil.** Grenze: Der EFF-Grenzleitfaden von 2017 warnt, dass ungewöhnliche oder geleerte Geräte Verdacht und Nachfragen auslösen können [**Extern**](#tag-external) (auf die USA bezogen), und das Gerät hat trotzdem eine SIM und eine IMEI.
- **Schalte vor Grenzen und Kontrollstellen aus.** Grenze: Es verhindert die Durchsuchung selbst nicht.
- **Grenzdurchsuchungen können stattfinden; nimm nichts mit, dessen Verlust oder Offenlegung du nicht verkraften kannst.** Die Regeln unterscheiden sich je Land [**Prüfen**](#verify-legal). Grenze: Keine Einstellung macht ein beschlagnahmtes Gerät sicher.
- **Verlasse dich nicht auf versteckte Dateien oder „gelöschte“ Daten.** Grenze: Forensik-Werkzeuge können mehr wiederherstellen, als die meisten Nutzer erwarten [**Empfehlung**](#tag-advice).
- **Halte einen Wiederherstellungsplan für verlorene, beschlagnahmte oder kompromittierte Geräte bereit** (Abschnitt 11), mit Wiederherstellungscodes offline und getrennt vom Gerät. Grenze: Ein Plan hilft nur, wenn du ihn durchspielst.

### Identitätstrennung in der Praxis

- **Halte private Identitäten von diesem Gerät fern. Trenne seine sensiblen Aufgaben durch eigene Profile.** Profile isolieren App-Daten, teilen aber zugrunde liegende Hardware/Netzzugang; profilbezogene VPNs können verschiedene Ausgangs-IPs ergeben [**Offiziell**](#tag-official). Gewohnheiten und wiederverwendete Konten bleiben Korrelationsrisiken, keine Anonymitätsgarantie [**Empfehlung**](#tag-advice).
- **Nutze private Konten in keinem Profil auf diesem Gerät.** Grenze: Ein Profil trennt Daten, nicht die Person, die es nutzt.
- **Nutze pro Identität eine eigene E-Mail-Adresse, Rufnummer, einen eigenen Benutzernamen und ein eigenes Profilbild.** Grenze: Du musst sie jedes Mal getrennt halten; ein einziger Ausrutscher verknüpft sie.
- **Teile zwischen Identitäten keine Dateien, Zwischenablageinhalte oder Benachrichtigungen.** Grenze: Ein Screenshot oder eine kopierte Zeile genügt, um die Grenze zu überschreiten.
- **Metadaten können Identitäten auch bei technischer Trennung korrelieren.** Zeitpunkte, Standort, Kontakte und Schreibstil sind Signale [**Empfehlung**](#tag-advice); wer sich bei Tor in einem Konto anmeldet, verrät der Seite, wer er ist [**Extern**](#tag-external).

**Verbleibendes Risiko:** Verhalten ist das schwächste Glied: Es erfordert tägliche Disziplin, und ein einziger Fehler kann Monate der Trennung zunichtemachen. Für eine Rolle mit hohem Risiko sind ein separates Gerät, eine separate SIM oder eSIM und ein getrenntes Netzwerknutzungsmuster die realistische Grenze; dieser Abschnitt verringert die Exposition, er beseitigt sie nicht.

---

## 10. Reisen und physische Sicherheit

Das ist keine Rechtsberatung. Regeln zu Durchsuchung, Beschlagnahme und erzwungener Entsperrung unterscheiden sich je Land und ändern sich. Prüfe die Regeln jedes Landes, in das du einreist oder durch das du reist. [**Prüfen**](#verify-legal) Das hier zitierte EFF-Grenzmaterial ist nur eine US-Grundlage; die Grenzhinweise von EFF SSD und FPF gelten nur für die USA, und keine Primärquelle im Prüfumfang deckt andere Länder ab.

### 10.1 Vor der Reise

- **Daten minimieren.** Entscheide, was auf dem Gerät sein muss, und entferne den Rest, soweit praktikabel auch Chat- und Browserverläufe. [**Extern**](#tag-external) (Reise-Checkliste der EFF für Journalisten, auf die USA bezogen)
- **Unnötige Apps entfernen.**
- **Nutze ein Reisegerät oder ein sauberes Profil**, falls angemessen; nimm keine sensiblen Daten mit, deren Verlust oder Offenlegung du nicht verkraften kannst. Der EFF-Grenzleitfaden von 2017 warnt, dass ungewöhnliche oder geleerte Geräte Verdacht und Nachfragen auslösen können. [**Extern**](#tag-external) (auf die USA bezogen)
- **Aktualisieren und neu starten.** Kurzes Auto-Reboot-Intervall setzen.
- **Sichere** nur, was du brauchst, verschlüsselt, und bewahre das Backup an anderer Stelle auf.
- **Wiederherstellungscodes** bleiben offline, verschlüsselt und getrennt vom Gerät.

### 10.2 An Grenzen und Kontrollstellen

- **Schalte das Gerät vor der Kontrolle vollständig aus**; die EFF merkt an, dass ein vollständig heruntergefahrenes Gerät die Festplattenverschlüsselung wiederherstellt. [**Extern**](#tag-external) (auf die USA bezogene Checkliste)
- **Starke Authentifizierung.** Lange, unvorhersehbare alphanumerische Geheimnisse werden empfohlen; die EFF-Checkliste von 2025 rät, vorab zu entscheiden, ob du entsperrst, und es in dem Fall selbst einzugeben und anwesend zu bleiben (auf die USA bezogen). [**Extern**](#tag-external)
- **Biometrie:** Die EFF sagt, im Protestkontext bestehe weniger Schutz gegen erzwungenes Entsperren per Gesicht oder Fingerabdruck als gegen erzwungene Herausgabe eines Passworts. [**Extern**](#tag-external) Lass die Biometrie ausgeschaltet. Rechtsordnungsabhängig. [**Prüfen**](#verify-legal)
- **Kenne die Realität von Grenzdurchsuchungen:** In den USA kann Nicht-Staatsbürgern, die eine Durchsuchung verweigern, die Einreise verweigert werden (EFF-Checkliste; auf die USA bezogen). [**Extern**](#tag-external)
- Nach der Richtlinie der US-Grenzbehörde CBP dürfen Beamte nur auf dem Gerät gespeicherte Daten durchsuchen, nicht Live-Cloud-Inhalte (auf die USA bezogen; andere Länder weichen ab). Die EFF-Checkliste von 2025 sagt, Beamte seien per Richtlinie angewiesen, das Gerät in den Flugmodus zu versetzen oder anderweitig zu trennen (als veröffentlichte Richtlinie; die Praxis kann abweichen); die aktuelle CBP-Richtlinie zur Grenzdurchsuchung ist Nr. 3340-049B (<https://www.cbp.gov/document/directives/cbp-directive-no-3340-049b-border-search-electronic-devices>), und die EFF bezweifelt, dass die Praxis immer der Richtlinie entspricht. [**Extern**](#tag-external)
- Die CBP-Richtlinie 3340-049B wurde am 28. Januar 2026 veröffentlicht und gilt seit dem 1. Januar 2026. Abschnitt 5.1.2 beschränkt die Untersuchung auf Informationen, die sich auf dem Gerät befinden und über das Gerät zugänglich sind, und lässt den absichtlichen Zugriff auf ausschließlich extern gespeicherte Informationen nach der veröffentlichten Richtlinie nicht zu. Die Netzverbindung wird wie in der Richtlinie festgelegt getrennt. Das beschreibt den Geltungsbereich der Richtlinie, nicht ihre Einhaltung in jeder Kontrolle [**Extern**](#tag-external) (<https://www.cbp.gov/sites/default/files/2026-01/cbp_directive_3340-049b_jan_2026_508.pdf>). Der Flugmodus schützt keine bereits auf dem Gerät liegenden Daten und macht das Telefon nicht ortungssicher (Abschnitt 9.1).
- **Duress/Löschen:** Verlasse dich nicht darauf. Das Löschen von Daten während einer erzwungenen Entsperrung kann in manchen Rechtsordnungen als Behinderung gewertet werden, und die Verweigerung eines Passcodes kann in manchen Rechtsordnungen selbst eine Straftat sein. [**Prüfen**](#verify-legal) Das Löschen von Daten nach einer rechtlichen Aufforderung oder in Erwartung einer Durchsuchung ist die riskanteste Handlung. Hole zuerst lokalen Rechtsrat ein.

### 10.3 Physische Maßnahmen

- **Verlasse dich nicht auf versteckte Dateien oder „gelöschte“ Daten** als Schutz.
- **Faraday-Beutel:** Die Freedom of the Press Foundation nennt sie als Option für den strengsten Standortschutz, wenn du ein Gerät nicht zurücklassen kannst. [**Extern**](#tag-external) Die FPF stellt ihn als letzte Möglichkeit dar und nennt keine Grenzen; ob ein Beutel wirkt, lässt sich kaum selbst prüfen. [**Empfehlung**](#tag-advice) Ein Faraday-Beutel behebt keine OPSEC-Fehler; er blockiert nur Funksignale, solange das Gerät darin liegt.
- Meide öffentliche USB-Ladeanschlüsse; nutze dein eigenes Ladegerät und Kabel.
- Lass das Gerät nie unbeaufsichtigt. War es außerhalb deiner Kontrolle, betrachte es als nicht vertrauenswürdig und prüfe die Auditor-Attestierung. [**Empfehlung**](#tag-advice)

**Verbleibendes Risiko:** Ein entschlossener Gegner mit physischer Kontrolle über ein entsperrtes oder nach dem ersten Entsperren befindliches Gerät kann trotzdem Erfolg haben. Reiseratschläge verringern die Exposition; sie garantieren keine Sicherheit.

---

## 11. Reaktion auf Vorfälle

Für jedes Szenario: Sofortmaßnahmen, was als kompromittiert gilt, was zu rotieren ist, was zu unterlassen ist und wann das Gerät nicht mehr genutzt werden sollte. Es handelt sich um [**Empfehlung**](#tag-advice), sofern nicht anders angegeben.

| Szenario | Sofortmaßnahmen | Als kompromittiert annehmen | Rotieren | Nicht tun | Gerät nicht mehr nutzen, wenn |
|---|---|---|---|---|---|
| **Gerät verloren** | Wenn möglich ausschalten; Zeit und Ort notieren; vertraute Kontakte auf anderem Weg informieren | Alles darauf, wenn das Geheimnis schwach oder das Gerät entsperrt war | Konten und Sitzungen, die darauf aktiv waren | Die Nummer des verlorenen Geräts nicht zum „Testen“ anrufen oder anschreiben; den Netzbetreiber bitten, die SIM zu sperren (eine SIM-PIN hilft); nicht annehmen, es sei gelöscht worden | es nicht zurückkommt oder nach unbekanntem Zugriff zurückkommt |
| **Gerät gestohlen** | Wie oben; ggf. melden | Alles darauf, auch zwischengespeicherte Nachrichten | Messenger-Sitzungen, Passwörter, 2FA-Seeds, Wiederherstellungscodes, die darauf lagen | Keine Vergeltung, keinen Kontakt zum Dieb | Immer (ersetzen) |
| **Verdacht auf Schadsoftware** | Sensible Nutzung stoppen; neu starten und aktualisieren; installierte Apps und Berechtigungen prüfen; saubere Neuinstallation erwägen | Das Profil und jedes darauf eingegebene oder angezeigte Geheimnis | Alles, was auf dem Gerät genutzt wurde | Nicht an Ort und Stelle „säubern“ und weiter nutzen | eine Neuinstallation die Symptome nicht beseitigt |
| **Verdächtige App** | Deinstallieren; Berechtigungen entziehen; prüfen, worauf sie zugegriffen hat | Daten, die die App erreichen konnte (Netzwerk, Kontakte, Speicher) | Alle Zugangsdaten, die eingegeben wurden, solange die App installiert war. | Nicht „zum Test“ neu installieren | sie weitreichenden Zugriff hatte, den du nicht ausschließen kannst |
| **Kontokompromittierung** | Überall abmelden; Passwort und 2FA von einem sauberen Gerät ändern; Sitzungen und verknüpfte Geräte widerrufen | Das Konto, seine Kontakte, sein Verlauf | Passwort, Wiederherstellungsdaten, 2FA-Seed | Das alte Passwort nicht wiederverwenden; den Wiederherstellungskontakt des Kontos nicht wiederverwenden | das Konto nicht wiederhergestellt werden kann |
| **SIM/eSIM-Kompromittierung** | Netzbetreiber kontaktieren (nach SIM-PIN und einer Sperre gegen Rufnummernmitnahme/SIM-Swap fragen); von einer Nummernübernahme ausgehen; Kontakte über einen anderen Kanal neu verifizieren; Signals Registrierungssperre (Registration Lock) erwägen [**Extern**](#tag-external) (eine PIN für die erneute Registrierung; Signal kann die PIN weder zurücksetzen noch wiederherstellen, und wer sie bei aktivierter Registrierungssperre vergisst, kann bis zu 7 Tage ausgesperrt sein; die Registrierungssperre läuft nach 7 Tagen Inaktivität ab; eine erneute Registrierung kann statt SMS einen Token plus die Signal-PIN nutzen, und Tokens werden durch eine neue Registrierung oder die Kontolöschung ungültig [**Extern**](#tag-external)) | Die Rufnummer und alles, was per SMS verifiziert wurde | Konten, die die Nummer für Wiederherstellung oder 2FA nutzen | Danach nicht auf SMS-2FA verlassen | du die Nummer nicht zurückerhältst |
| **Physische Beschlagnahme** | Wo das Recht es erlaubt, kannst du Antworten verweigern; Rechtshilfe suchen [**Prüfen**](#verify-legal) für dein Land; festhalten, was geschah | Das Gerät und alles darauf, auch wenn es zurückgegeben wird | Alle Konten und Geheimnisse, die darauf waren | Das Gerät nicht ohne vollständiges erneutes Flashen von einem vertrauenswürdigen Computer über den offiziellen Installer (Entsperren, Flashen, Sperren) weiterverwenden. Bei ausgeschalteter OEM-Entsperrung setzt das ein Gerät voraus, das noch startet und die Wiederaktivierung erlaubt; ist das nicht möglich, betrachte es als dauerhaft nicht vertrauenswürdig und ersetze es. Nie nach einem fehlgeschlagenen oder unvollständigen Flash sperren | Immer, außer du kannst die Integrität prüfen (Auditor, saubere Neuinstallation) und akzeptierst das Risiko |
| **Versehentliche Identitätsverknüpfung** | Stoppen; die verknüpfte Identität nicht mehr nutzen; auflisten, was offengelegt wurde | Die betroffene Identität und ihre Kontakte | Benutzernamen, E-Mail, Rufnummer, wo möglich | Keine Daten löschen, die für einen möglichen Rechtsfall relevant sind, ohne vorher Rechtsrat einzuholen [**Prüfen**](#verify-legal) | die Verknüpfung nicht aufgelöst werden kann |

> ⚠️ Nutze den Duress-Wipe nicht als allgemeines Werkzeug der Vorfallsreaktion. Er ist unumkehrbar. [**Offiziell**](#tag-official)

**Verbleibendes Risiko:** Du merkst womöglich nicht, dass ein Vorfall stattgefunden hat. Behandle unerklärliches Verhalten als Vorfall.

---

## 12. Useful websites / Nützliche Webseiten

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
| GrapheneOS-X-Beitrag, 13. Juni 2024 | <https://x.com/GrapheneOS/status/1801294115407106186> | GrapheneOS-Aussage, dass Forensik-Firmen Lösch-Apps wie Wasted und Sentry ausgenutzt haben | Abschnitt 4.5 | Aussage des Projekts, aber ein Social-Media-Beitrag, keine Dokumentation | Beiträge können bearbeitet oder gelöscht werden; nicht auf grapheneos.org |
| GrapheneOS-Forenthread „wasted-sentry“ | <https://discuss.grapheneos.org/d/28627-wasted-sentry> | Community-Diskussion zu Wasted und Sentry, einschließlich Berichten zur Zuverlässigkeit unter Android 15 | Abschnitt 4.5 | Nutzerinhalt, nicht offiziell | Beobachtung eines einzelnen Nutzers; hier nicht unabhängig getestet |
| privacygear.nl GrapheneOS-Härtungsleitfaden | <https://privacygear.nl/en/guides/grapheneos-hardening-guide/> | Einstellungs-Anleitung mit Menüpfaden (NFC) | Gegenprüfung von Menüpfaden | Sekundärquelle (geprüft am 05.11.2026, GrapheneOS 2026110200); keine offizielle GrapheneOS-Dokumentation | Pfade variieren je nach Version und Android-Version; es empfiehlt Orbot für Tor auf App-Ebene, wovon das offizielle GrapheneOS-Konto am 4. November 2024 abriet (und ein Maintainer bereits 2020 kritisierte) |
| Google Android-Hilfe: Lockdown | <https://support.google.com/android/answer/9075927?hl=en> | Dokumentiert, wie Lockdown aufgerufen wird und was es deaktiviert | Abschnitt 4.1 | Offizielle Google-Dokumentation zum Android-Verhalten; keine GrapheneOS-Dokumentation | Menübezeichnungen variieren je nach Android-Version und Gerät |
| Android-Entwicklerdokumentation: eSIM (eUICC-API) | <https://source.android.com/docs/core/connect/esim-euicc-api> | Beschreibt die EID als Kennung der eUICC-Hardware | Abschnitt „Eine separate Leitung einrichten“ | Offizielle Android-Plattformdokumentation; keine GrapheneOS-Dokumentation | Beschreibt die Plattform-API, nicht die Praxis der Netzbetreiber |
| Signal-Nutzungsbedingungen | <https://signal.org/legal/> | Verlangt Rechte an der zur Registrierung genutzten Rufnummer | Vor der Nutzung einer Zweit- oder virtuellen Nummer | Die eigenen Bedingungen von Signal | Sagt nichts Spezifisches zu virtuellen Nummern |

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
- [ ] Bluetooth, NFC und Standort aus; WLAN aus, solange es nicht für Kommunikation, Recherche, Updates oder App-Installation benötigt wird
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
- [ ] Private DNS ist global. Keinen Private-DNS-Hostnamen zusammen mit einem VPN konfigurieren; sobald irgendein Zweitprofil ein VPN nutzt, Private DNS global vollständig auf Aus stellen, wie GrapheneOS ausdrücklich empfiehlt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Dieser Leitfaden empfiehlt zusätzlich als strengere Autorenregel Aus bei jedem VPN [**Empfehlung**](#tag-advice). VPN-Kill-Switch geprüft.

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
- [ ] Lokale Regeln zu Gerätedurchsuchung und erzwungener Entsperrung kennen [**Prüfen**](#verify-legal)
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
- [ ] VPN-Entscheidung getroffen. Private DNS ist global. Keinen Private-DNS-Hostnamen zusammen mit einem VPN konfigurieren; sobald irgendein Zweitprofil ein VPN nutzt, Private DNS global vollständig auf Aus stellen, wie GrapheneOS ausdrücklich empfiehlt [**Offiziell**](#tag-official) (<https://grapheneos.org/faq#vpn-support>). Dieser Leitfaden empfiehlt zusätzlich als strengere Autorenregel Aus bei jedem VPN [**Empfehlung**](#tag-advice).
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
| „VPN = anonym“ | Ein VPN verschiebt das Vertrauen zum Anbieter. EFF: „A VPN is not a tool for anonymity“ [**Extern**](#tag-external) |
| „Tor = für alles sicher“ | Tor schützt nur dafür konfigurierte Apps, und Anmeldung oder Preisgabe von Details hebelt es aus [**Extern**](#tag-external). Das Projekt nennt die Sicherheit des Tor Browsers auf Android schwach [**Offiziell**](#tag-official) |
| „GrapheneOS = nicht verfolgbar“ | Netzbetreiber, WLAN-Betreiber und Dienste sehen weiterhin Ausschnitte deiner Aktivität |
| „Gelöschte Daten sind weg“ | Gelöschte Daten können in Backups, Caches und auf Geräten von Empfängern fortbestehen |
| „Ein verschlüsselter Messenger schützt vor einem kompromittierten Telefon“ | Ende-zu-Ende-Verschlüsselung schützt den Transport, nicht die Endpunkte |
| „Ein zweites Profil macht mich anonym“ | Profile teilen zugrunde liegende Hardware/Netzzugang, nicht zwingend Ausgangs-IPs (profilbezogene VPNs sind möglich). Gewohnheiten und wiederverwendete Konten können Identitäten weiterhin verknüpfen; keine Anonymitätsgarantie [**Empfehlung**](#tag-advice). |
| „Der Flugmodus macht ein Telefon ortungssicher“ | Er blockiert Standortdienste womöglich nicht, und Apps können gespeicherte Daten später senden; Ausschalten ist der stärkste verfügbare Schritt [**Extern**](#tag-external) |
| „Ein Faraday-Beutel löst OPSEC“ | Er blockiert Funk, solange er geschlossen ist; er behebt weder Konten noch Gewohnheiten noch ein kompromittiertes Gerät [**Empfehlung**](#tag-advice) |
| „Ein Wegwerf-Telefon ist automatisch anonym“ | Die EFF nennt Bedingungen, damit ein Wegwerf-Telefon überhaupt wirkt (keine Wiederverwendung von SIM oder Gerät, nicht zusammen mit dem normalen Telefon mitgeführt, keine Anrufe an dieselben Personen) [**Extern**](#tag-external); Standort- und Nummernkorrelation bleiben [**Empfehlung**](#tag-advice) |

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
| GrapheneOS-Installation, Entsperren/Sperren, Löschvorgänge, Grenzen des Secure Elements, Auto-Reboot, USB-C-Modi, Scopes, Berechtigungen, Private-DNS- und VPN-Hinweise, LTE-only, eSIM, Vanadium-Verhalten, Accrescent und PDF-Betrachter im App-Repository, Einstellung zur Zwischenablage im Private Space, Fehlen einer Fernlöschung | Gegen primäre GrapheneOS-Dokumentation und, wo verlinkt, gepinnten GrapheneOS-Projektquelltext geprüft (getrennte Evidenzarten; kein Test ausgelieferter APKs) [**Offiziell**](#tag-official) |
| EFF (einschließlich der Grenz-Checkliste von 2025), Tor Project, FPF (einschließlich Signalen bei ausgeschaltetem Gerät), RSF (Digital Security and Spyware Guide), Signal-Blog und Support-Artikel (einschließlich Backups, Sicherheitsnummern, Signal-PIN, Registrierungssperre und APK-Seite), HIBP, App-Lizenzen und -Quellen | Externe Herkunft: eigene Projektdokumentation/eigener Code ist primär für eigene Aussagen (einschließlich Signal, Android und Accrescent); Dokumentation und Projektquelltext sind getrennt. Weitere genannte Primärquellen wurden stichprobenartig geprüft; der NFC-Einstellungspfad ist zudem in den GrapheneOS-Release-Notes belegt [**Offiziell**](#tag-official) (<https://grapheneos.org/releases#2026050400>) [**Extern**](#tag-external) |
| Offene Prüfthemen: [versionsabhängige Pfade und ungeprüftes Build-Verhalten](#verify-menu-paths); [eSIM-/Daten-eSIM-Konto-, Ausweis- oder Zahlungspflichten](#verify-esim); [IMEI-Sichtbarkeit ohne SIM](#verify-imei); [SIM-Regeln und Neuvergabe virtueller Nummern](#verify-sim-rules); [Rechts- und Grenzregeln](#verify-legal) | Nur Notation, keine Anzahl einzelner Aussagen: [**Prüfen**](#tag-verify) |

*Bei einer offenen Aussage die passende Primärdokumentation oder den Projektquelltext und die genannten Grenzen heranziehen. Quellenlektüre ist kein Praxistest.*
