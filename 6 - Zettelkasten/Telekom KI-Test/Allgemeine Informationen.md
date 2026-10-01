
Tags: [[BSI]]


[ZERTIFIZIERTE KI | Qualität sichern. Fortschritt gestalten.](https://www.zertifizierte-ki.de/)

Das Projekt „ZERTIFIZIERTE KI“ betrachtet sechs große Vertrauenswürdigkeitsdimensionen: **Autonomie und Kontrolle, Fairness, Transparenz, Verlässlichkeit, Sicherheit sowie Datenschutz**. Dazu kommen konkrete technische Prüfwerkzeuge und Prüfmethoden.

Bei einem heutigen LLM-Stack würde das praktisch beispielsweise bedeuten, dass man nicht nur klassische Benchmarks wie MMLU oder HumanEval fährt, sondern Tests in der Art von:

| Bereich        | Beispielhafte Prüfung                                         |     |
| -------------- | ------------------------------------------------------------- | --- |
| Security       | Prompt Injection, Indirect Prompt Injection, Jailbreaks       |     |
| Data leakage   | Kann das Modell sensible Informationen wiedergeben?           |     |
| Robustness     | Wie reagiert es auf manipulierte oder ungewöhnliche Inputs?   |     |
| Reliability    | Halluzinationen, Reproduzierbarkeit, Fehlermodi               |     |
| RAG            | Kann manipuliertes Retrieval den System-Prompt überschreiben? |     |
| Tool Calling   | Ruft das Modell unerlaubte Tools oder Parameter auf?          |     |
| Access Control | Kann das Modell RBAC/ABAC-Mechanismen umgehen?                |     |
| Privacy        | PII, Training-Data Leakage, Logging                           |     |
| Fairness       | systematische Verzerrungen bestimmter Gruppen                 |     |
| Transparency   | Modellversion, Datenherkunft, bekannte Grenzen                |     |
| Operations     | Modellupdates, Monitoring, Incident Management                |     |
| Governance     | Verantwortlichkeiten, Risikobewertung, Dokumentation          |     |

Besonders interessant: Der BSI-Katalog sagt beispielsweise explizit, dass System-Prompts **nicht als Rechte-/Rollensystem verwendet werden sollten** und dass Verantwortliche sich bewusst sein müssen, dass System-Prompts durch Prompt Injection umgangen werden können.
