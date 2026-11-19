# Basisboard ESP32-S3: Pflichtenheft (Stand 2026-11-19, Entwurf)

Ablage: dieses Repo, Datei `docs/pflichtenheft.md`. Das Basisboard heisst im Funkfüürli bisher "Hauptplatine" (`docs/platine.md` im Funkfüürli-Repo). Gemeinsame Anforderungen des Geräts stehen in der Projektdefinition des Funkfüürli (Nummern F, G, H, T, L, O). Hier steht nur, was das Basisboard selbst können muss.

## 1. Zweck und Abgrenzung

* Das Basisboard trägt ESP32-S3, Display, Encoder, Strom und Audio. Das **Funkmodul** steckt über den Stecker **RX** auf (Funkfüürli: RX-Board mit Si4732, Wellenjäger: eigenes SDR-Modul).
* Es wird **für das Funkfüürli gebaut** (Kostenziel 30 bis 60 CHF, kleines Gehäuse). Der Wellenjäger nutzt dieselbe Hardware, bekommt aber nur Steckerpins, reservierte GPIOs und Reserve beim Regler. Wellenjäger-Bauteile kommen nicht aufs Basisboard.
* Firmware gehört nicht ins Basisboard-Repo, sie bleibt in den Projekt-Repos (verschieden lizenziert). Ein gemeinsamer Kern ist möglich, siehe Abschnitt 5.
* Bestellung erst nach bestandenem Lochraster-Test (Entscheid 2026-11-15).

## 2. Anforderungen

Priorität: **M** = muss, **S** = soll, **K** = kann.

| Nr | Anforderung | Prio | Bemerkung |
|---|---|---|---|
| BB1 | ESP32-S3-DevKitC-1 (N16R8) auf 2 Buchsenleisten 1x22, gedrehte Kontakte | M | Reihenabstand messen. Unter der Antennenfläche des Moduls kein Kupfer und keine Bauteile. USB-C am Rand, Ausschnitt im Gehäuse |
| BB2 | Stecker **RX** für das Funkmodul, 1x13, Belegung nach RX-Board-Pflichtenheft Abschnitt 4 | M | Kodierung, Pin 1 markiert. Rev A (1x9) bleibt steckbar. Name "RX" statt "J1", weil die ESP32-Leisten J1 und J3 heissen |
| BB3 | Display 2.0" ST7789V (SPI, 240x320) auf Stiftleiste | M | Backlight nur ein/aus über Transistor, kein PWM (T7) |
| BB4 | Drehencoder mit Taster, Entprell-RC | M | F2 |
| BB5 | Stromversorgung für 1 Zelle (3.0 bis 4.2 V). Pads für 14650-Halter und JST für LiPo 103665, nur einer bestückt | M | T5, O5 |
| BB6 | Hauptschalter, Verpolschutz mit Schottky 1N5819 in der Lastleitung, Pufferkondensator, Tiefentladeschutz | M | G6 |
| BB7 | LDO 3.3 V, mindestens 500 mA, kleine Dropout-Spannung, Ferrit am Ausgang zum Funkmodul. Einspeisung am 3V3-Pin des ESP32 (Regler des Moduls umgehen, Schutz gegen Rückspeisung über USB) | M | Entscheid 2026-11-15. MCP1700 (250 mA) reicht nicht. Kandidat LF33CV |
| BB8 | Laden: TP4056-Modul auf Stiftleiste, Laden und Hören nicht gleichzeitig (USB-Erkennung trennt die Last) | M | H5, T5 |
| BB9 | Audio: PAM8403-Modul (HW-012) auf Stiftleiste, Versorgung per GPIO schaltbar, Mono-Mischer mit 3-poligem Jumper (Radio-L oder Mischer) | M | T6. BTL-Ausgang, Lautsprecher-Minus nie an Masse |
| BB10 | 3.5-mm-Klinke mit Schaltkontakt, Line-Out stereo direkt vom Funkmodul | M | trennt den Lautsprecher beim Einstecken |
| BB11 | Lautstärkebegrenzung für Kopfhörer | M | G5, Lösung offen (Poti oder Software, O7) |
| BB12 | Steckplatz für optionales Bluetooth-Sendemodul mit Taster und Enable | K | F13, T6 |
| BB13 | Antennenanschlüsse: BNC, Teleskop, Ferritstab per Kabel zum RX-Board, am Platinenrand | M | Ferritstab nicht auf dem Basisboard, weit weg von Akku, Lautsprecher, ESP32, Display, Lader |
| BB14 | Messpunkte: 3V3, GND, Akku, Lastseite nach Schalter, Teiler-Ausgänge | M | Prototypmessungen (Strom, Spannung) |
| BB15 | Akku- und USB-Spannung über Teiler an ADC1 und GPIO. 5 V darf nie direkt auf einen ESP32-Pin gelangen | M | Pinplan, Prüfpunkt 6 |
| BB16 | Alles Durchsteckmontage oder fertige Module, kein SMD zum Löten | M | H2. Ein vorbestücktes Prüfstück für den Kursleiter (K5) |
| BB17 | Layout: Trennung von Lader, MCU, Audio/Bluetooth und Empfangsteil, durchgehende Massefläche, Funkmodul möglichst weit weg von ESP32, Display und Verstärker | M | T7, T8 |
| BB18 | Befestigung mit 4 M3 auf Abstandsbolzen. Die Platine trägt keine mechanischen Lasten | M | T10 |
| BB19 | Reserve für den Wellenjäger: I2S-Leitungen auf 4 reservierte GPIOs (RX Pins 10 bis 13) | M | Abschnitt 3. Beim Funkfüürli unbelegt |
| BB20 | Siebdruck: Bauteilnamen, Symbole, Revision, Jahr, `Copyright <Jahr> FerienBSD aka Marcel Sauder`, Repo-Link, kein Rufzeichen | M | H1 |
| BB21 | KiCad 9, 2 Lagen, Gerber im Repo, DRC vor jeder Bestellung | M | H1 |
| BB22 | Lizenz Hardware CERN-OHL-P-2.0, Doku CC-BY-4.0 | M | L1 |
| BB23 | Platinengrösse passt in das Funkfüürli-Gehäuse (höchstens ca. 180 x 120 mm Gehäuse) | S | Grösse offen, ergibt sich aus den Modulen |

## 3. Pinplan und Reserve

Stand Pinplan (`pinplan.md`, 2026-11-15): 19 belegte Pins, frei sind 15, 18, 38, 39, 47, 48. GPIO 38 oder 48 hängt je nach Modul an der RGB-LED des DevKits.

| Verwendung | GPIOs |
|---|---|
| Belegt (Funkfüürli) | 1, 2, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 16, 17, 21, 40, 41, 42 |
| **Vorschlag I2S-Reserve (Wellenjäger)** | 15, 18, 39, 47 (BCLK, WS, DIN, DOUT) |
| Danach noch frei | 38 und 48 (einer davon an der LED), davon höchstens 1 echt frei |

Folgen:
* Mit den 4 I2S-Reservepins bleibt kaum Platz. Der optionale **INT**-Pin des RX-Boards (RX Pin 8) und Notfall-Extras (F14) konkurrieren um den letzten freien GPIO.
* Ein Systemtakt (MCLK) für den Wellenjäger-Codec wäre ein fünfter Pin. Das Wellenjäger-Konzept hat das noch nicht geklärt.
* Der Fork des ATS-Mini nutzt eigene Pins. Wo er abweicht, wird entweder der Pinplan oder die Pindefinition im Fork angepasst (Pinplan, Prüfpunkt 2).

## 4. Strom

* Akku 3.0 bis 4.2 V, Schottky verliert etwa 0.3 V (messen). Die Mindestspannung am Si4732 ist 2.7 V. Der LDO braucht deshalb eine kleine Dropout-Spannung, sonst bricht das 3.3-V-Netz schon bei teilentladenem Akku ein.
* Der LDO muss die WLAN-Spitzen des ESP32 liefern (Entscheid 2026-11-15: mindestens 500 mA).
* Strombudget des Funkfüürli vor der LDO-Wahl messen (Breadboard-Stufe, Prototyp Schritt 7): ESP32 mit und ohne WLAN, Display, Si4732, Verstärker.
* **Wellenjäger-Reserve:** Der Analogteil (Si5351, Codec, DAC) bringt Zusatzstrom, der heute unbekannt ist. Entweder bleibt er unter der Reserve des 500-mA-LDO, oder das Wellenjäger-Modul bringt einen eigenen, rauscharmen Regler mit. Entscheid in der Wellenjäger-Entwicklung, nicht jetzt.

## 5. Firmware (Hinweis)

* Pro Projekt eine Firmware: Funkfüürli aus dem ATS-Mini-Fork (MIT), Wellenjäger aus easysdr (GPL-3.0).
* Ein gemeinsamer Kern (Display, Encoder, Strom, Audio, Watchdog) ist möglich, wenn er **unter MIT oder eigener Lizenz** steht: Ein GPL-Projekt darf MIT-Code übernehmen, ein MIT-Projekt darf GPL-Code nicht übernehmen. Der Kern darf also keinen GPL-Code enthalten.
* Die Pinbelegung als kleine Datei (z.B. `pins.h`) im Basisboard-Repo, die beide Firmwares einbinden, hält Hardware und Software synchron.
* Die Firmware erkennt das Funkmodul optional selbst: Der Si4732 antwortet im I2C auf Adresse 0x11, der Si5351 des Wellenjäger auf einer anderen.

## 6. Offene Punkte

| Nr | Punkt | Stand |
|---|---|---|
| Q1 | Repo `Funkbasis-ESP32`, Sprache Deutsch (festgelegt 2026-11-19) | erledigt |
| Q2 | Stecker RX: 1x13 gegenüber Rev A mit 1x9, Lage der Leiste und Kodierung | offen |
| Q3 | I2S-Reservepins 15, 18, 39, 47 bestätigen, MCLK ja oder nein, INT-Pin des RX-Boards | offen |
| Q4 | Strombudget messen, LDO-Typ festlegen (Datenblatt LF33CV), Wellenjäger-Reserve klären | offen |
| Q5 | Reihenabstand der ESP32-Leisten messen, Pins 13 und 14 gegen Multimeter prüfen (Beschriftung des Clones) | offen |
| Q6 | Display: Pinbelegung und Masse | offen |
| Q7 | Module HW-012 (PAM8403) und TP4056: Masse und Pinreihenfolge | offen |
| Q8 | Anschluss des 14650-Halters (Lötfahnen oder Drähte, Kontaktabstand) | offen |
| Q9 | Ferritstab: Typ und Länge (Rev B des RX-Boards) | offen |
| Q10 | Schaltung der Verstärker-Versorgung (GPIO 5): High-Side-Schalter in THT, der mit 3.3 V sicher schaltet | offen |
| Q11 | Lautstärke: Poti am Modul oder per Software (O7 der Projektdefinition) | offen |
| Q12 | Pins mit dem ATS-Mini-Fork abgleichen | offen |
| Q13 | Platinengrösse und Lage der Anschlüsse zum Gehäuse | offen, nach Q5 bis Q8 |

*Copyright FerienBSD aka Marcel Sauder. Doku unter CC-BY-4.0.*
