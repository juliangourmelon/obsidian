
Tags: [[AI_GOVERNANCE]]; [[BSI]]


Freitag, 10. April 2026
08:07
 
Welches Artifact Repository wird verwendet? 
Wie werden Modelle abgespeichert? (OCI, model files)
Welcher Speicher wird für die MLFlow / Kubeflow Metadaten verwendet? (PostgreSQL?)
Wie werden Modelle / Runtime-Images gescannt?
Gibt es einen Mirror?
Können Modelle von Hugging Face genutzt werden? (über Mirror?)

 
### Wichtige Sicherheitsaspekte: 
•	Authentifizierung per Service Account
•	Image Security 
•	Model Security (bezogen auf die Modell-Artefakte)
•	Network Security
•	Supply Chain Security 
•	Secrets Management
 
Welche Security Mechanismen für Modelle? 
-> safetensors?
-> modelcards?
-> specific sources (meta, etc.)
 
Zugriff von Modell Runtime auf Secrets in S3/ Host Filesystem muss unterbunden werden
 
 
### Sicherheitsabstufungen:
•	DEV vs. PROD
•	Kritikalität der Use Cases
 
 
### EU AI Act:
Monitoring and Logging at every Layer:
•	Model Layer: 
o	Provenance 
o	Documentation (AIBOM)
o	Risk Classification
•	Serving Layer:
o	Request/ Response Logging (with sidecars)
o	Explainability hooks (for high risk)
o	Human override capability
•	Platform layer:
o	Admission control (OPA/ Kyverno)
o	Image Policies
o	Signed Artifacts
•	Pipeline Layer:
o	Model validation
o	Bias checks
o	Automatic AIBOM generation
o	Security scans
o	Metadata generation (model cards)
 
Model Documantation:
•	Model card
•	Training data summary
•	Limitations
-> Mandatory AI Act
 
 
Prompt Database??
Conversation History?
 
 
 
Output Filtering
Input threat detection
Runtime Security (Red Hat Advanced Cluster Security)
Human in the loop
Guardrails