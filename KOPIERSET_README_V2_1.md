# KOPIERSET_README_V2_1

## Zweck

Dies ist der operative Startsatz fuer ein neues reales Vorhabensprojekt.
Nur diese Dateien in ein neues Vorhabensprojekt uebernehmen.

## Vorgehen

1. Neues Vorhabensprojekt anlegen
2. Project Instructions aus `PROJEKTHINWEISE_VORHABENPROJEKT_V2_1.md` einsetzen
3. restliche Dateien und Basisverzeichnisse uebernehmen
4. HERMES-Szenario, Vorgehensweise und Tailoring in `HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1.md` festhalten
5. dann mit `STARTPROMPT_NEUES_VORHABEN_V2_1.md` starten

Im Routinebetrieb gilt danach:
- zuerst `steering/PROJEKTSTATUSBERICHT.md` lesen
- danach nur das direkt betroffene Artefakt oder Ergebnis lesen
- ganze Ordner nur bei echtem Ausnahmegrund lesen

## Mitgelieferte Grundstruktur

Relativ zum Arbeitsverzeichnis enthaelt das Template:

- `/src/` fuer Quellcode
- `/extsrc/` fuer externe Informationsquellen, nur lesen
- `/docs/` fuer HERMES-Ergebnisraeume und weitere Projektdokumentation
- `/steering/` fuer HERMES-Governance-Dokumente

## HERMES-Basissatz

Der Kopiersatz liefert bewusst einen schlanken, aber verbindlichen HERMES-Kern mit:

- Initialisierung unter `steering/01_INITIALISIERUNG/`
- phasenuebergreifendem Reporting unter `steering/`
- parallelen Entstehungspfad-Markern fuer klassisch und agil
- Abschlussartefakten unter `steering/05_ABSCHLUSS/`
- lokaler Aktivierungsdatei `HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1.md`

## Nicht uebernehmen

Keine Live-Dateien aus `10_LIVE_STANDARD/` zusaetzlich hochladen.
Keine Release-Vorlagen oder Freeze-Dokumente in das Vorhabensprojekt ziehen.

## Herkunft

Dieser Kopiersatz basiert auf dem ab `V2_0` geltenden HERMES-Kern und dem in `V2_1` nachgeschaerften minimalen Lesepfad.
