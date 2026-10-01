CMDB
│
│  z.B.
│  Produkt = "Apache Tomcat"
│  Version = "9.0.82"
│  Hersteller = "Apache"
│
▼
[1] Normalisierung / Entity Resolution
│
▼
[2] CPE Candidate Search
│
├── NVD CPE API
├── Internet-/Herstellerrecherche
└── vorhandener CPE-Katalog
│
▼
[3] LLM Candidate Matching
│
│  Kandidaten:
│  cpe:2.3:a:apache:tomcat:9.0.82:...
│  cpe:2.3:a:apache:tomcat:9.0.80:...
│  cpe:2.3:a:apache:http_server:...
│
▼
[4] Confidence / Entscheidung
│
├── HIGH   → automatisch akzeptieren
├── MEDIUM → Human Review
└── LOW    → kein Mapping
│
▼
CMDB ↔ CPE Mapping
│
▼
[5] NVD CVE Lookup
│
▼
CVE Candidates
│
▼
[6] Applicability Prüfung
│
▼
CMDB Asset ↔ CVE