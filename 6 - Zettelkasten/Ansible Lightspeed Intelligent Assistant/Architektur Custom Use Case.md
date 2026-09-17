
#### Beschreibung des Use Cases

Pro Tag laufen ungefähr 3000 Ansible-Jobs auf diversen über die AAP (Ansible Automation Plattform) gesteuerten Servern. Die Logs dieser Jobs können nicht manuell überprüft werden, da die entsprechende menschliche Arbeitskraft fehlt. Ziel des Use Cases ist es, die Jobs täglich mit Hilfe des Intelligent Assistant zu analysieren und bei Fehlern oder Auffälligkeiten Lösungsoptionen und Hilfestellungen (in Textform) anzubieten. Der Intelligent Assistant erhält keinerlei Schreibrechte auf der AAP.
Es wäre ineffizient alle 3.000 Jobs jeden Tag direkt von dem Intelligent Assistant analysieren zu lassen. Aus diesem Grund sollen die Jobs bereits vorher innerhalb der AAP gefiltert und geclustert werden. Nur bestimmte Jobs (Jobcluster) werden dann an den eigentlichen Intelligent Assistant (IA) geschickt und dort von einem Granite-Modell (20/32B) und der üblichen RAG-Architektur (Zugriff auf Red Hat Docs, interne Konfigurationen, stderr, etc.) bewertet. 


#### Notwendige Architektur für den Use Case

Die Standard-IA-Architektur ist für den vorliegenden Use Case nicht ausreichend. Grund hierfür ist, dass die Jobs vor verarbeitet werden müssen. Diese Funktionalität ist nicht Teil des IA oder der AAP. Im Standard Use Case des IA stellen User diesem Fragen zu bestimmten Aspekten der AAP oder konkreten Jobs. Der IA reichert seinen Kontext dann mit Hilfe von RAG an und gibt dem User qualifizierte Handlungsempfehlungen. Im vorliegenden Fall interagiert der User zunächst nicht direkt mit dem IA, sondern relevante Jobs werden automatisch dort hingeschickt.  


#### Logischer Ablauf des Use Cases

                    AAP
                     │
              Job abgeschlossen
                     │
                     ▼
              Event / Collector
                     │
                     ▼
          ┌──────────────────────┐
          │ Preprocessing        │
          │                      │
          │ Status               │
          │ failed tasks         │
          │ error messages       │
          │ tenant               │
          │ inventory            │
          │ job template         │
          │ runtime              │
          └──────────┬───────────┘
                     │
                     ▼
          ┌──────────────────────┐
          │ Rule / Anomaly       │
          │ Detection            │
          └──────────┬───────────┘
                     │
             only interesting
                  results
                     │
                     ▼
          ┌──────────────────────┐
          │ Clustering           │
          │                      │
          │ "These 87 failures   │
          │ have same cause"     │
          └──────────┬───────────┘
                     │
                     ▼
                 Granite
                     │
              Root Cause /
              Recommendation
                     │
          ┌──────────┴───────────┐
          ↓                      ↓
      Lightspeed             Alerting
      Assistant              Mail/Teams




#### Workflow Architektur

                         AAP
                          │
                ~3,000 Jobs / day
                          │
                          ▼
                Event-Driven Ansible
                          │
                          ▼
                 Analysis Service
                          │
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
       Rule Engine                Embeddings
             │                         │
             │                    Clustering
             │                         │
             └────────────┬────────────┘
                          │
                 Interesting Events
                          │
                          ▼
                     AI Gateway
                          │
                          ▼
             Granite 4.0-H-Small (20/32B)
                          │
                          ▼
                      Findings
                          │
             ┌────────────┼────────────┐
             ↓            ↓            ↓
          Database      Alerting    Findings MCP
                                      │
                                      ▼
                            Intelligent Assistant
                                      │
                                      ▼
                                    Admin




#### Offene Punkte

- Wie stellen wir sicher, dass das Kontextfenster des Granite Modells nicht überläuft? (Bsp. 87 Jobs werden gleichzeitig an das Modell geschickt)
- Wie können wir Batching gestalten? (Ist das Teil des IA? In welchem Zeitraum müssen die Jobs analysiert werden?)
- Kann ich die Batching-Strategie nur auf vLLM-Ebene einstellen, oder kann ich hier adaptiv aus der AAP heraus vorgehen?


#### Vorschlag nächste Schritte

1. IA implementieren
2. MCP-Layer aktivieren und READ-only-flag setzen
3. Event-Pipeline und Analysis Service in AAP deployen
4. Semantisches Clustering (per Embedding Modell), um ähnliche Jobs/ Fehler/ etc. zusammenzufassen
5. Service, der per Prompt-Template Ergebnisse an Granite-Modell schickt





Use Case 1: Manueller Betrieb
Use Case 2: 