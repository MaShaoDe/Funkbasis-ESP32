# Funkbasis-ESP32: Basisplatine für Funkgeräte

[Deutsch](README.md) | [English](README.en.md)

*Eine Platine, verschiedene Funkmodule.*

**Stand: Pflichtenheft (Entwurf).** Es gibt noch keine Hardware und keine Firmware. Alles, was bisher entschieden ist, steht in [docs/pflichtenheft.md](docs/pflichtenheft.md).

## Was ist das?

Die Funkbasis ist die gemeinsame Basisplatine für Funkgeräte mit ESP32-S3. Sie trägt alles, was jedes dieser Geräte braucht. Das Funkmodul steckt über den Stecker RX auf. Welches Modul steckt, entscheidet, welches Gerät daraus wird.

* **Steuerung:** ESP32-S3-DevKitC-1 (N16R8) auf Buchsenleisten. Das Modul bleibt wiederverwendbar.
* **Bedienung:** Display 2.0" ST7789V (240x320) und Drehencoder mit Taster.
* **Strom:** 1 Zelle (14650 oder flacher LiPo), Linearregler, Verpolschutz, Hauptschalter, Laden über USB-C mit linearem Ladechip. Kein Schaltregler, damit MW und KW ruhig bleiben.
* **Audio:** Verstärker PAM8403 (Modul), Lautsprecher, 3.5-mm-Klinke mit Schaltkontakt, Line-Out, Steckplatz für ein Bluetooth-Sendemodul (optional).
* **Funkmodul:** Stecker RX mit I2C, Reset, Ton links und rechts, 3.3 V, plus reservierte I2S-Leitungen.

Die Firmware gehört nicht in dieses Repo. Sie liegt in den Projekt-Repos, weil sie je Gerät anders ist und anders lizenziert ist.

## Geräte auf dieser Basis

| Gerät | Funkmodul | Repo |
|---|---|---|
| Funkfüürli (Notfallradio für Kinder, UKW, MW, KW) | RX-Board mit Si4732 | [Funkfuerli](https://github.com/MaShaoDe/Funkfuerli), [RX-Board-Si4732](https://github.com/MaShaoDe/RX-Board-Si4732) |
| Wellenjäger (Ham-SDR für Prüfungskandidaten) | eigenes SDR-Modul, später | [Wellenjaeger](https://github.com/MaShaoDe/Wellenjaeger) |

Die Basis wird für das Funkfüürli gebaut (Kostenziel 30 bis 60 CHF pro Bausatz). Der Wellenjäger nutzt dieselbe Hardware über den Stecker RX, die reservierten Pins und Reserve beim Regler. Bauteile, die nur der Wellenjäger braucht, kommen nicht auf die Basis.

Wer ein eigenes Funkgerät mit ESP32 bauen will, kann die Platine forken oder nachbauen und ein eigenes Funkmodul auf den Stecker RX setzen.

## Ordner

| Ordner | Inhalt |
|---|---|
| `docs/` | Pflichtenheft |
| `hardware/` | KiCad-9-Projekt, Gerber, Bestückungsdaten (folgt) |
| `LICENSES/` | Lizenztexte |

## Plan

- [x] Pflichtenheft (Entwurf)
- [ ] Offene Punkte klären (Q2 bis Q13 im Pflichtenheft)
- [ ] Pinplan übernehmen und gegen Stecker RX, Display und Fork prüfen
- [ ] Breadboard-Test und Lochraster-Prototyp (im Projekt Funkfüürli)
- [ ] Schaltplan und Layout in KiCad 9
- [ ] Bestellung erst nach bestandenem Lochraster-Test

## Lizenz

Hardware CERN-OHL-P-2.0, Dokumentation CC-BY-4.0. Siehe [LICENSE.md](LICENSE.md).

73 de Marcel (MaShaoDe)
