# D3: Meetings und Arbeitsprozesse

**Team 4:** Immobilienplattform  
**Gültigkeit:** Modul M324 DevOps (Phase A & B)  
**Board:** [GitHub Projects – M324 Team 4 Board](https://github.com/orgs/m324-ap23a-team4/projects/1)  

---

## 1. Übersicht & Zielsetzung

Dieses Dokument definiert die verbindlichen Arbeitsprozesse, Meeting-Strukturen und Rollen von Team 4 für das Modul M324. Da unser Modulunterricht in 4-Lektionen-Blöcken pro Woche stattfindet, ist unsere Prozesslandschaft auf maximale Effizienz, klare Rollen und schlanke Feedback-Schlaufen ausgelegt.

Ziel ist es:
- Allen Teammitgliedern zu jedem Zeitpunkt Klarheit über ihre Aufgaben zu geben.
- Leerläufe durch vorausschauende Task-Vorbereitung zu verhindern.
- Entwicklung (Dev) und Betrieb (Ops) eng zu synchronisieren.
- Eine kontinuierliche Verbesserung durch wöchentliche Mini-Retrospektiven zu leben.

---

## 2. Meeting-Rhythmus & Struktur (2 Meetings pro Blocktag)

An jedem Unterrichtstag (4 Lektionen) führen wir genau **zwei kurze, zeitlich strikt begrenzte Meetings (Timeboxes)** durch:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        BLOCKTAG (4 LEKTIONEN)                          │
├───────────────────┬────────────────────────────────┬───────────────────┤
│ 08:00 - 08:15     │ 08:15 - 11:15                  │ 11:15 - 11:30     │
│ Morning Check-In  │ Fokuszeit: Arbeitsphase        │ Wrap-Up & Retro   │
│ (Planung/Standup) │ (Dev, Ops, Tests, Reviews)     │ (Review & Learn)  │
└───────────────────┴────────────────────────────────┴───────────────────┘
```

### A. Morning Check-In & Task-Planung (10–15 Minuten)
- **Wann:** Zu Beginn des Unterrichtsblocks (z.B. 08:00 – 08:15).
- **Ziel:** Arbeitsplan des Tages synchronisieren, Tasks aus dem Backlog ziehen, Blocker frühzeitig erkennen.
- **Ablauf (Reihum-Prinzip):**
  1. *Board-Check:* Der Moderator öffnet das [GitHub Project Board](https://github.com/orgs/m324-ap23a-team4/projects/1).
  2. *Reihum-Abfrage:* Jedes Mitglied beantwortet kurz genau 3 Fragen:
     - **Was habe ich seit dem letzten Mal erledigt?**
     - **Was nehme ich mir heute konkret vor?** (Zuweisung einer Karte aus `Ready` nach `In Progress`).
     - **Wo stecke ich fest oder brauche Unterstützung?** (Identifikation von Blockern).
  3. *Schnittstellen-Check Dev ↔ Ops:* Benötigt Dev eine Anpassung der Docker-Umgebung? Benötigt Ops neue Endpunkte oder Umgebungsvariablen?
  4. *Abschluss:* Aufgaben sind zugewiesen, alle starten fokussiert in die Arbeitsphase.

### B. Wrap-Up & Mini-Retrospektive (10–15 Minuten)
- **Wann:** Kurz vor Lektionsende (z.B. 11:15 – 11:30).
- **Ziel:** Tagesergebnisse reviewen, Board auf den aktuellen Stand bringen, Erkenntnisse festhalten.
- **Ablauf:**
  1. *Review der Karten:* Welche Tasks wurden fertiggestellt? (`In Review` / `Done`). Wurden PRs gemergt?
  2. *Offene Punkte:* Was bleibt bis nächste Woche in Arbeit?
  3. *Mini-Retrospektive (5 Minuten):*
     - **Was lief heute besonders gut?**
     - **Wo gab es Reibungsverluste oder Probleme?**
     - **Was ändern / verbessern wir nächste Woche?** (1 konkrete Massnahme).
  4. *Protokoll-Check:* Der Protokollführer speichert die Notizen kurz ab.

---

## 3. Rollenverteilung

Um Effizienz und Verbindlichkeit zu garantieren, sind die Rollen klar aufgeteilt. Zu Beginn von Phase A starten wir mit folgenden festen Zuweisungen:

| Rolle | Person | Hauptverantwortung im Prozess |
|---|---|---|
| **Moderation & Ops Lead** | **Loris Imbrogno** | Leitet die Meetings pünktlich ein, führt durch die Agenda, achtet auf aktive Beteiligung aller und koordiniert die Infrastruktur/Deployment-Themen. |
| **Protokoll & Timekeeper** | **Cedric (cedi254)** | Führt das Meeting-Protokoll (Beschlüsse, Blocker, Action Items) und überwacht die strikte Einhaltung der Timeboxes (15 Min). |
| **Dev Lead** | **Karol Jakub** | Koordiniert die Entwicklung der Microservices `ms1` und `ms2`, achtet auf Konsistenz der Schnittstellen und Code-Struktur. |
| **Quality & Review Lead** | **Andrin Rüegg (AriesDevlo)** | Überwacht die Testabdeckung, stellt sicher, dass CI-Pipelines grün sind und Reviews im PR nicht blockieren. |
| **Docs & Release Manager** | **Marvin Kropf** | Hält die Moduldokumentation im Repo `team` aktuell und bereitet Meilenstein-Releases und Tagging vor. |

### Feste Lead-Verantwortung & Phasenwechsel (Phase A ↔ Phase B)
Um kontinuierliche Qualität und Stabilität zu gewährleisten, bilden **Loris Imbrogno** und **Karol Jakub** die durchgehende technische Führung des Teams:
- **Phase A:** **Loris** ist **Ops Lead** (Infrastruktur/Deployment) und **Karol** ist **Dev Lead** (Microservices ms1 & ms2).
- **Phase B (beim Rollentausch):** Wenn Teilgruppe A und B planmässig tauschen, bleiben Loris und Karol weiterhin die Leads ihrer Gruppen, tauschen jedoch spiegelbildlich die Fachdisziplinen: **Loris übernimmt den Dev Lead** und **Karol übernimmt den Ops Lead**. Dadurch ist sichergestellt, dass das erarbeitete Wissen nahtlos transferiert wird und beide Bereiche stets erfahrene Führung haben.
- **Rollenrotation bei Moderation/Protokoll:** Die Rollen für Moderation und Protokoll können zusätzlich rotieren, sodass jedes Mitglied Einblick in alle organisatorischen Abläufe erhält.

---

## 4. Aufgabenverwaltung & Kanban-Board

Wir nutzen ausschliesslich das integrierte **[GitHub Project Board (M324 Team 4 Board)](https://github.com/orgs/m324-ap23a-team4/projects/1)**. Dadurch sind Issues, Pull Requests und Code direkt mit dem Board verknüpft.

### Spalten-Definition & Workflow

```text
[ 1. Backlog ] ──► [ 2. Ready ] ──► [ 3. In Progress ] ──► [ 4. In Review ] ──► [ 5. Done ]
```

1. **Backlog:** Alle User Stories, Ideen und groben Anforderungen aus dem Modulauftrag.
2. **Ready (Priorisiert):** Tasks, die vorbereitet sind und sofort begonnen werden können.
   - *Kriterium:* Der Task hat eine klare Beschreibung und ein messbares Akzeptanzkriterium.
3. **In Progress (In Arbeit):** Aufgaben, an denen aktuell aktiv gearbeitet wird.
   - *WIP-Limit (Work in Progress):* **Maximal 1–2 Tasks pro Person gleichzeitig**, um Multitasking und Engpässe zu verhindern.
   - Jede Karte **muss** einer Person zugewiesen sein (`Assignee`).
4. **In Review (Pull Request offen):** Der Code ist geschrieben und getestet. Ein Pull Request ist offen und wartet auf das Review durch das zuständige Team gemäss `CODEOWNERS`.
5. **Done (Abgeschlossen):** Der PR ist erfolgreich durch die CI-Pipeline geprüft, gereviewt und nach `main` gemergt.

### Regeln gegen «vergessene» Karten
- Keine Karte bleibt länger als 2 Schultage ohne Update in `In Progress`.
- Tritt ein Blocker auf, wird die Karte mit dem Label `blocked` markiert und im nächsten Standup besprochen.

---

## 5. Vorausschauende Planung (Kein Leerlauf)

Damit kein Teammitglied auf Arbeit warten muss:
- **Puffer im Ready-Backlog:** Es befinden sich **immer mindestens 3–5 fertig definierte Tasks in der Spalte `Ready`**, bevor die Lektionen beginnen.
- **Definition of Ready (DoR):** Ein Task darf erst in `Ready` verschoben werden, wenn:
  - Das Ziel verständlich beschrieben ist.
  - Klar ist, welches Repository betroffen ist (`ms1`, `ms2`, `infra`, `team`).
  - Abhängigkeiten (z.B. "benötigt zuerst DB-Container") geklärt sind.
- **Definition of Done (DoD):** Ein Task gilt erst als `Done`, wenn:
  - Der Code / Text lokal getestet wurde.
  - Die GitHub Actions CI-Pipeline grün ist.
  - Mindestens 1 Approval eines Teammitglieds im Pull Request vorliegt.
  - Der Merge nach `main` erfolgt ist.

---

## 6. Onboarding & Vertretung (Einführung neuer/abwesender Mitglieder)

Sollte ein Teammitglied krank oder abwesend gewesen sein:
1. **Schritt 1:** Das Protokoll des letzten Wrap-Ups im Verzeichnis `docs/meeting-logs/` lesen.
2. **Schritt 2:** Das [GitHub Project Board](https://github.com/orgs/m324-ap23a-team4/projects/1) öffnen und die Spalte `Ready` bzw. die zugewiesenen Aufgaben prüfen.
3. **Schritt 3:** Im 5-Minuten-Briefing vor dem Morning Check-In mit dem Moderator (Loris) kurz eventuelle Fragen klären.

---

## 7. Vorlagen für Meeting-Protokolle

Um den Protokollaufwand für Cedric minimal zu halten, verwenden wir standardisierte Vorlagen:

### Vorlage: Morning Check-In (Standup)
```markdown
### Morning Check-In – Datum: [TT.MM.JJJJ]
- **Anwesend:** [Namen]
- **Timebox:** 10 Minuten (Start: 08:00, Ende: 08:10)

#### Reihum-Status:
- **Loris:** Gestern: [ ] | Heute geplant: [ ] | Blocker: [keine / ...]
- **Cedric:** Gestern: [ ] | Heute geplant: [ ] | Blocker: [keine / ...]
- **Karol:** Gestern: [ ] | Heute geplant: [ ] | Blocker: [keine / ...]
- **Andrin:** Gestern: [ ] | Heute geplant: [ ] | Blocker: [keine / ...]
- **Marvin:** Gestern: [ ] | Heute geplant: [ ] | Blocker: [keine / ...]

#### Besprochene Schnittstellen / Blocker:
- [z.B. Dev benötigt Port-Freigabe für ms2]
```

### Vorlage: Wrap-Up & Retrospektive
```markdown
### Wrap-Up & Mini-Retro – Datum: [TT.MM.JJJJ]
- **Timebox:** 15 Minuten (Start: 11:15, Ende: 11:30)

#### Erreichte Ergebnisse:
- [x] Task #12: Endpunkt /api/ortschaften implementiert (PR #4 gemergt)
- [ ] Task #14: Dockerfile optimiert (in Review)

#### Mini-Retrospektive:
- **Was lief gut?** [z.B. Schnelle Code-Reviews, gute Absprache]
- **Was war schwierig?** [z.B. Git-Konflikt bei README]
- **Konkrete Massnahme für nächste Woche:** [z.B. PRs vor der Pause mergen]
```
