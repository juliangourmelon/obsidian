






EU AI Act: 
- Sind wir Hochrisiko? => eher nein, außer die BSH wird als KRITIS eingeordnet
- Trotzdem am besten kurze Dokumentation über AI Use Case
- AI Literacy
- Kurzer Eintrag im AI-Register

Thema	Vulnerability Scanner
Zweck	Ermittlung plausibler CPEs und CVEs
AI-Komponente	z. B. LLM für Entity/CPE Matching
Input	CMDB-Produktinformationen
Output	CPE + Confidence + Begründung
Entscheidung	Vulnerability Candidate, nicht automatisch bestätigte Schwachstelle
Human Oversight	Security Analyst (Steffen) kann Zuordnung prüfen
Datenquellen	CMDB, Hersteller, NIST/NVD etc.
Modell	Modellname + Version/Endpoint
Fehlerarten	False Positive / False Negative / Halluzination
Logging	Prompt/Input, Modellversion, Output, Tool Calls
Validation	CPE/CVE gegen strukturierte Quellen prüfen
Confidence	z. B. accepted / ambiguous / rejected
Automation	keine produktive Remediation ohne zusätzliche Kontrolle


Datenschutz: 
- Gibt es personenbezogene Daten?
- In welche Schutzbedarfsstufe fallen die Daten?


Informationssicherheit:
- Wie kann ich die Datensicherheit klassifizieren?





Fragen, die sich hieraus ergeben: 
- Welche LLMs dürfen genutzt werden (Foundation Model API; Lokales Deployment)?
- Dürfen Daten langfristig Serverless verarbeitet werden (Serverless = außerhalb des Azure Networks)?
- Wie genau müssen wir den Use Case dokumentieren?
- Welche Daten wollen wir an LLMs in unserem Agent-Workflow senden?
- Was sind mögliche Ansprechpartner für Datenschutz und Informationssicherheit?
- Gibt es bereits eine zentrale KI-Use Case Liste?




Welche Klassifizierung haben die Daten: 

PUBLIC
   ↓
externe Modelle erlaubt

INTERNAL
   ↓
nur freigegebene Enterprise Provider

CONFIDENTIAL
   ↓
nur vertraglich abgesicherte Plattform
+ EU Processing
+ No Training
+ definierte Retention

STRICTLY CONFIDENTIAL
   ↓
kein externer LLM Endpoint
bzw. nur speziell freigegebene Umgebung



#### Provider-Bewertung für Foundation-Modelle: 

Training: Werden Prompts oder Outputs für Modelltraining verwendet?
Retention: Werden Prompt und Completion gespeichert? Wie lange?
Human Access: Können Mitarbeiter des Providers auf die Daten zugreifen?
Subprocessors: Welche weiteren Unternehmen verarbeiten die Daten?
Processing Location: In welchen Ländern/Regionen findet Inference statt?
Data Residency: Wo werden persistente Daten gespeichert?
International Transfer: Können Daten außerhalb EU/EWR gelangen?
Encryption: Verschlüsselung in Transit und at Rest?
Isolation: Wie werden Mandanten voneinander getrennt?
Deletion: Wann und wie werden Daten gelöscht?
Logging: Welche Inhalte landen in Provider-Logs?
Contract: DPA/AVV, TOMs, SCCs usw. vorhanden?
Security: Zertifizierungen, Audit Reports, Incident Management usw.



| Frage | Vulnerability Scanner |
|---|---|
| Personenbezogene Daten? | möglichst **Nein** |
| Personenbezug entfernbar? | **Ja** |
| Credentials/Secrets? | **nie übertragen** |
| interne IP/Hostname nötig? | **Nein** |
| vollständige CMDB nötig? | **Nein** |
| vollständige Vulnerability-Daten nötig? | **Nein** |
| minimal notwendiger Input | Vendor/Product/Version |
| Training durch Provider? | muss ausgeschlossen/geprüft sein |
| Retention | prüfen/minimieren |
| Processing Region | EU-Anforderung prüfen |
| Subprocessor | prüfen |
| DPA/AVV | bei personenbezogenen Daten prüfen |
| Security-Freigabe | abhängig von Datenklasse |
| Logging | Input/Output möglichst intern auditierbar |



Auftragsverarbeitung: 

Die DSGVO sagt nicht „personenbezogene Daten dürfen grundsätzlich nicht verarbeitet werden“. Vielmehr braucht jede Verarbeitung eine Rechtsgrundlage. Art. 6 Abs. 1 DSGVO nennt sechs mögliche Grundlagen.

| Rechtsgrundlage | Typisches Beispiel |
|---|---|
| **Einwilligung** | freiwillige Anmeldung für bestimmte Verarbeitung |
| **Vertrag / vorvertragliche Maßnahmen** | Adresse für Warenlieferung |
| **Rechtliche Verpflichtung** | Mitarbeiterdaten für Steuer/Sozialversicherung |
| **Lebenswichtige Interessen** | medizinischer Notfall |
| **Öffentliches Interesse / öffentliche Gewalt** | bestimmte behördliche Aufgaben |
| **Berechtigtes Interesse** | Betrugsprävention, unter Umständen IT-/Netzwerksicherheit |