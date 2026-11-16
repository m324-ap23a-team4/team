# Team 4: Immobilienplattform (M324 DevOps)

Willkommen im zentralen Übersichts-Repository von **Team 4** für das Modul **M324**.  
Dieses Dokument dient der Lehrperson und dem Team als zentraler Einstiegspunkt mit Schnellzugriff auf alle Repositories, Dokumente und Theorieabgaben.

---

## ⚡ Schnellzugriff / Quick Links

| Bereich | Dokument / Ressource | Beschreibung / Zweck |
|---|---|---|
| **Kanban-Board** | 📌 [M324 Team 4 Board](https://github.com/orgs/m324-ap23a-team4/projects/1) | Live-Aufgabenverwaltung, Backlog & Sprints |
| **Meetings & Prozesse** | 📋 [D3: Meetings und Arbeitsprozesse](./docs/D3_Meetings_Prozesse.md) | Verbindliche Meeting-Struktur, Timeboxes & Rollen |
| **Meeting-Vorlage** | ✍️ [Meeting-Protokoll Vorlage](./docs/meeting-vorlage.md) | Standard-Template zum Kopieren für Check-Ins & Retros |
| **Entscheidungen** | 🎫 [Ticket #1: Kickoff-Entscheidungen](https://github.com/m324-ap23a-team4/team/issues/1) | Begründete Architekturentscheidungen (closed) |
| **Vereinbarung** | 🤝 [Vertrag Dev ↔ Ops](./docs/team-vereinbarung.md) | Schnittstellen, DoD, DoR & Arbeitsregeln |
| **Retrospektiven** | 🔄 [Retrospektiven & Notizen](./docs/retrospektiven.md) | Lessons Learned aus Phase A & B |

---

## 👥 Mitglieder & Rollen (Phase A & B)

| Name | GitHub Account | Teilgruppe | Rolle Phase A | Rolle Phase B |
|---|---|---|---|---|
| **Loris Imbrogno** | [@Lorisimbrogno](https://github.com/Lorisimbrogno) | B (Ops → Dev) | **Ops Lead & Moderation** | **Dev Lead & Moderation** |
| **Karol Jakub** | [@KarolJakubGroups](https://github.com/KarolJakubGroups) | A (Dev → Ops) | **Dev Lead** | **Ops Lead** |
| **Cedric Fischer** | [@cedi254](https://github.com/cedi254) | B (Ops → Dev) | Ops / Protokoll & Timekeeper | Dev / Protokoll & Timekeeper |
| **Andrin Ruegg** | [@AriesDevlo](https://github.com/AriesDevlo) | A (Dev → Ops) | Dev / Quality & Review Lead | Ops / Quality & Review Lead |
| **Marvin Kropf** | [@MarvinKropf2](https://github.com/MarvinKropf2) | A (Dev → Ops) | Dev / Docs & Release Manager | Ops / Docs & Release Manager |

> **Feste Lead-Verantwortung:** Loris Imbrogno und Karol Jakub bilden durchgehend die technische Leitung des Teams. In Phase A leitet Loris Ops und Karol Dev. Bei Phasenwechsel in Phase B bleiben beide in Lead-Funktion, führen aber spiegelbildlich den neuen Bereich (Loris führt Dev, Karol führt Ops) und coachen den Wissenstransfer.

---

## 📚 Theorie-Abgaben ([theorie/](./theorie/))

Alle Theoriearbeiten der vier Blöcke B1 bis B4 sind vollständig ausgearbeitet und abgelegt:

| Block | Thema | Datei | Zuständig | Reviewer |
|---|---|---|---|---|
| **B1** | DevOps-Kultur und Umgang mit Störungen | 📄 [B1_DevOps_Kultur.md](./theorie/B1_DevOps_Kultur.md) | Loris Imbrogno | Cedric Fischer |
| **B2** | Prozesse und Zusammenarbeit | 📄 [B2_Prozesse_Zusammenarbeit.md](./theorie/B2_Prozesse_Zusammenarbeit.md) | Cedric Fischer | Andrin Ruegg |
| **B3** | Continuous Integration und Artefakte | 📄 [B3_CI_Artefakte.md](./theorie/B3_CI_Artefakte.md) | Andrin Ruegg | Karol Jakub |
| **B4** | Continuous Delivery, Umgebungen und Deployment | 📄 [B4_CD_Betrieb.md](./theorie/B4_CD_Betrieb.md) | Karol / Marvin | Marvin Kropf |
| **Übersicht** | Kriterien & Review-Tabelle | 📄 [theorie/README.md](./theorie/README.md) | Team 4 | Alle |

---

## 🛠️ Repositories & System-Übersicht

Unsere Microservices-Architektur ist in 4 Repositories innerhalb der Organisation [**`m324-ap23a-team4`**](https://github.com/m324-ap23a-team4) aufgeteilt:

| Repository | Zweck | Status / Pipeline | Hauptverantwortung |
|---|---|---|---|
| [**`team`**](https://github.com/m324-ap23a-team4/team) | Team-Organisation, Theorie, Docs & Retros | Aktiv | Alle Mitglieder (Write) |
| [**`ms1`**](https://github.com/m324-ap23a-team4/ms1) | Microservice 1: Ortschaften (Web-API) | [CI Actions](https://github.com/m324-ap23a-team4/ms1/actions) (✓ Grün) | Teilgruppe A (Dev) |
| [**`ms2`**](https://github.com/m324-ap23a-team4/ms2) | Microservice 2: Immobilien (Web-API) | [CI Actions](https://github.com/m324-ap23a-team4/ms2/actions) | Teilgruppe A (Dev) |
| [**`infra`**](https://github.com/m324-ap23a-team4/infra) | Docker Orchestrierung & Runbook | Bereit für Phase A | Teilgruppe B (Ops) |

---

## 📌 System & Live-Links
| Komponente | Link |
|---|---|
| **Kanban Board** | [M324 Team 4 Board (GitHub Projects)](https://github.com/orgs/m324-ap23a-team4/projects/1) |
| **GitHub Organisation** | [github.com/m324-ap23a-team4](https://github.com/m324-ap23a-team4) |
| **Zeitlogging** | Tymeprint (individuell) |
| **Produktionsumgebung** | (wird in Phase A bereitgestellt) |
| **Runbook** | [infra/README.md](https://github.com/m324-ap23a-team4/infra) (ab Phase A) |
