# ENTSCHEID_WEITERES_VORGEHEN

## Zweck

Formale Verdichtung des Entscheids ueber das weitere Vorgehen nach der Initialisierung.

## Status

- Entscheidungsstand: sponsor-ready Entwurf
- Formale HERMES-Entscheidung: ausstehend
- Bezugsgrundlagen:
  - `docs/ZIELBILDER_WEITERES_VORGEHEN.md`
  - `HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1.md`
  - `extsrc/Hermes/HERMES-Projektmanagement.pdf`

## Kernbefund

- Die bestehende Anwendung soll nicht fachlich neu erfunden werden, sondern als funktional konservative Modernisierung weitergefuehrt werden.
- Der fachliche Kern bleibt erhalten; ersetzt werden vor allem Claude-gebundene Runtime-, Batch- und Betriebsannahmen.
- Das Ziel ist ein provider-flexibler, self-hosted und Docker-Compose-faehiger Betrieb mit OpenAI als erstem produktiven Provider.
- Sicherheitsseitig liegt keine belegte Malware-Feststellung vor; jedoch besteht klarer Hardening-Bedarf bei privilegierten Batch-Mechanismen, Shell-Ausfuehrung und Self-Update.

## Entscheid

- Projektfortsetzung: ja
- bevorzugte Loesungsvariante: bestehende Anwendung funktional konservativ modernisieren
- HERMES-Szenario: IT-Entwicklung
- Vorgehensweise fuer die Loesungsentstehung: agil
- Projektwertigkeit / Sizing-Annahme: mittel
- Releasefreigabe in agiler Loesungsentstehung: ja

## Begruendung des Entscheids

### Warum IT-Entwicklung

- HERMES sieht das Szenario IT-Entwicklung fuer Projekte vor, in denen eine bestehende IT-Loesung weiterentwickelt und technisch wie organisatorisch integriert wird; genau dies trifft auf den Zielzustand zu.
- Das Szenario IT-Adaption wuerde eine Beschaffungslogik in den Vordergrund ruecken. Diese ist fuer Release 1 nicht leitend.

### Warum agil

- Die fachliche Richtung ist stabil, aber technische Risiken und Unsicherheiten bleiben hoch: Providerwechsel, Ersatz der bisherigen Runtime, Compose-Betrieb, Hardening und moegliche Qualitaetsunterschiede zwischen Modellen.
- Diese Unsicherheiten lassen sich besser ueber nutzbare, pruefbare Inkremente steuern als ueber eine einmalige Durchplanung bis in die Umsetzung.
- Die Wahl ist damit fachlich und vorgehenstechnisch begruendet und folgt nicht bloss einem Trend.

### Warum Releasefreigabe ja

- Jede technische Release-Stufe kann Funktionsfaehigkeit, Sicherheitsgrenzen und Betriebsreife wesentlich beeinflussen.
- Darum soll in der agilen Loesungsentstehung jede Release-Stufe bewusst freigegeben werden, bevor der naechste Inkrement-Schnitt beginnt.

## Freizugebender Scope der Loesungsentstehung

### In Scope

- provider-neutrale Runtime mit OpenAI als erstem produktiven Adapter
- Ersatz der bisherigen Claude-CLI-Kopplung
- Ersatz des bisherigen Batch-Modells ueber `claude -p`
- self-hosted Zielbetrieb auf Docker Compose
- Trennung von Core, Worker, Browser/Rendering und optionalem Dashboard gemaess `docs/ZIELBILDER_WEITERES_VORGEHEN.md`
- Hardening der heute bekannten Risikooberflaechen

### Nicht Ziel von Release 1

- neue Produktdomaenen ausserhalb des heutigen Job-Operations-Kerns
- CRM-, Mail- oder Kalender-Integration
- grosser UI-Neubau
- Multi-Tenant-SaaS-Betrieb
- finale Sicherheitsentwarnung ohne weitergehende Evidenz

## Risiken und offene Punkte

- Die Ergebnisqualitaet kann sich durch den Wechsel von Claude zu OpenAI veraendern.
- Vorhandene Modus- und Prompt-Artefakte koennen implizite Claude-Annahmen enthalten.
- Dateibasierte Persistenz bleibt fuer Release 1 nur tragfaehig, wenn Schreibkonflikte sauber begrenzt werden.
- Der Sicherheitsbefund bleibt vorlaeufig; eine weitergehende Security-Pruefung ist spaeter separat einzuplanen.

## Folgerungen fuer die naechsten HERMES-Ergebnisse

- Der Entscheid `Weiteres Vorgehen` bildet die Grundlage fuer die Fortschreibung des `steering/PROJEKTMANAGEMENTPLAN.md` und anschliessend des `steering/DURCHFUEHRUNGSAUFTRAG.md`.
- Bei agiler Loesungsentstehung ist der spaetere `steering/RELEASEBERICHT.md` als zentrales Fuehrungsartefakt einzuplanen.
- Architektur- und Sicherheitsentscheidungen sind weiter gegen `docs/ZIELBILDER_WEITERES_VORGEHEN.md` zu pruefen.

## Sponsor-Empfehlung

- Das Vorhaben soll als funktional konservative Modernisierung mit Szenario IT-Entwicklung und agiler Loesungsentstehung weitergefuehrt werden.
- Die Weiterarbeit soll erst nach Fortschreibung der Initialisierungsdokumente und anschliessender sponsor-seitiger Pruefung in execution-nahe Pakete uebergehen.
