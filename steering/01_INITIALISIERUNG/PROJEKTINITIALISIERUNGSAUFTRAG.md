# PROJEKTINITIALISIERUNGSAUFTRAG

## Zweck

Formaler Start der Phase Initialisierung gemaess HERMES.

## Status

- Dokumentstand: sponsor-ready Entwurf
- Formale Freigabe durch menschliche HERMES-Rolle: ausstehend
- HERMES-Abgrenzung: Dieser Entwurf bereitet die formale Initialisierung vor; lokale Roo-Rollen ersetzen keine HERMES-Freigabe

## Ausgangslage

- Mit `career-ops` liegt eine lauffaehige Anwendung vor, deren fachlicher Kern bewusst weitgehend erhalten bleiben soll.
- Das Vorhaben zielt nicht auf eine fachliche Neuerfindung, sondern auf die kontrollierte Ueberfuehrung in ein provider-flexibles und self-hosted Betriebsmodell gemaess `docs/ZIELBILDER_WEITERES_VORGEHEN.md`.
- Im Zentrum stehen drei Veraenderungen:
  - Wegfall der Claude-Code- und `claude -p`-Abhaengigkeiten
  - OpenAI als erster produktiver Provider bei provider-neutraler Zielarchitektur
  - self-hosted Betrieb per Docker Compose mit explizitem Hardening

## Ziele

- Die HERMES-Initialisierung so weit verdichten, dass der Entscheid `Weiteres Vorgehen` belastbar getroffen werden kann.
- Szenario, Vorgehensweise, Projektwertigkeit und Tailoring nachvollziehbar festlegen.
- Die Voraussetzungen schaffen, um danach den Projektmanagementplan und den Durchfuehrungsauftrag sauber abzuleiten.

## Ziele der Phase Initialisierung

- die Zielbilder des kuenftigen Systems final als Entscheidungsgrundlage verankern
- die bevorzugte Loesungsvariante gegen Alternativen absichern
- das fuer die Loesungsentstehung passende HERMES-Szenario bestimmen
- klassisch oder agil fachlich und vorgehenstechnisch begruendet festlegen
- Sicherheits-, Betriebs- und Organisationsrisiken frueh sichtbar machen

## Rahmenbedingungen

- funktional konservative Modernisierung; kein Produktneubau
- self-hosted Zielbetrieb; kein zentrales SaaS-Ziel in Release 1
- OpenAI als erster produktiver Provider; provider-neutrale Architektur als Leitplanke
- Human-in-the-loop bleibt verbindlich
- kein versteckter Integrationsausbau zu CRM, Mail oder Kalender in Release 1

## Ressourcenbedarf

- benoetigt werden in der Initialisierung mindestens:
  - ein menschlicher Entscheider fuer die formale HERMES-Freigabe
  - sponsor-seitige Verdichtung und Review
  - architektonische Klaerung des Zielbetriebsmodells
- Budget-, Termin- und Detailressourcen fuer die Loesungsentstehung werden erst nach dem Entscheid `Weiteres Vorgehen` konkretisiert

## Projektorganisation und Kommunikation

- lokale Roo-Sicht:
  - `SPONSOR` als Standard-SPOC fuer Verdichtung und Entscheidungsaufbereitung
  - `ARCHITECT` fuer Struktur-, Betriebs- und Sicherheitszielbild
- HERMES-seitig bleiben Auftraggeber, Projektleiter und Anwendervertreter menschlich zu besetzen bzw. formell zu bestaetigen
- Reporting erfolgt bis auf Weiteres ueber `steering/PROJEKTSTATUSBERICHT.md`

## Risiken der Initialisierung

- versteckte Claude-Annahmen in bestehenden Artefakten koennen den Migrationsaufwand erhoehen
- Sicherheitsrelevanz von Self-Update, Shell-Aufrufen und privilegierten Batch-Mechanismen kann die Zielarchitektur beeinflussen
- Modell- und Qualitaetsunterschiede zwischen Claude und OpenAI koennen zu fachlichen Nacharbeiten fuehren
- ungeklaerte Betriebsdetails koennen spaeter Tailoring oder Projektwertigkeit verschieben

## Erwartete Ergebnisse der Phase Initialisierung

- `docs/ZIELBILDER_WEITERES_VORGEHEN.md`
- `HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1.md`
- `steering/01_INITIALISIERUNG/ENTSCHEID_WEITERES_VORGEHEN.md`
- anschliessend als Folgeartefakte: `steering/PROJEKTMANAGEMENTPLAN.md` und `steering/DURCHFUEHRUNGSAUFTRAG.md`

## Sponsor-Hinweis

- Dieser Stand ist entscheidungsreif fuer die weitere Initialisierung, aber noch keine formale HERMES-Freigabe.
