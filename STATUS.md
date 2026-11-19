# Status Funkbasis-ESP32

Höchstens 30 Zeilen. Immer überschreiben, nicht anhängen. Erledigtes streichen.

## Stand (2026-11-19)
- Pflichtenheft liegt in docs/pflichtenheft.md (Entwurf).
- Noch keine KiCad-Datei, kein Pinplan in diesem Repo, keine Hardware.

## Als Nächstes
- Vorschlag: Pinplan aus dem Funkfüürli-Repo übernehmen und gegen Stecker RX prüfen (Q3).
- Vorschlag: Strombudget im Breadboard-Test messen, LDO festlegen (Q4).
- Vorschlag: offene Punkte Q2 bis Q13 im Pflichtenheft klären.

## Entscheide (Marcel Sauder)
- Eine Basisplatine für Funkfüürli und Wellenjäger, Funkmodul über Stecker RX (2026-11-19).
- Gebaut für das Funkfüürli, keine Wellenjäger-Bauteile auf der Basis (2026-11-19).
- Reserve: 4 GPIOs für I2S im Stecker RX, auf dem Funkfüürli unbelegt (2026-11-19).
- Firmware bleibt in den Projekt-Repos (2026-11-19).
- Repo-Name Funkbasis-ESP32, Dokumentation Deutsch (2026-11-19).
- Bestellung erst nach bestandenem Lochraster-Test (2026-11-15).

## Stolpersteine
- Freie GPIOs sind knapp: mit der I2S-Reserve bleibt höchstens 1 Pin frei.
- RX-Board Rev A hat 1x9 und kein KW, Rev B kommt erst nach den Rev-A-Tests.
