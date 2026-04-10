# HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1

## Zweck

Diese lokale `_ROO`-Datei dokumentiert die Aktivierung des HERMES-Vorhabens im konkreten Projekt.
Sie ersetzt keine HERMES-Kernartefakte, sondern steuert deren lokale Anwendung.

## Pflichtentscheidungen zu Projektbeginn

- HERMES-Szenario: IT-Entwicklung
- Vorgehensweise: agil
- Projektwertigkeit / Sizing-Annahme: mittel; funktional konservative Modernisierung einer bestehenden IT-Loesung mit architektur-, betriebs- und sicherheitsrelevanten Anpassungen bei begrenztem Nutzerkreis
- Tailoring-Annahmen:
  - Phase Initialisierung und Phase Abschluss bleiben HERMES-gemaess klassisch gefuehrt; nur die Loesungsentstehung wird agil ausgerichtet.
  - Das Standardszenario IT-Entwicklung ist die Basis, weil eine bestehende IT-Loesung weiterentwickelt und technisch wie organisatorisch integriert wird; eine formale Beschaffung steht nicht im Zentrum.
  - Der fachliche Kern der bestehenden Anwendung bleibt gemaess `docs/ZIELBILDER_WEITERES_VORGEHEN.md` erhalten; ersetzt werden primaer Claude-gebundene Runtime-, Betriebs- und Sicherheitsmechanismen.
  - Das heutige Shell-/Subagent-Modell ueber `claude -p` wird nicht fortgeschrieben, sondern spaeter durch ein internes Job-/Worker-Modell ersetzt.
  - Beschaffung wird fuer Release 1 nicht aktiviert, weil keine formale Marktbeschaffung einer Loesung geplant ist; die vorhandene Codebasis wird angepasst.
  - IT-Migration wird initial nicht aktiviert, solange keine eigenstaendige Daten- oder Altsystemmigration als gesonderter Loesungsgegenstand bestaetigt ist.
  - Das Produkt-Modul wird initial nicht aktiviert; Release 1 fokussiert auf das IT-System, seinen Betrieb und die sichere technische Ueberfuehrung.
  - ISDS, IT-Betrieb und Tests werden frueh mitgefuehrt, weil self-hosted Betrieb, Providerwechsel und Hardening den Projekterfolg praegen.
- Releasefreigabe vorgeschrieben: ja; bei agiler Loesungsentstehung soll jede nutzbare Release-Stufe vor Weiterarbeit explizit gegen Funktionsfaehigkeit, Sicherheitsgrenzen und Betriebsreife bewertet werden

## Zu aktivierende HERMES-Module

- Pflichtmodule:
  - Projektsteuerung
  - Projektfuehrung
  - Projektgrundlagen
  - Einfuehrungsorganisation
- Zusatzmodule:
  - Organisation
  - IT-System
  - Tests
  - IT-Betrieb
  - ISDS
- nicht aktiviert mit Begruendung:
  - Beschaffung; keine formale Beschaffung im Scope von Release 1
  - IT-Migration; derzeit keine bestaetigte separate Daten- oder Legacy-Migration
  - Produkt; keine eigenstaendige Dienstleistungs- oder Produktneuentwicklung im Scope von Release 1

## Zu materialisierende Zusatzdokumente

- sofort nachziehen:
  - `steering/01_INITIALISIERUNG/PROJEKTINITIALISIERUNGSAUFTRAG.md`
  - `steering/01_INITIALISIERUNG/ENTSCHEID_WEITERES_VORGEHEN.md`
  - `docs/ZIELBILDER_WEITERES_VORGEHEN.md`
- spaeter nachziehen:
  - `steering/PROJEKTMANAGEMENTPLAN.md`
  - `steering/DURCHFUEHRUNGSAUFTRAG.md`
  - `steering/RELEASEBERICHT.md`
- bewusst nicht jetzt anlegen:
  - Beschaffungsartefakte wie Ausschreibung, Zuschlag oder Evaluationsbericht
  - klassische Artefakte der Phasen Konzept, Realisierung und Einfuehrung, solange der Entscheid fuer agile Loesungsentstehung gilt
  - Abschlussartefakte vor Durchfuehrungsfreigabe

## Lokale Roo-Erweiterungen

- benoetigte `_ROO`-Artefakte:
  - `HERMES_TAILORING_UND_AKTIVIERUNG_ROO_V2_1.md`
  - `QUALITAETSGATE_VORHABENPROJEKT_ROO_V2_1.md`
- besondere Handoff-Regeln:
  - Jede dauerhafte Uebergabe muss Phase, Szenario, Vorgehensweise sowie betroffene HERMES- und `_ROO`-Artefakte benennen.
  - Architektur- und Sicherheitsannahmen muessen gegen `docs/ZIELBILDER_WEITERES_VORGEHEN.md` gespiegelt werden.
  - Keine Codefreigabe vor sponsor-seitig verdichtetem Entscheid `Weiteres Vorgehen`.
- besondere Sicherheitsrahmen-Hinweise:
  - Keine stillschweigende Uebernahme des bisherigen Remote-Updaters aus `update-system.mjs` in den Zielbetrieb.
  - Keine Fortfuehrung privilegierter Batch-Mechanik ueber `claude -p` im Zielbetrieb.
  - Geheimnisse duerfen nicht in Projektdateien abgelegt werden; Betriebssecrets sind spaeter getrennt zu fuehren.

## Merksatz

HERMES bleibt kanonisch.
Diese Datei dient nur der lokalen Aktivierung und Bedienung.
