JSON-Export der DOTX-Vorlagen

Inhalt:
- templates/*.json: eine strukturierte JSON-Datei pro DOTX-Vorlage
- index.json / index.csv: kompakter Überblick über alle Vorlagen
- summary.json: Laufzusammenfassung
- errors.json: nur vorhanden, falls einzelne Dateien nicht verarbeitet werden konnten

Schema pro Vorlage (vereinfacht):
- source_*: Herkunft der Datei im Eingangsarchiv
- document_properties: Core/App/Custom Properties aus der Office-Datei
- settings: relevante Word-Einstellungen wie update_fields_on_open
- summary: Kennzahlen zur Vorlage
- headings: erkannte Überschriften im Hauptdokument
- used_styles: verwendete Absatz- und Tabellenstile
- detected_placeholders: erkannte Platzhalter aus Content Controls, Glossary und typischen Mustern
- field_codes: Word-Feldfunktionen wie TOC, PAGEREF, DATE, PAGE
- content_controls: strukturierte SDT/Content-Control-Informationen inkl. Dropdown-/Combobox-Optionen
- document / headers / footers / glossary / footnotes / endnotes: extrahierte Inhaltsstruktur als Blöcke
- custom_xml: vorhandene customXml-Teile vereinfacht extrahiert

Hinweise:
- __MACOSX- und AppleDouble-Dateien (._*) wurden ignoriert.
- Die JSON-Dateien bilden die Word-Struktur semantisch ab, nicht pixelgenau das Layout.
- Feldcodes werden separat ausgewiesen; sichtbarer Text steht zusätzlich in den jeweiligen Blöcken.
