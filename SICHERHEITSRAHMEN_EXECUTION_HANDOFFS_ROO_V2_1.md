# SICHERHEITSRAHMEN_EXECUTION_HANDOFFS_ROO_V2_1

## Pflicht bei CODE oder DEBUG

Jede execution-nahe Uebergabe muss enthalten:

- Erlaubt
- Verboten
- Aenderungsradius
- Betroffene Bereiche
- Ausgeschlossen
- Pruefpflicht
- Erwartete Artefaktupdates
- Abbruch bei
- Dann zurueck an

## Minimaltemplate

```text
Sicherheitsrahmen:
- Erlaubt:
- Verboten:
- Aenderungsradius:
- Betroffene Bereiche:
- Ausgeschlossen:
- Pruefpflicht:
- Erwartete Artefaktupdates:
- Abbruch bei:
- Dann zurueck an:
```

## Standardregel

Wenn der Auftrag ohne neue Produkt-, Scope- oder Strukturentscheidung nicht sauber loesbar ist:
zurueck an SPONSOR, nicht still weitermachen.

In generischen Vorhabenprojekten gilt zusaetzlich:
`/extsrc/` ist read-only.
Schreibende Aenderungen dort sind unzulaessig.
