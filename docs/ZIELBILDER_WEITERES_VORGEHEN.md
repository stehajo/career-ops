# Architektur-Zielbilder fuer `career-ops`

## 1. Zweck und Entscheidungsbezug

Dieses Dokument beschreibt sponsor-taugliche Zielbilder fuer das weitere Vorgehen mit der bestehenden Anwendung `career-ops`.

Es dient als Grundlage fuer den Entscheid zum weiteren Vorgehen in der HERMES-Initialisierung und beantwortet insbesondere diese Leitfragen:

- Wie bleibt der fachliche Kern weitgehend erhalten?
- Wie wird die heutige Claude-Kopplung ersetzt, ohne die Produktlogik auszuweiten?
- Wie sieht ein provider-flexibles, self-hosted und Docker-Compose-faehiges Zielbetriebsmodell aus?
- Welche Sicherheitsgrenzen und welches Hardening sind fuer Release 1 erforderlich?

## 2. Scope und verbindliche Leitplanken

### In Scope

- funktionaler Kern der heutigen Anwendung bleibt moeglichst gleich:
  - Angebotsbewertung
  - PDF-Erzeugung
  - Portal-Scan
  - Batch-Verarbeitung
  - Tracker-/Pipeline-Pflege
- provider-flexibler Betrieb mit OpenAI als erstem Zielprovider
- Entkopplung von Claude Code und `claude -p`
- self-hosted Betrieb per Docker Compose
- Sicherheits- und Betriebszielbild fuer bekannte Hardening-Flaechen

### Nicht-Ziele von Release 1

- keine funktionale Produktausweitung ueber den heutigen Kern hinaus
- keine CRM-, Mail- oder Kalender-Integration ausser moeglichen Platzhaltern oder klaren Schnittstellenpunkten
- kein autonomes Abschicken von Bewerbungen
- keine Kubernetes-Zielarchitektur
- keine Malware-Entwarnung oder Sicherheitsfreigabe ohne weitergehende Evidenz

## 3. Befund aus der bestehenden Anwendung

### 3.1 Was heute fachlich bereits tragfaehig ist

Die vorhandene Anwendung hat einen klaren fachlichen Kern, der weiterverwendbar ist:

- AI-gestuetzte Bewertung von Stellenangeboten
- Erzeugung individualisierter CV-/PDF-Artefakte
- Dateibasierter Tracker als Single Source of Truth
- Batch-Verarbeitung und Scan-Logik
- Mensch-in-der-Schleife als bewusste Produktgrenze

Dieser Kern ist fuer Release 1 nicht neu zu erfinden, sondern in ein anderes Betriebs- und Ausfuehrungsmodell zu ueberfuehren.

### 3.2 Was heute strukturell gekoppelt ist

Die aktuelle Runtime ist deutlich an Claude-spezifische Mechanismen gekoppelt:

- Interaktion ueber Claude Code als primaeren Laufzeitkontext
- Instruktions- und Bedienmodell in `CLAUDE.md`
- Batch-Orchestrierung ueber Shell-Skript und `claude -p`
- lokale Setup-Pruefung mit Erwartung eines lokalen CLI-/Dateisystem-Betriebs
- Update-Mechanismus mit Remote-Fetch und Git-Checkout auf dem Zielsystem

### 3.3 Sicherheitsrelevante Befunde

Aus Sponsor-Sicht sind insbesondere diese Mechanismen relevant:

- privilegiert wirkende Batch-Worker-Mechanik mit Shell-Prozesssteuerung
- Updater mit Remote-Fetch und Git-Checkout auf dem Produktivsystem
- Shell-Ausfuehrung als technisches Mittel fuer Kernablaufe

Wichtig: Diese Befunde belegen keine Malware. Sie begruenden jedoch einen plausiblen Hardening-Bedarf und muessen im Zielbild als Angriffs- und Missbrauchsflaechen behandelt werden.

## 4. Zielbild 1 - fachlich-betriebliches Zielbild des kuenftigen Systems

### 4.1 Zielaussage

`career-ops` bleibt ein lokal bzw. self-hosted betriebenes, AI-gestuetztes Job-Operations-System fuer eine Einzelperson oder einen kleinen, vertrauten Nutzerkreis.

Der fachliche Kern bleibt erhalten:

- Stellenangebote erfassen oder scannen
- Angebote bewerten
- CV-/PDF-Artefakte erzeugen
- Batch-Laeufe ausfuehren
- Tracking- und Statusdaten konsistent halten

Neu ist nicht das Produktversprechen, sondern das Betriebsmodell:

- kein Claude-Code-Zwang
- kein lokaler `claude`-CLI-Zwang
- Betrieb als self-hosted Compose-Stack
- Anbindung an einen austauschbaren LLM-Provider, zunaechst OpenAI

### 4.2 Ziel-Betriebsmodell

Das kuenftige System wird als betreiberkontrollierter Compose-Stack bereitgestellt.

Charakteristika:

- der Betreiber fuehrt den Stack auf eigener Infrastruktur oder auf einem selbst kontrollierten Host aus
- persoenliche Daten, Reports, Tracker und generierte Dateien liegen in persistenten, lokal kontrollierten Volumes
- nur fuer benoetigte Faelle besteht ausgehender Verkehr zu:
  - OpenAI als erstem Zielprovider
  - Zielwebseiten / Jobportalen fuer Scan und Extraktion
- es gibt kein Produktziel eines zentral gehosteten SaaS-Dienstes in Release 1

### 4.3 Fachliche Leitplanken, die bewusst bleiben

- Mensch-in-der-Schleife bleibt verbindlich
- keine automatische Bewerbungseinreichung
- dateibasierte Arbeitsweise darf in Release 1 bleiben, solange Konsistenz und Sperrmechanismen sauber geregelt sind
- bestehende Bewertungs- und Artefaktlogik wird konservativ uebernommen, nicht fachlich neu designt

### 4.4 Was bleiben kann / was ersetzt werden muss / was nicht Ziel von Release 1 ist

| Bereich | Kann bleiben | Muss ersetzt oder neu gerahmt werden | Nicht Ziel von Release 1 |
|---|---|---|---|
| Fachlogik | Bewertungslogik, PDF-Logik, Tracker-/Merge-Logik, Portal-Scan-Grundprinzip | Claude-spezifische Laufzeitannahmen | neue Fachmodule ausserhalb des heutigen Kerns |
| Datenhaltung | Markdown-, YAML-, TSV- und Datei-Artefakte | robuste Sperr- und Schreibregeln fuer parallelen Betrieb | relationale Datenbankmigration |
| Bedienung | command-/job-orientierte Nutzung | Claude-gebundene Bedienlogik | neue grosse Web-Produktoberflaeche |
| Automatisierung | Batch- und Pipeline-Grundidee | `claude -p`-Ausfuehrung, generische Shell-Orchestrierung | vollautonome End-to-End-Bewerbungsautomation |
| Betrieb | lokaler/self-hosted Charakter | Compose-faehige Laufzeit, Healthchecks, Secrets-Handling | zentraler Multi-Tenant-Betrieb |

## 5. Zielbild 2 - technische Zielarchitektur fuer provider-flexiblen, self-hosted Docker-Compose-Betrieb

### 5.1 Architekturentscheidung

Die kuenftige Architektur trennt strikt zwischen:

1. fachlichen Assets
2. Runtime-Orchestrierung
3. Provider-Anbindung
4. Browser-/PDF-Ausfuehrung
5. Persistenz und Betriebsdaten

Die fachlichen Assets bleiben weitgehend dateibasiert und wiederverwendbar. Die heutige Claude-Laufzeit wird jedoch durch eine provider-neutrale Ausfuehrungsschicht ersetzt.

### 5.2 Zielstruktur in Bausteinen

#### A. Fachliche Assets

Bleiben als inhaltliche Grundlage erhalten:

- Modus-/Prompt-Dateien
- Templates
- Profile, CV, Portalkonfiguration
- Report- und Trackerformate

Diese Ebene ist fachlich stabiler als die aktuelle Runtime und soll deshalb moeglichst wenig veraendert werden.

#### B. Control Plane / Orchestrator

Neue provider-neutrale Steuerungskomponente fuer:

- Entgegennahme von Auftraegen wie Evaluate, Scan, PDF, Batch
- Validierung von Eingaben und Konfiguration
- Erzeugen von Ausfuehrungsjobs
- Job-Status, Retry-Regeln und Healthchecks
- Auswahl des konfigurierten Provider-Adapters

Diese Komponente ersetzt die heutige implizite Steuerung durch Claude Code.

#### C. Execution Worker

Neue Worker-Komponente fuer die eigentliche Auftragsausfuehrung:

- Prompt-/Modus-Rendering aus bestehenden Assets
- Aufruf des Provider-Adapters
- Generierung von Reports, Tracker-Ergaenzungen und PDF-Auftraegen
- kontrollierte Batch-Ausfuehrung mit Parallelitaet ohne Shell-Subagent-Modell

Diese Worker laufen bewusst unprivilegiert.

#### D. Browser-/Render-Service

Separater Laufzeitbaustein fuer:

- Webseitenabruf und Inhaltsgewinnung
- Portal-Scan
- PDF-Rendering per Browser/Chromium

Die Trennung reduziert Sicherheits- und Stabilitaetsrisiken gegenueber einer Vermischung mit dem Kernprozess.

#### E. Artefakt- und Zustandsablage

Release 1 bleibt bewusst dateibasiert:

- Reports
- Tracker-Dateien
- Ausgabedateien
- Job-/Statusdateien
- Logs

Dadurch bleibt die Loesung klein und nahe am Bestand. Voraussetzung ist jedoch eine saubere Schreibserialisierung fuer konkurrierende Worker.

### 5.3 Docker-Compose-Zielbausteine

Fuer Release 1 werden folgende Compose-Bausteine explizit vorgesehen:

| Compose-Baustein | Rolle im Zielbild | Pflicht in Release 1 |
|---|---|---|
| `career-ops-core` | Control Plane / Orchestrator, API oder Kommandoendpunkt, Konfigurations- und Health-Verantwortung | Ja |
| `career-ops-worker` | unprivilegierte Abarbeitung von Evaluate-, Batch-, Scan- und PDF-nahen Jobs | Ja |
| `career-ops-browser` | isolierter Browser-/Playwright-/Chromium-Baustein fuer Scan, Extraktion und PDF-Rendering | Ja |
| `career-ops-dashboard` | optionale Anzeige- oder Viewer-Komponente auf bestehendem Datenbestand | Optional |
| persistente Volumes | Ablage fuer Daten, Reports, Output, Logs und Jobstatus | Ja |

Bewusste Nicht-Entscheidung fuer Release 1:

- kein eigener Datenbankdienst als Muss
- kein eigener Queue-Broker als Muss
- kein Reverse Proxy als Muss
- kein separater Scheduler als Muss

Falls zeitgesteuerte Scans spaeter benoetigt werden, ist ein kleiner Scheduler- oder Cron-Baustein anschlussfaehig, aber nicht Voraussetzung fuer Release 1.

### 5.4 Explizite Behandlung der heutigen Claude-Kopplungen

| Heutige Kopplung | Ziel im kuenftigen System |
|---|---|
| Claude Code als Interaktionsrahmen | ersetzt durch provider-neutrale Control Plane mit klaren Jobs/Kommandos |
| `CLAUDE.md` als Laufzeitanweisung | ersetzt durch provider-neutrale Runtime-/Ops-Konfiguration; fachliche Inhalte aus Modusdateien bleiben nutzbar |
| `claude -p` fuer Batch-Worker | ersetzt durch interne Worker-Jobs mit Provider-Adapter |
| Claude-spezifische Bedienwege / Slash-Commands | ersetzt durch neutrale Aufrufschicht, z. B. API-Endpunkte oder Container-Kommandos |
| lokale Claude-CLI-Voraussetzung | faellt im Zielbetrieb weg |

### 5.5 Ersatzmodell fuer `claude -p`

Das heutige Batch-Modell basiert auf Shell-gesteuerten, externen Claude-Unterprozessen. Dieses Modell wird in Release 1 bewusst ersetzt.

#### Zielmodell

Jeder Einzelauftrag wird als interner Ausfuehrungsjob behandelt:

1. ein Auftrag wird als `JobDescriptor` angelegt
2. der Worker rendert die benoetigten Prompt-/Modusbausteine mit Laufzeitvariablen
3. ein `ProviderAdapter` ruft den konfigurierten LLM-Provider auf
4. strukturierte Resultate werden in Reports, Tracker-Ergaenzungen und Folgejobs ueberfuehrt
5. Jobstatus, Retry-Zaehler und Fehlerbilder werden als Betriebszustand persistiert

#### Zielvorteile

- keine Abhaengigkeit von lokal installierter Claude-CLI
- keine Shell-Subagent-Kette fuer Kernlogik
- klarere Beobachtbarkeit und Fehlerbehandlung
- anschlussfaehig fuer weitere Provider nach OpenAI
- besser mit Compose und unprivilegierten Containern vereinbar

### 5.6 Provider-Flexibilitaet

Die Provider-Flexibilitaet wird in Release 1 ueber eine stabile Adaptergrenze erreicht.

#### Architekturprinzip

- fachliche Logik kennt keinen konkreten Provider
- nur der `ProviderAdapter` kennt API-Endpunkte, Authentisierung und provider-spezifische Parameter
- OpenAI ist der erste produktive Adapter
- weitere Adapter sind strukturell moeglich, aber nicht automatisch Teil von Release 1

#### Konservative Release-1-Entscheidung

- Ziel ist provider-flexible Struktur
- geliefert werden muss mindestens eine produktive OpenAI-Anbindung
- ein zweiter produktiver Provider ist fuer Release 1 nicht erforderlich

### 5.7 Was technisch bleiben kann / was ersetzt werden muss

| Technischer Bereich | Kann bleiben | Muss ersetzt werden |
|---|---|---|
| Prompt-/Modusdateien | ja, weitgehend | nur dort anpassen, wo Claude-spezifische Laufzeitanweisungen enthalten sind |
| Berichts-, PDF- und Trackerformate | ja | nur technische Erzeugungspfade neu verdrahten |
| dateibasierte Persistenz | ja, in Release 1 | Shell-/PID-zentrierte Nebenlaeufigkeitssteuerung |
| Dashboard auf Dateibestand | wahrscheinlich ja, optional | direkte Abhaengigkeit von Claude-Laufzeitannahmen |
| `doctor`-Gedanke als Betriebspruefung | ja, fachlich | lokale CLI-/Host-Annahmen durch Container-Healthchecks ersetzen |
| Updater-Zweck (System aktualisieren) | ja, als Betriebsfaehigkeit | Git-Fetch/Checkout im Zielsystem |

## 6. Zielbild 3 - Sicherheits- und Betriebszielbild mit Hardening-Annahmen

### 6.1 Zielaussage

Release 1 wird als kontrollierter self-hosted Dienst mit kleinen, trennscharfen Sicherheitsgrenzen betrieben. Mechanismen mit erhoehter Missbrauchs- oder Eskalationsflaeche werden reduziert, isoliert oder ersetzt.

### 6.2 Sicherheitsgrenzen

Die kuenftige Loesung trennt mindestens diese Vertrauenszonen:

- Bedien-/Operator-Zone
- Orchestrierungs-Zone
- Worker-Zone
- Browser-/Webzugriffs-Zone
- Persistenz-/Artefakt-Zone
- externe Provider- und Zielwebseiten-Zone

Ziel ist, dass ein Problem in einer Zone nicht automatisch Vollzugriff auf alle anderen Zonen erzeugt.

### 6.3 Hardening-Annahmen fuer Release 1

#### A. Batch-Worker

Heutiges Risiko:

- Shell-gesteuerte Unterprozesse mit potenziell weitreichenden Dateisystem- und Laufzeitrechten

Zielbild:

- Worker laufen als unprivilegierte Container- oder Prozessidentitaet
- nur benoetigte Volumes werden gemountet
- eigener temporarer Arbeitsbereich je Job
- Ressourcenlimits fuer CPU, RAM und Laufzeit
- keine Docker-Socket-, Host-Root- oder pauschalen Schreibrechte

#### B. Updater

Heutiges Risiko:

- Remote-Fetch und Git-Checkout direkt auf dem Zielsystem

Zielbild:

- kein In-App-Git-Checkout im Zielbetrieb
- Updates erfolgen ueber kontrollierten Image-/Release-Wechsel durch den Betreiber
- Versionen werden explizit gepinnt und nachvollziehbar gewechselt
- Rollback erfolgt ueber Betriebsartefakte bzw. vorige Images, nicht ueber implizite Self-Mutation

#### C. Shell-Ausfuehrung

Heutiges Risiko:

- Shell als allgemeines Ausfuehrungsmittel fuer Kernprozesse

Zielbild:

- Shell-Ausfuehrung wird fuer Kernprozesse entfernt oder strikt reduziert
- falls Prozessaufrufe technisch benoetigt bleiben, erfolgen sie ueber explizit allowlistete Kommandos
- keine provider- oder promptgesteuerte allgemeine Remote-Shell im Release-1-Zielbetrieb

#### D. Secrets und Konfiguration

Zielbild:

- Provider-Secrets liegen ausserhalb versionierter Projektdateien
- Nutzung von Compose-Secrets oder gleichwertig kontrollierter Secret-Uebergabe
- Trennung zwischen fachlicher Konfiguration und geheimen Betriebsdaten

#### E. Logging und Nachvollziehbarkeit

Zielbild:

- strukturierte Logs fuer Jobs, Fehler, Retries und Provider-Aufrufe
- keine unnoetige Ablage sensitiver Inhalte in Logs
- Betriebsereignisse muessen fuer Diagnose und Audit nachvollziehbar sein

#### F. Netzwerk und Egress

Zielbild:

- ausgehender Verkehr nur fuer benoetigte Ziele
- OpenAI-Zugriff klar konfigurierbar
- Webzugriff fuer Scanner/Browser bewusst auf die dafuer vorgesehenen Komponenten begrenzt

### 6.4 Sicherheitsbezogene Nicht-Ziele

- keine Aussage, dass das heutige System unbedenklich oder frei von Schadverhalten sei
- keine forensische Analyse im Rahmen dieses Zielbilddokuments
- keine Vollhaertung fuer beliebige Multi-Tenant- oder Internet-Exposure-Szenarien in Release 1

## 7. Zusammenfassende Leitentscheidung: unveraendert vs. ersetzt

### 7.1 Unveraendert oder weitgehend beibehalten

- fachlicher Kern der Pipeline
- vorhandene inhaltliche Prompt-/Modus-Assets, soweit provider-neutral nutzbar
- dateibasierte Artefakte und Trackerlogik in Release 1
- Browser-/PDF-Grundprinzip
- Human-in-the-loop-Produktgrenze

### 7.2 Zu ersetzen oder neu zu rahmen

- Claude-Code-zentrierte Laufzeit
- `claude -p`-Batchmodell
- Git-basierter Self-Updater im Zielbetrieb
- generische Shell-Ausfuehrung fuer Kernablaeufe
- lokale CLI-zentrierte Betriebspruefung als primaerer Produktionsmechanismus

### 7.3 Bewusst nicht Ziel von Release 1

- neue Produktdomaenen ausserhalb des heutigen Job-Operations-Kerns
- grosser UI-Neubau
- Datenbank- oder Queue-Landschaft ohne zwingenden Bedarf
- Multi-Tenant-SaaS-Betrieb
- Integrationsausbau zu CRM/Mail/Kalender

## 8. Annahmen, Risiken und offene Punkte

### 8.1 Annahmen

- Release 1 darf funktional konservativ bleiben und muss nicht die gesamte Nutzererfahrung neu gestalten
- ein kleiner, klarer Compose-Stack ist einem groesseren Plattform-Setup vorzuziehen
- OpenAI reicht als erster produktiver Provider aus, solange die Architektur weitere Adapter zulaesst
- dateibasierte Persistenz ist fuer Release 1 tragfaehig, wenn Nebenlaeufigkeit sauber begrenzt wird

### 8.2 Risiken

- Ergebnisqualitaet kann sich durch den Wechsel von Claude zu OpenAI veraendern
- bestehende Prompt-/Modusinhalte koennen implizite Claude-Annahmen enthalten und muessen bereinigt werden
- dateibasierte Parallelitaet bleibt fehleranfaelliger als ein transaktionaler Store
- selbst gehosteter Browserbetrieb kann betriebliche und sicherheitstechnische Zusatzkomplexitaet erzeugen
- Hardening reduziert Risiken, ersetzt aber keine spaetere Sicherheitspruefung

### 8.3 Offene Punkte fuer Sponsor- bzw. Folgeentscheid

- Soll Release 1 nur einen operatorischen API-/CLI-Zugang bereitstellen oder zusaetzlich eine kleine Bedienoberflaeche bekommen? Konservativer Default: nur API-/CLI-Zugang.
- Soll das bestehende Dashboard Bestandteil des Compose-Stacks sein oder optional ausserhalb bleiben? Konservativer Default: optional.
- Wird zeitgesteuerte Automatisierung in Release 1 benoetigt oder reichen manuelle Trigger? Konservativer Default: manuelle Trigger reichen.
- Wie streng sollen Netzwerk-Egress und Secret-Management im Zielumfeld operationalisiert werden? Konservativer Default: minimale Egress-Freigaben und keine Secrets in Projektdateien.

## 9. Empfohlener Hand-off fuer die weitere Initialisierung

Fuer den Entscheid `Weiteres Vorgehen` sollte auf Basis dieses Zielbilds festgehalten werden:

1. `career-ops` wird als funktional konservative Modernisierung weitergefuehrt, nicht als Produktneubau.
2. Claude-Code- und `claude -p`-Abhaengigkeiten werden als zu ersetzende Laufzeitkopplungen behandelt.
3. Release 1 zielt auf einen self-hosted Docker-Compose-Betrieb mit OpenAI als erstem produktiven Provider.
4. Updater, Batch-Worker und Shell-Ausfuehrung werden als Hardening-Schwerpunkte behandelt.
5. Dateibasierte Persistenz darf in Release 1 bleiben, solange Schreibkonflikte und Betriebsgrenzen sauber geloest werden.

## 10. Sponsor-Fazit in einem Satz

Das tragfaehige Zielbild fuer `career-ops` ist keine fachliche Neuerfindung, sondern die kontrollierte Ueberfuehrung des bestehenden Job-Operations-Kerns in eine provider-neutrale, Docker-Compose-faehige und sicherer abgegrenzte self-hosted Runtime ohne Claude-CLI-Abhaengigkeit.
