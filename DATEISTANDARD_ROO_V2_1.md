# DATEISTANDARD_ROO_V2_1

## Grundregeln

- Dateinamen in GROSSBUCHSTABEN
- Woerter mit `_` trennen
- keine Leerzeichen
- keine Umlaute im Dateinamen
- keine unnoetigen Versionsnummern ausser bei Releases
- Dateiname soll Art, Zweck, Projekt und ggf. Zielrolle klar zeigen

## Verzeichniskonvention fuer generische Vorhabenprojekte

Relativ zum Arbeitsverzeichnis gilt standardmaessig:

- `/src/` enthaelt Quellcode.
- `/extsrc/` enthaelt externe Informationsquellen; dort nur lesen, niemals schreiben.
- `/docs/` enthaelt HERMES-Ergebnisraeume und weitere Projektdokumentation.
- `/steering/` enthaelt HERMES-Governance-Dokumente.

## HERMES-Kern

HERMES-native Projektergebnisse tragen HERMES-Begriffe und **kein** `_ROO`.

## LOCAL_ROO

Lokale Roo-Erweiterungen bleiben sichtbar markiert.

## HERMES-Struktur unter `/steering/`

- `01_INITIALISIERUNG/`
- klassisch: `02_KONZEPT/`, `03_REALISIERUNG/`, `04_EINFUEHRUNG/`
- agil: `02_UMSETZUNG/`
- `05_ABSCHLUSS/`

## Routine-Lesepfad

Im Routinefall zuerst `steering/PROJEKTSTATUSBERICHT.md` lesen und danach nur das direkt betroffene Artefakt.

## Zusatzregel fuer Versionen

Nur eingefrorene Releases und deren Kopiersaetze tragen `VX_Y`.
