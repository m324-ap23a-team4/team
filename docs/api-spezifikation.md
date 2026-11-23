# API-Spezifikation und Teststandard

MS1 verwaltet Ortschaften, MS2 verwaltet Immobilien. Beide APIs senden JSON. POST-Anfragen brauchen den Header `Content-Type: application/json`. Im lokalen Compose-Setup ist MS1 unter `http://localhost:3001` und MS2 unter `http://localhost:3002` erreichbar. Jeder Service schreibt in seine eigene PostgreSQL-Datenbank.

## Healthchecks

`GET /health` wird auf beiden Services ohne Request-Body aufgerufen und antwortet mit `200 OK`.

**MS1**

```json
{
  "status": "ok",
  "service": "ms1",
  "uptime": 12.34,
  "timestamp": "2026-11-23T10:00:00.000Z"
}
```

**MS2**

```json
{
  "status": "ok",
  "service": "ms2"
}
```

## MS1 · Ortschaft erfassen

`POST /ortschaften` erwartet folgende Felder.

| Feld | Vorgabe |
| --- | --- |
| `name` | Pflichtfeld, String mit mindestens zwei Zeichen nach Entfernen äusserer Leerzeichen |
| `plz` | Pflichtfeld, String aus vier Ziffern, eindeutig in MS1 |
| `gruendungsdatum` | Pflichtfeld, gültiges Kalenderdatum im Format `YYYY-MM-DD` |
| `einwohner` | Pflichtfeld, nichtnegative Ganzzahl. Null ist erlaubt. |

**Request**

```json
{
  "name": "Niederhasli",
  "plz": "8155",
  "gruendungsdatum": "1899-05-15",
  "einwohner": 5543
}
```

**201 Created**

```json
{
  "id": "c3f8a4b2-9d1e-4f7a-8b2c-1e4d5a6b7c8d",
  "name": "Niederhasli",
  "plz": "8155",
  "gruendungsdatum": "1899-05-15",
  "einwohner": 5543
}
```

**400 Bad Request** bei einem ungültigen Feld oder einer bereits vergebenen PLZ.

```json
{
  "error": "Validierungsfehler: Einwohnerzahl muss positiv sein.",
  "field": "einwohner"
}
```

## MS1 · Ortschaften auslesen

`GET /ortschaften` wird ohne Request-Body aufgerufen und liefert bei `200 OK` eine nach Namen sortierte Liste. Ohne Einträge lautet die Antwort `[]`.

```json
[
  {
    "id": "c3f8a4b2-9d1e-4f7a-8b2c-1e4d5a6b7c8d",
    "name": "Niederhasli",
    "plz": "8155",
    "gruendungsdatum": "1899-05-15",
    "einwohner": 5543
  }
]
```

`GET /ortschaften/:id` erwartet die UUID im Pfad und liefert bei `200 OK` ein einzelnes Ortschaftsobjekt in derselben Form wie die POST-Antwort. Für eine unbekannte oder ungültige ID antwortet MS1 mit `404 Not Found`.

```json
{
  "error": "Ortschaft mit ID c3f8a4b2-9d1e-4f7a-8b2c-1e4d5a6b7c8d nicht gefunden"
}
```

## MS2 · Immobilie erfassen

`POST /immobilien` erwartet einen nichtleeren Typ, positive Zahlen für `zimmer`, `flaeche` und `preis` sowie eine UUID als `ortschaftId`. Das optionale `verkaufsdatum` ist ein gültiges Kalenderdatum im Format `YYYY-MM-DD` oder `null`.

MS2 fragt die Ortschaft per HTTP über `GET ${MS1_URL}/ortschaften/:id` ab. MS1 muss `200 OK` liefern, bevor MS2 die Immobilie speichert. Bei einer Antwort mit `404`, einem anderen Fehlerstatus oder einem Verbindungsfehler antwortet MS2 mit `400 Bad Request` und dem Feld `ortschaftId`. Der HTTP-Aufruf hat ein Zeitlimit von fünf Sekunden.

**Request**

```json
{
  "typ": "Haus",
  "zimmer": 5.5,
  "flaeche": 145,
  "ortschaftId": "c3f8a4b2-9d1e-4f7a-8b2c-1e4d5a6b7c8d",
  "preis": 1250000,
  "verkaufsdatum": null
}
```

**201 Created**

```json
{
  "id": "e9b1c2d3-4a5f-4e7b-8c9d-0a1b2c3d4e5f",
  "typ": "Haus",
  "zimmer": 5.5,
  "flaeche": 145,
  "ortschaftId": "c3f8a4b2-9d1e-4f7a-8b2c-1e4d5a6b7c8d",
  "preis": 1250000,
  "verkaufsdatum": null
}
```

**400 Bad Request** bei unbekannter Ortschaft.

```json
{
  "error": "Validierungsfehler: Angegebene Ortschaft existiert nicht in MS1.",
  "field": "ortschaftId"
}
```

## Teststandard und Testpyramide

Jeder Testfall erhält einen TSDoc-Kommentar (`/** … */`), der den geprüften Fall und das erwartete Verhalten benennt. Mit `npm ci` und `npm test` werden die Tests im jeweiligen Service-Repository ausgeführt. Die isolierten API-Tests nutzen einen lokalen Express-Testserver, Fake-Repositories und für MS2 einen Mock des ausgehenden HTTP-Aufrufs. Sie brauchen keine laufende Datenbank und keinen separat gestarteten Service.

| Story | Happy Path und Grenzfälle | Fehlerfälle | Tests |
| --- | --- | --- | --- |
| US1 · POST Ortschaft | `201` mit UUID und gespeicherten Werten. Null Einwohner und ein gültiger Schalttag werden akzeptiert. | Negative Einwohnerzahl, doppelte PLZ, fehlender Name und ungültiger Kalendertag ergeben `400`. Datum und Nullwert werden im selben Testfall geprüft. | [5 in MS1-PR #1](https://github.com/m324-ap23a-team4/ms1/pull/1/files) |
| US2 · GET Ortschaften | Gefüllte und leere Liste, vorhandene ID sowie erneuter Abruf einer per POST angelegten Ortschaft ergeben `200`. | Unbekannte oder ungültige ID ergibt `404`. Lesefehler ergibt `500`. | [6 in MS1-PR #2](https://github.com/m324-ap23a-team4/ms1/pull/2/files) |
| US3 · POST Immobilie | MS1 antwortet mit `200`, MS2 speichert und antwortet mit `201`. | MS1 liefert `404` oder einen Serverfehler, Zimmerzahl ist negativ oder Preis ist `0`. MS2 liefert `400` und speichert nichts. | [4 in MS2-PR #1](https://github.com/m324-ap23a-team4/ms2/pull/1/files) |

Die 15 isolierten Tests bilden die Basis. Integrationstests prüfen zusätzlich die echten SQL-Abfragen, eindeutige PLZ und die Speicherung in PostgreSQL. Ein systemweiter Test legt eine Ortschaft in MS1 an und verwendet ihre UUID im POST an MS2. Dabei wird die Ortschaft über den echten Detail-Endpunkt geprüft und die Immobilie in einer getrennten Datenbank gespeichert.
