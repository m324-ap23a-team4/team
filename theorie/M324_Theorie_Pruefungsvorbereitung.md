# M324 DevOps – Komplette Prüfungsvorbereitung (Blöcke B1 – B4)

Dieses Dokument fasst alle 28 Kriterien des offiziellen **TBZ Kriterienkatalogs** für die Modulprüfung M324 vollständig, präzise und mit allen realen Fallbeispielen zusammen. Es ist ideal als Lernskript und als direkte Textquelle für **Google NotebookLM (Audio Overview / Podcast)**.

---

# BLOCK B1: DevOps-Kultur und Umgang mit Störungen

## [B1-K01] DevOps-Begriff, Zielkonflikt und Missverständnisse
- **Definition:** DevOps ist keine Software, kein Tool und keine einzelne Stellenbezeichnung. Es ist eine Kultur- und Methodenbewegung, die Softwareentwicklung (Dev) und IT-Betrieb (Ops) zusammenführt, um Software schneller, zuverlässiger und in höherer Qualität bereitzustellen.
- **Klassischer Zielkonflikt («Wall of Confusion»):**
  - **Entwicklung (Dev):** Wird an Geschwindigkeit und neuen Features gemessen. Dev strebt nach ständiger **Veränderung**.
  - **Betrieb (Ops):** Wird an Systemstabilität, Verfügbarkeit (Uptime, SLA) gemessen. Da Änderungen Risiken bergen, strebt Ops nach **Stabilität / minimaler Veränderung**.
  - Die «Wall of Confusion» entsteht, wenn Dev fertigen Code ohne Rücksicht auf Betriebsanforderungen «über die Mauer» wirft und Ops bei Fehlern allein gelassen wird.
  - **Lösung:** Geteilte Gesamtverantwortung («You build it, you run it»), gemeinsame Metriken und kleine, häufige Deployments statt riskanter Gross-Releases.
- **Drei verbreitete Missverständnisse:**
  1. *«DevOps ist ein Tool» (z.B. Docker oder Kubernetes einführen):* Tools nützen nichts, wenn Silodenken und Misstrauen bestehen bleiben. Man automatisiert sonst nur schlechte Prozesse.
  2. *«DevOps ist ein separates Team»:* Ein isoliertes «DevOps-Team» erzeugt nur ein drittes Silo zwischen Dev und Ops.
  3. *«DevOps bedeutet NoOps (Entwickler machen alles allein)»:* Ops verschwindet nicht, sondern baut moderne Self-Service-Plattformen und Automatisierung für Devs.

## [B1-K02] CALMS
Das CALMS-Framework beschreibt die fünf Säulen erfolgreicher DevOps-Organisationen:
1. **Culture (Kultur):** Psychologische Sicherheit, geteilte Verantwortung, Vertrauen und Blameless-Kultur. *Beispiel:* Entwickler und Ops sitzen im selben Daily Standup.
2. **Automation (Automatisierung):** Manuelle, fehleranfällige Routineaufgaben eliminieren. *Beispiel:* Automatisierte CI/CD-Pipelines für Build, Test und Deployment.
3. **Lean (Schlankheit):** Verschwendung (Waste) eliminieren, kleine Batches, WIP-Limits. *Beispiel:* Grosse 6-Monats-Releases durch wöchentliche kleine Releases ersetzen.
4. **Measurement (Messung):** Datenbasierte Entscheidungen treffen. *Beispiel:* DORA-Metriken (Deployment-Frequenz, Mean Time to Restore) und System-Telemetrie messen.
5. **Sharing (Teilen):** Wissen organisationsweit verfügbar machen. *Beispiel:* Blameless Postmortems, gemeinsame Runbooks und offene Dokumentation.

> **Warum steht Culture an erster Stelle?**  
> Die besten Tools und Automatisierungen scheitern, wenn Misstrauen herrscht, Wissen gehortet wird oder Mitarbeiter Angst vor Fehlern haben. Kultur ist das tragende Fundament.

## [B1-K03] The Three Ways (Die Drei Wege)
1. **The First Way: Flow (Fluss von links nach rechts beschleunigen)**
   - Schneller Durchlauf der Arbeit von Dev bis zum Kunden in Produktion.
   - *Massnahmen:* Arbeit auf Kanban-Boards sichtbar machen, Batch-Grössen reduzieren, WIP-Limits setzen, keine unfertige/fehlerhafte Arbeit weiterreichen.
2. **The Second Way: Feedback (Rückkopplung von rechts nach links verkürzen)**
   - Schnelle, ständige Rückmeldungen aus Produktion und Tests zurück an die Entwickler.
   - *Massnahmen:* Monitoring & Alarme, CI-Testergebnisse innerhalb von Minuten, «Andon Cord» (Pipeline stoppen bei Fehlern, bis die Ursache behoben ist).
3. **The Third Way: Continuous Learning and Experimentation (Lernen & Experimentieren)**
   - Kultur des täglichen Lernens und des Eingehens kalkulierter Risiken.
   - *Massnahmen:* Blameless Postmortems nach Vorfällen, Notfallübungen (Fire Drills, Chaos Monkey), feste Zeit für Refactoring und Weiterbildung.

## [B1-K04] Vergleich CALMS und Three Ways
- **Gemeinsamkeiten:** Beide stellen den Menschen, Vertrauen, Messung/Feedback und kontinuierliche Verbesserung in den Mittelpunkt. Beide wollen Silos aufbrechen.
- **Unterschiede:**
  - **CALMS** ist ein **Kriterienkatalog / Dimensionenmodell** (5 gleichwertige Bereiche zur Reifegrad-Beurteilung: Was müssen wir beachten?).
  - **The Three Ways** ist ein **dynamisches Handlungsmodell** (3 aufeinander aufbauende Schritte im Wertstrom: 1. Fluss beschleunigen ➔ 2. Feedback verstärken ➔ 3. Lernen kultivieren).
- **Zusammenspiel:** CALMS liefert die Bausteine (Automation & Lean für First Way, Measurement für Second Way, Culture & Sharing für Third Way).

## [B1-K05] Monitoring und Alarme
- **Bausteine der Observability:**
  - **Health Check:** Einfache Status-Endpunkte (z.B. `GET /health` liefert 200 OK), um festzustellen, ob ein Service lebt.
  - **Logs:** Diskrete Text-Events mit Timestamp und Kontext (z.B. Exception-Stacktrace mit User-ID) fürs Detail-Debugging.
  - **Metriken:** Aggregierte Zahlenreihen über Zeit (CPU %, RAM, Latenz, Request-Rate) für Dashboards und Trends.
  - **Alarme:** Benachrichtigungen bei Grenzwertüberschreitungen.
- **Guter Alarm:** Muss **Actionable** sein (erfordert sofortige menschliche Handlung) und **symptombasiert** sein (Kundenwirkung messen, z.B. 5xx-Fehlerrate > 2%, statt reine CPU-Spitzen).
- **Zusammenhang mit Second Way:** Monitoring und Alarme sind die technische Umsetzung schneller Feedbackschlaufen von der Produktion zurück zur Entwicklung.
- **Alert Fatigue (Alarmmüdigkeit):** Zu viele Fehlalarme führen dazu, dass echte kritische Alarme ignoriert oder übersehen werden.

## [B1-K06] Incidents, Blameless-Kultur und Postmortem
- **Ablauf eines Incidents:**
  1. *Erkennung (Detection):* Monitoring schlägt an.
  2. *Eindämmung & Behebung (Mitigation/Resolution):* **Vorrang hat immer die schnellstmögliche Wiederherstellung des Kundendienstes** (z.B. Rollback, Neustart), nicht die sofortige Ursachenforschung!
  3. *Nachbereitung (Postmortem):* Tiefgehende Ursachenanalyse nach Wiederherstellung.
- **Blameless-Kultur:** Menschliches Versagen ist das Symptom, nicht die Ursache. Sucht man Schuldige («Blame»), vertuschen Mitarbeiter Fehler aus Angst. Bei «Blameless» fragt man: *«Welche Sicherheitsmechanismen im System haben gefehlt, dass ein Mensch diesen Fehler machen konnte?»*
- **Postmortem:** Strukturierter Bericht nach einem Vorfall mit: Zusammenfassung & Auswirkung, minutengenauer Timeline (UTC), Ursachenanalyse (5-Whys) und konkreten Action Items mit Verantwortlichen.

## [B1-K07] Fall GitLab 2017
- **Der Vorfall:** Ein übermüdeter Sysadmin führte bei Problemen mit der Datenbank-Replikation versehentlich `rm -rf` auf dem Produktions-Primärserver aus. 300 GB Live-Daten wurden gelöscht.
- **Totalversagen der Backups:** Keiner der 5 Backup-Mechanismen funktionierte (pg_dump-Versionskonflikt, S3-Skript stumm abgebrochen, Azure-Snapshots nicht aktiviert, Staging überschrieben). **Hauptursache:** Restore wurde nie automatisiert getestet. *Ein ungetestetes Backup existiert nicht!*
- **CALMS-Zuordnung:** Culture (blameless Umgang mit Admin), Automation (fehlende automatisierte Restore-Tests), Measurement (kein Alarm bei fehlgeschlagenem S3-Upload).
- **Ways:** Vor dem Vorfall fehlte der **Second Way** (kein Feedback über kaputte Backups); danach wirkte der **Third Way** (radikale Transparenz via YouTube-Livestream, öffentliches Postmortem).
- **Schuldfrage:** Der Ingenieur ist **nicht schuld**. Das System war fragil, unzureichend automatisiert und bot keine Schutzmechanismen für fatale Befehle.
- **Dauerhafte Massnahme:** Automatische, regelmässige Restore-Tests in einer Testumgebung mit Alarmierung bei Fehlschlag.

---

# BLOCK B2: Prozesse und Zusammenarbeit

## [B2-K01] Vom SDLC zum DevOps Lifecycle
- **Phasen:** Plan ➔ Code ➔ Build ➔ Test ➔ Release ➔ Deploy ➔ Operate ➔ Monitor.
- **Kreislauf (Unendlichkeitsschleife $\infty$):** Softwareentwicklung ist nie «fertig». Aus Monitor und Operate fliessen kontinuierlich neue Erkenntnisse zurück in Plan und Code.
- **Unterschiede zum Wasserfall:**
  1. Kleine, inkrementelle Batches statt riesiger Phasen.
  2. Kontinuierliches Feedback statt Feedback erst am Projektende.
  3. Integrierte Teams (Dev & Ops gemeinsam) statt sequentieller Übergaben über Silogrenzen.
- **Risiko:** Grosse, seltene Releases enthalten hunderte Änderungen auf einmal; wenn etwas bricht, ist die Ursache kaum zu finden. Kleine Releases lassen sich sofort isolieren und innerhalb von Minuten beheben oder zurückrollen.

## [B2-K02] MVP und Walking Skeleton
- **MVP (Minimum Viable Product):** Das kleinstmögliche Produkt, das dem Kunden echten Nutzen bringt, um schnellstmöglich Kundenfeedback am Markt zu validieren.
- **Walking Skeleton (Wandelndes Skelett):** Eine winzige, durchgängige technische Implementierung (z.B. Frontend ruft Backend auf, Backend schreibt in DB, läuft durch eine Pipeline). Es hat noch kaum Fachlogik, beweist aber, dass die **Architektur, Schnittstellen und Deployment-Pipelines von Anfang an zusammenarbeiten**.

## [B2-K03] Anforderungen und Tickets
- **User Story Aufbau:** *«Als [Rolle] möchte ich [Funktion], um [Nutzen/Ziel] zu erreichen.»*
  - *Beispiel:* «Als Kunde möchte ich nach Immobilien nach Ortschaft filtern, um schnell passende Objekte zu finden.»
  - *Akzeptanzkriterien (testbar):*
    1. Wenn nach «Zürich» gefiltert wird, werden nur Immobilien mit `ortschaftId = Zürich` angezeigt.
    2. Wenn keine Treffer existieren, wird eine leere Liste mit HTTP 200 zurückgegeben.
- **Vertikaler vs. horizontaler Schnitt:**
  - *Horizontal (schlecht):* Schicht für Schicht (z.B. ein Ticket für DB-Schema, eins für Backend-API, eins für Frontend). Kein Einzelticket bringt dem Kunden isoliert Nutzen.
  - *Vertikal (DevOps-Standard):* Schneidet quer durch alle Schichten (Frontend + API + DB) für eine einzelne Funktion. Jedes Ticket liefert sofort deploybaren Kundenwert.
- **Ticketarten:** Feature (neue Funktion), Bug (Fehlerbehebung), Incident (akute Produktionsstörung), Change (geplante Infrastrukturänderung). Ticketvorlagen sichern Vollständigkeit.

## [B2-K04] Kanban und Definition of Done
- **Kanban-Grundprinzipien:** Arbeit visualisieren, Work in Progress (WIP) begrenzen, Arbeitsfluss (Flow) steuern, kontinuierlich verbessern.
- **WIP-Limits & Engpässe:** WIP-Limits begrenzen die Anzahl Karten pro Spalte (z.B. max. 2 in «In Review»). Ein Engpass (Bottleneck) ist dort erkennbar, wo sich viele Karten vor einer Spalte stauen oder die Spalte dauernd am Limit ist.
- **DevOps Definition of Done (DoD):** Geht weit über «Code fertig» hinaus. Umfasst: Code gereviewt, Unit- & Integrationstests grün, CI-Pipeline grün, Docker-Image gebaut, auf Staging deployed, Monitoring/Healthchecks konfiguriert und Runbook aktualisiert.

## [B2-K05] Nachvollziehbare Entwicklung im Team
- **Der Lifecycle einer Änderung:**  
  Ticket (#42) ➔ Feature-Branch (`feat/login`) ➔ Commits mit Ticket-Referenz ➔ Pull/Merge Request (PR) ➔ Automatisierte Pipeline läuft ➔ Peer Review & Approval ➔ Merge nach `main` ➔ Automatisches Deployment.
- **Zweck des Peer Reviews:** Findet nicht nur Bugs und Sicherheitslücken, sondern dient vor allem dem **Wissenstransfer** im Team, erhöht die Code-Konsistenz und stellt sicher, dass kein Code ohne Vier-Augen-Prinzip in Produktion gelangt.

## [B2-K06] DORA-Kennzahlen (DevOps Research and Assessment)
Die 4 Kernmetriken für High-Performing Teams:
1. **Deployment Frequency (Bereitstellungshäufigkeit):** Wie oft wird erfolgreich nach Produktion deployed? (Ziel: täglich bis mehrfach täglich).
2. **Lead Time for Changes (Vorlaufzeit für Änderungen):** Wie lange dauert es vom ersten Commit bis zum produktiven Code beim Kunden? (Ziel: weniger als 1 Tag).
3. **Change Failure Rate (Änderungsfehlerrate):** Wie viel Prozent der Deployments führen zu Störungen in Produktion? (Ziel: 0–15 %).
4. **Time to Restore Service / MTTR (Wiederherstellungszeit):** Wie lange dauert es bei einem Ausfall, bis der Service wieder läuft? (Ziel: unter 1 Stunde).

> **Tempo und Stabilität gehören zusammen!**  
> Früher glaubte man, Geschwindigkeit schade der Stabilität. DORA beweist das Gegenteil: Teams, die häufig kleine Änderungen deployen, haben stabilere Systeme und beheben Fehler viel schneller.  
> **Keine Personenbeurteilung:** DORA-Metriken messen die Performance des gesamten soziotechnischen Systems, nicht Einzelpersonen (führt sonst zu Manipulation / Gaming).

## [B2-K07] Fall Pixelwerk
- **Berechnung DORA-Werte:** Wenn ein Team nur alle 4 Wochen deployt und 50% der Releases fehlschlagen, ist die Deployment Frequency extrem niedrig und die Change Failure Rate dramatisch hoch.
- **Engpass auf dem Board:** Wenn sich in der Spalte «Testing» oder «Review» 12 Karten stauen, während «In Arbeit» leer ist, ist Testing/Review der Engpass.
- **WIP-Limit:** Vorschlag: WIP-Limit auf 3 setzen, damit Entwickler erst beim Testen/Reviewen helfen («Stop starting, start finishing»), bevor sie neue Arbeit beginnen.
- **Kritik an Stornierungs-Story:** War horizontal nach Schichten geschnitten. Besser in 3 vertikale Stories schneiden: 1. Stornierung im Backend ermöglichen, 2. Stornierungsbutton im UI einbinden, 3. Automatische Bestätigungs-E-Mail versenden.

---

# BLOCK B3: Continuous Integration und Artefakte

## [B3-K01] Continuous Integration (CI)
- **Bedeutung:** Entwickler führen ihren Code mehrmals täglich auf dem Haupt-Branch (`main`) zusammen. Bei jedem Merge/Commit wird der Code automatisch gebaut und durch automatisierte Tests verifiziert.
- **Problem ohne CI («Merge Hell»):** Wenn Entwickler wochenlang auf isolierten Branches arbeiten, driften die Codebasen auseinander. Das Zusammenführen führt zu tagelangen, extrem schmerzhaften Merge-Konflikten.
- **Kein CI ohne häufige Integration:** Eine CI-Pipeline zu haben nützt nichts, wenn man nur alle zwei Wochen mergt. CI ist eine **Arbeitsdisziplin**, kein Tool.

## [B3-K02] Was eine Pipeline macht
- **Auslöser:** Automatisch durch Git-Events (Push auf Branch, Erstellen eines Pull Requests, Git Tag) oder zeitgesteuert (Cron) / manuell.
- **Typische Phasen:**
  1. *Checkout:* Quellcode aus Git laden.
  2. *Lint / Static Analysis:* Syntax- und Code-Style-Prüfung, Sicherheitsprüfung.
  3. *Compile / Build:* Code kompilieren und Abhängigkeiten auflösen.
  4. *Test:* Unit- und Integrationstests ausführen.
  5. *Package / Docker Build:* Unveränderliches Artefakt / Container-Image erstellen.
  6. *Publish / Push:* Artefakt in Registry hochladen.
- **Fehlschlag:** Bricht die Pipeline sofort ab («Fail Fast»); der Pull Request darf nicht gemergt werden.
- **Gute Pipeline:** Schnell (< 10 Minuten für schnelles Feedback), deterministisch (keine Zufallsergebnisse) und isoliert.

## [B3-K03] Werkzeuge und Tests
- **Build-Tool:** Automatisiert Kompilierung und Packaging (z.B. `npm`, `maven`, `gradle`).
- **Abhängigkeitsverwaltung:** Verwaltet externe Libraries mit exakten Versionen (z.B. `package.json`, `pom.xml`).
- **Linter:** Prüft Codequalität ohne Ausführung (z.B. `ESLint`, `SonarQube`).
- **Container:** Kapselt Code samt Runtime und Libraries betriebssystemunabhängig (z.B. `Docker`).
- **Testpyramide:**
  - *Basis (viele, schnell, billig):* **Unit-Tests** (prüfen einzelne Funktionen/Klassen isoliert).
  - *Mitte (mittel):* **Integrationstests** (prüfen Zusammenspiel von Komponenten, z.B. Service mit Datenbank).
  - *Spitze (wenige, langsam, teuer):* **End-to-End-Tests (E2E)** (prüfen den gesamten Benutzerablauf über UI und Backend).
- **Smoke Test:** Sehr schneller, oberflächlicher Basistest nach dem Deployment («Raucht der Server?»), der nur prüft, ob die Anwendung startet und auf `/health` antwortet.

## [B3-K04] Branching-Strategien
- **GitFlow:** Sehr komplex, viele langlebige Branches (`develop`, `feature`, `release`, `hotfix`, `master`). Führt zu seltenen Releases und hohen Merge-Konflikten.
- **GitHub Flow:** Sehr schlank. Nur `main` und kurzlebige `feature`-Branches, die per Pull Request direkt nach `main` gemergt und sofort deployt werden.
- **Trunk-Based Development (TBD):** Entwickler mergen mehrmals täglich direkt auf den Haupt-Branch (`trunk` / `main`). Neue Features werden über **Feature Flags** im Code deaktiviert, falls sie noch unfertig sind.
- **Risiko langlebiger Branches:** Je länger ein Branch getrennt lebt, desto grösser werden Merge-Konflikte und desto später bemerkt man Integrationsfehler.

## [B3-K05] Semantic Versioning (SemVer: `MAJOR.MINOR.PATCH`)
- **Format:** `vX.Y.Z` (z.B. `v2.4.1`)
  - **MAJOR (X):** Breaking Changes (Inkompatible API-Änderungen). *Beispiel:* Endpunkt `/api/users` umbenannt oder Pflichtparameter entfernt ➔ `v3.0.0`.
  - **MINOR (Y):** Neue Funktionalität abwärtskompatibel hinzugefügt. *Beispiel:* Neuer optionaler Filter-Parameter ➔ `v2.5.0`.
  - **PATCH (Z):** Abwärtskompatible Fehlerbehebung / Bugfix. *Beispiel:* NullPointer-Exception behoben ➔ `v2.4.2`.
- **Wichtigkeit bei Microservices:** Services kommunizieren über Schnittstellen. Wenn Service B nicht weiss, ob Service A seine API gebrochen hat, fällt das Gesamtsystem aus.

## [B3-K06] Artefakte und Registry
- **Artefakt:** Das fertige, kompilierte und ausführbare Paket einer Software (z.B. Docker-Image, JAR-Datei, npm-Package).
- **Registry:** Zentraler Speicherort für Artefakte (z.B. Docker Hub, GitHub Packages GHCR, Nexus).
- **Unveränderlichkeit (Immutability):** Ein Artefakt mit einer bestimmten Versionsnummer (z.B. `ms1:v1.2.0`) darf niemals überschrieben werden.
- **Warum niemals `:latest` deployen?** `:latest` ist ein dynamischer Zeiger, der sich jederzeit ändern kann. Man weiss nie, welcher Code gerade läuft, und ein zuverlässiger Rollback ist unmöglich!

## [B3-K07] Fall Knight Capital und Versionierung (2012)
- **Der Vorfall:** Finanzhandelsfirma verlor 440 Millionen Dollar in 45 Minuten und ging pleite.
- **Drei Ursachen:**
  1. *Manuelles Deployment:* Ein Mitarbeiter kopierte die Software manuell auf 8 Server – und vergass Server Nummer 8.
  2. *Toter Code & wiederverwendetes Flag:* Auf Server 8 war noch uralter Testcode aktiv, der durch ein wiederverwendetes Feature-Flag («Power Peg») aktiviert wurde.
  3. *Kein einheitliches Artefakt / keine Validierung:* Keine Pipeline prüfte, ob auf allen Servern dieselbe Version lief.
- **Was hätte ein versioniertes Artefakt geändert?** Ein automatischer Rollout desselben Docker-Images auf alle 8 Server hätte die Inkonsistenz verhindert.
- **Learning zu totem Code:** Toter Code muss radikal gelöscht werden; Flags dürfen niemals für andere Funktionen recycelt werden.

---

# BLOCK B4: Continuous Delivery, Umgebungen und Deployment

## [B4-K01] Continuous Delivery vs. Continuous Deployment
- **Continuous Delivery (CDel):** Jede Änderung wird automatisch gebaut, getestet und ist **jederzeit auf Knopfdruck produktionsreif**. Das tatsächliche Deployment nach Produktion wird jedoch durch einen **manuellen Geschäftsentscheid** (Button-Klick) freigegeben.
- **Continuous Deployment (CDep):** Jede Änderung, die die Pipeline erfolgreich durchläuft, wird **vollautomatisch ohne menschlichen Eingriff direkt in Produktion ausgerollt**.
- **Voraussetzungen für Continuous Deployment:**
  - Extrem hohe Testabdeckung (Unit-, Integrations-, E2E-Tests).
  - Umfassendes Monitoring und automatische Rollbacks bei Fehlern.
  - Hohe Fehlerkultur und Feature Flags zur Risikominimierung.

## [B4-K02] Umgebungen und «Build once, deploy many»
- **Umgebungen:**
  - **Dev:** Lokale Entwicklungsumgebung oder Entwicklungsserver für schnelle Iterationen.
  - **Test:** Automatisierte Ausführung von Integrationstests.
  - **Staging:** Exakte 1:1-Kopie der Produktion für finale Freigabetests.
  - **Produktion (Prod):** Die echte Live-Umgebung für zahlende Kunden.
- **Umgebungs-Parität (Environment Parity):** Alle Umgebungen müssen technisch identisch sein (gleiche OS-Version, gleiche DB-Version, gleiche Konfigurationsstruktur), um den gefürchteten Effekt *«Auf meinem Rechner lief es aber!»* zu verhindern.
- **«Build once, deploy many»:** **Genau dasselbe Artefakt** (z.B. exakt dasselbe Docker-Image), das in Test und Staging getestet wurde, wird in Produktion deployed. Es wird **nicht** für jede Umgebung neu gebaut! Nur die Umgebungsvariablen ändern sich.

## [B4-K03] Infrastructure as Code (IaC) und Konfiguration
- **Infrastructure as Code (IaC):** Server, Netzwerke und Container werden über Code definiert (z.B. `docker-compose.yml`, Terraform, Ansible) und in Git versioniert.
  - *Vorteile:* Reproduzierbarkeit auf Knopfdruck, keine manuellen Konfigurationsfehler, Versionskontrolle für Infrastrukturänderungen.
- **Trennung von Code und Konfiguration (12-Factor App):** Konfigurationen (DB-Passwort, Hostnamen, Ports) werden über **Umgebungsvariablen** von aussen übergeben, niemals hart im Code programmiert. Nur so kann dasselbe Image in Dev, Staging und Prod laufen.

## [B4-K04] Secrets (Passwörter & API-Keys)
- **Regeln:** Secrets gehören **niemals** ins Git-Repository und **niemals** fest in ein Dockerfile/Image!
- **Wohin gehören sie?** In gesicherte Secret-Stores (z.B. GitHub Secrets, HashiCorp Vault, AWS Secrets Manager) und werden zur Laufzeit als Umgebungsvariablen injiziert.
- **Warum reicht Löschen im Git nicht?** Git speichert die gesamte Versionshistorie. Selbst wenn die Zeile gelöscht wird, bleibt das Passwort in alten Commits für immer lesbar!
- **Least Privilege:** Dienste erhalten nur exakt die minimal notwendigen Rechte.
- **Rotation:** Secrets müssen regelmässig und im Ernstfall sofort ungültig gemacht und neu generiert werden können.

## [B4-K05] Deployment-Strategien
1. **Recreate:** Alte Instanz stoppen ➔ Neue Instanz starten.
   - *Vorteil:* Sehr einfach, keine Ressourcenverdopplung.
   - *Nachteil:* **Downtime** (Ausfallzeit für Kunden).
2. **Rolling Update:** Instanzen werden nacheinander schrittweise ausgetauscht.
   - *Vorteil:* Keine Downtime, ressourcenschonend.
   - *Nachteil:* Während des Rollouts laufen alte und neue Version gleichzeitig nebeneinander.
3. **Blue/Green Deployment:** Zwei identische Umgebungen (Blue = Live, Green = Neu). Neue Version wird auf Green deployed und getestet. Dann schaltet der Router/Load Balancer den Traffic schlagartig auf Green um.
   - *Vorteil:* Zero Downtime, blitzschneller Rollback durch Zurückschalten des Routers.
   - *Nachteil:* Doppelte Infrastrukturkosten während des Deployments.
4. **Canary Deployment:** Neue Version wird zuerst nur für einen winzigen Prozentsatz der Nutzer (z.B. 2%) freigeschaltet. Wenn Fehlerraten stabil bleiben, wird schrittweise auf 100% erhöht.
   - *Vorteil:* Minimiertes Risiko; Fehler treffen nur wenige Nutzer.
   - *Nachteil:* Komplexe Routing- und Monitoring-Infrastruktur erforderlich.
- **Feature Toggles (Flags):** Schalter im Code, um Funktionen zur Laufzeit ohne Deployment an- oder abzuschalten. Trennt das technische **Deployment** (Code auf Server bringen) vom geschäftlichen **Release** (Funktion für Kunden freischalten).

## [B4-K06] Rollback und Datenbankänderungen
- **Rollback vs. Roll-forward:**
  - *Rollback:* Zurückkehren zur vorherigen stabilen Version (z.B. altes Docker-Image starten).
  - *Roll-forward:* Den Fehler im Code blitzschnell beheben und als neuen Patch nach vorne deployen.
- **Das Datenbank-Problem:** Ein Rollback der Software ist unmöglich, wenn die neue Version bereits ein Datenbankschema verändert oder Tabellenspalten gelöscht/umbenannt hat. Die alte Version versteht die veränderte DB nicht mehr.
- **Expand and Contract (Phased Migrations):**
  1. *Expand:* Datenbank erweitern (neue Spalte hinzufügen, alte Spalte bleibt bestehen).
  2. *Transition:* Code deployen, der in beide Spalten schreibt, aber aus der neuen liest.
  3. *Contract:* Wenn alles stabil läuft, wird die alte Spalte in einem separaten Schritt gelöscht.

## [B4-K07] Fall CrowdStrike (Juli 2024)
- **Der Vorfall:** Sicherheitsfirma CrowdStrike rollte ein fehlerhaftes Konfigurationsupdate für ihren Sensor weltweit an 8,5 Millionen Windows-Rechner gleichzeitig aus. Folge: Weltweiter «Blue Screen of Death» (BSOD) an Flughäfen, Banken und Spitälern.
- **Beste Deployment-Strategie:** **Canary Deployment / Staged Rollout** (z.B. erst interne Testrechner, dann 1%, dann 10%). Ein Canary hätte den Absturz sofort erkannt, und maximal eine Handvoll Rechner wären betroffen gewesen.
- **Warum war Rollback so schwer?** Rechner befanden sich in einer Bootschleife (BSOD). Es gab keinen Fernzugriff (kein Netzwerk). Techniker mussten physisch zu jedem einzelnen PC reisen, im abgesicherten Modus starten und die defekte `.sys`-Datei manuell löschen.
- **Sicherheitsupdates an alle?**
  - *Pro:* Schneller Schutz vor akuten Zero-Day-Exploits.
  - *Kontra:* Extremes Risiko eines globalen Single-Point-of-Failure ohne gestaffelte Tests.
