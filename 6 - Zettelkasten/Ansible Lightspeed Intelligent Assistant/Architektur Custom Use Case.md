
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


