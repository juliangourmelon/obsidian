

Begriffsklärungen
	- MaaS
	- PaaS
	- Mandantentrennung
	- KV-Cache

Anforderungen an die Plattform

Problem mit PaaS Ansatz bzgl. Mandantentrennung


Begründung warum MaaS besser ist


Beschreibung der Betriebsmodelle:
	- MaaS
	- MaaS-Hybrid
	- MaaS + PaaS


Beschreibung der Ausbaustufen von MaaS (Gab hier allerdings noch kein Review)


Beschreibung der Optionen für MaaS:
- MaaS-Lite (aktueller Zustand)
- MaaS-rvEvo
- MaaS-RZ

Zusammenfassung des geteilten Verantwortungsmodells und Begründung warum MaaS-RZ die einzige Möglichkeit ist, um dieses konform umzusetzen 




Beschreibung

Jeder Mandant erhält seinen eigenen Teil der Fusion und der darauf laufenden Open Shift Cluster. Da wir sowohl CPU, GPU als auch Speicherressourcen, muss die Trennung auf mehreren Ebenen erfolgen. Sehr starke Trennung auf CPU-Ebene (dedizierte Worker Nodes), Cluster-Ebene oder GPU-Node-Ebene ist nicht möglich/ praktikabel. Daher ergibt sich eine Vielzahl verschiedener Optionen, die alle mit unterschiedlichen Vor- und Nachteilen einhergehen. In jedem Fall muss zwischen einer Reihe verschiedener relevanter Faktoren abgewogen werden. Zu den hier entstehenden Trade-Offs, siehe nächste Folie.


Mögliche Trennungsebenen

•Hardware Trennung

•komplette Racks

•CPU-Nodes (ist bei uns nicht möglich)

•GPUs

•Dedizierte Nodes

•Dedizierte Karten

•MIG

•Speicher

•Cluster

•Komplett eigene Cluster (ist bei uns nicht möglich)

•Hosted Control Planes (nur 4 möglich)

•Namespace-Ebene (mit zusätzlichen Sicherheitsmaßnamen)

•Sandboxed Containers

•CoCo + NCC

•Subnetze

•gute RBAC + ACCs




Relevante Faktoren für die Mandantentrennung

