Tags: [[DSGVO]]; [[GPU]]; [[AI_SECURITY]]

##### Entscheidungsfaktoren (keine besondere Reihenfolge)

- Betriebsoverhead
- Availability
- Zahl der Mandanten
- *BSI-Konformität*
- *Sicherheitsfreigabe durch die DRV*
- *Tatsächliche Sicherheit*
- Zusätzliche Kosten
- Effiziente Nutzung
- Starke Trennung zwischen NonProd und Prod Umgebungen
- Betriebsmodelle ermöglichen (PaaS / MaaS)
- Sowohl Daten mit Schutzbedarfsstufe normal, hoch (und evtl. sehr hoch) verarbeiten
- ~~Möglichkeit Prod-Workloads umzusetzen~~


-> Prod Workloads werden auf der Fusion umgesetzt werden können. Der Worst Case ist nicht, dass die Fusion nur als Spielwiese verwendet werden kann. Im Notfall werden allerdings Abstriche im Bereich der Mandantenzahl und Availability gemacht werden müssen.


##### Dimensionalität

![[Dimensionalität 1.png]] 

BSI-Konformität, Sicherheitsfreigabe durch die DRV und die Minimierung tatsächlicher Risiken gehen in eine ähnliche Richtung (sind allerdings aber nicht dasselbe!!). Prinzipiell sind die effiziente Nutzung der GPU-Ressourcen, Availability und die Zahl der Mandanten gegenläufig. Siehe [[Mandantentrennung#^1436ee]]. 

Beispiel: 
Wenn ich hohe Sicherheit möchte (durch dedizierte GPU-Nodes) 
- wird die Zahl der Mandanten eingeschränkt (es gibt nur 4 Nodes -> wenn noch eine starke Trennung zwischen NonProd und Prod stattfinden soll, 
- wird die Zahl der Mandanten auf 2 beschränkt), die GPU-Ressourcen können nicht mehr so effizient genutzt werden (Jeder Mandant erhält genau einen Node, unabhängig vom tatsächlichen Bedarf) und 
- die Availability wird eingeschränkt (Workloads können unter Umständen nicht mehr zwischen Hardware verschoben werden).

Der Betriebsaufwand verläuft im Verhältnis zu den anderen Dimensionen nicht linear: Bestimmte Lösungen gehen mit hohen Aufwänden einher. Nach meinem aktuellen Verständnis sind das Folgende: 
- Härtung durch Network Policies, VMs, etc. (ist komplex umzusetzen, wenn RHOAI verwendet wird - was bei uns der Fall ist)
- Trennung auf GPU-Ebene (ist laut Jens Lindenberg anspruchsvoll, - bin mir nicht mehr ganz sicher, warum)

##### Harte Wahrheiten / Technische Einschränkungen

- Es gibt nur 4 GPU-Nodes
- Es gibt nur 4 HCPs
- Jeder Fusion Rack verfügt nur über 3 CPU-Nodes. Die Control-Plane der HCPs muss hochverfügbar auf allen drei Nodes laufen. Echte Hardwaretrennung ist innerhalb eines Fusion Racks also nicht möglich
- Gemeinsame Verwendung von GPU-Ressourcen hat mehr Sicherheitsrisiken als gemeinsame Verwendung von CPU-Ressourcen. 
- Härtung der Mandantentrennung außerhalb von dedizierter Hardware und HCPs geht fast immer mit Betriebsoverhead und teilweise mit zusätzlichen Kosten einher


##### Konkrete Trade-Offs

^1436ee

- Trennung auf GPU(-Karten)-Ebene ist mit Betriebsoverhead verbunden. MiG ist allerdings nicht so sicher.
- Trennung auf GPU-Node Ebene ist sehr sicher, schränkt aber die Zahl der Mandanten auf 2-3 ein
- Umso "höher" die Trennung auf GPU-Ebene ist, desto ineffizienter werden die GPU-Ressourcen eingesetzt




##### Konkrete Technische Entscheidungen

- **GPU-Trennung** (besonders relevant, da GPUs besondere Risiken mit sich bringen bei Multi-Tenancy)
	- Ebene der Trennung
		- Node
		- GPU(-Karte)
		- MiG
		- Shared GPU (keine Option in Prod)
	- Zusätzliche Härtung der Sicherheit
		- NVIDIA Confidential Computing
		- OpenShift CoCo
- **Allgemeine Trennung/ CPU-Trennung**:
	- Trennung auf Hardware-Ebene (im aktuellen Aufbau der Fusion nicht möglich)
	- Trennung auf HCP-Ebene (im aktuellen Aufbau der Fusion nur 4 HCPs möglich)
	- Weitere Maßnahmen, um Mandantentrennung zu härten:
		- Sandboxed Containers (Kata Container)
		- Verbesserte Netzwerktrennung
		- ... (weitere Vorschläge von Steffen Lützenkirchen, etc.)
- **Speicher-Trennung** (haben wir aktuell noch keinen großen Fokus drauf gehabt, sollte aber kein Problem sein)





##### Worst Case #1

- Nur zwei Mandanten dürfen auf die Fusion (jeder bekommt ein komplettes Rack, oder jeder bekommt jeweils eine HCP mit einem GPU-Node auf jedem der beiden Racks)
	- 2 Mandanten (+ Workloads auf Fusion Systemtest)
	- Dedizierte GPU-Nodes (pro Mandant und pro Umgebung)
	- Echte Hardwaretrennung (eigene Racks), oder Availability (Racks werden geteilt, Workloads können verschoben werden)

##### Worst Case #2

- Nur 3 Mandanten dürfen auf die Fusion. Jeder Mandant erhält eine eigene HCP mit eigenem GPU-Node. Eine HCP mit einem GPU-Node wird zwischen den Mandanten als NonProd-Umgebung geteilt
	- 3 Mandanten (+ Workloads auf Fusion Systemtest)
	- Dedizierte GPU-Nodes in Prod
	- Effiziente Nutzung der Ressourcen in NonProd
	- Trennung der Prod Umgebungen auf HCP-Ebene


##### Best Case

- Wir erfüllen alle BSI/ DRV-Auflagen und unsere eigenen Sicherheitsziele mit virtueller Trennung der CPUs und Aufteilung der GPUs auf MiG-Ebene / GPU-Ebene. 
	- 4 Mandanten (+ Option auf weitere)
	- Effiziente Nutzung der Ressourcen in NonProd und Prod
	- Trennung von NonProd und Prod auf HCP-Ebene
	- Trennung der GPUs auf MiG-/Kartenebene
		- Innerhalb der Mandanten können wir die GPUs virtualisieren, um die Auslastung effizienter zu gestalten
	- 1 Node für NonProd; 3 Nodes für Prod


##### Lösung aufgrund von Vorschlag von Klaus

Wir haben ein zentrales MaaS Deployment auf das alle Bedarfsträger zugreifen dürfen. Hier werden ein oder zwei Nodes komplett reserviert und von uns verwaltet. Wir deployen Modelle und ein zentrales AI-Gateway. Wir stellen die Möglichkeiten zur Verfügung, eigene Guardrails je nach Use Case zu deployen.
=> Datenschutz / BSI !!!
Die anderen HCPs und GPU-Nodes werden für PaaS verwendet: Hier trennen wir auf GPU-Kartenebene und erlauben nur 2 Mandanten (rvEvo und Abteilung 11).




##### Erforderliche Schritte für die Entscheidungsfindung:

- [ ] Mit Patrick / Michael Bier klären, ob es nicht doch die Möglichkeit für ein zentrales MaaS Deployment gibt
- [ ] Gespräch mit Leonardo, ob Datenverarbeitung auf geteilter GPU-Ebene möglich ist
- Anforderungen der DRV an Mandantentrennung müssen eingeholt werden:
	- Ist (gehärtete) Namespace-Trennung ok? -> Ansonsten müssen wir uns mit 2-3 Mandanten zufrieden geben
	- Werden dedizierte GPU-Nodes verlangt -> Dann sind wir bei einer der Lösungen mit 2-3 Mandanten
	- Ist high-Availability weiterhin verlangt, auch wenn das mit erheblichen Einbußen bzgl. der Mandantenzahl und der Effizienz einhergeht?
	- [ ] Termin mit Michael Bier ausmachen
	- [ ] Termin mit Wiebke
- Einschätzung zum Betriebsaufwand von Dedizierten GPU-Karten von Jens Lindenberg
	- [ ] Termin mit Jens ausmachen
- Tatsächliche Risiken der unterschiedlichen GPU-Trennungsstufen müssen evaluiert und für die Entscheidungsträger verständlich dokumentiert werden
	- [ ] Fragen an Norbert zur Mail stellen📅 2026-06-07 
- Möglichkeiten zur Härtung der Sicherheit wie CoCo oder NCC müssen gegen die Risiken evaluiert und für Entscheidungsträger verständlich dokumentiert werden.
- Übersicht zu Möglichkeiten der virtuellen Trennung auf Namespace-Ebene einholen (von Steffen Lützenkirchen - alternativ von CC)
- Einschätzung bzgl. des Betriebsaufwandes einer Lösung mit Trennung auf Namespace-Ebene mit gehärteter Sicherheit von RedHat / CC


https://www.mindstudio.ai/blog/build-ai-second-brain-claude-code-obsidian

#### Ressourcen

##### Aufbau der Fusion

2 identische Racks, jedes hat:
- 2 GPU-Nodes: 
	- 8 H100 GPUs NVL (94GB)
		- FP8 Support
		- 3x faster inference than A100
		- bis zu 7 MIG-Slices
	- Verbunden mit NVLink (viel mehr Bandbreite als PCI und umgeht Weg über CPU)
- 3 Control Nodes
	- C10 - 32 Cores
- 3 Worker Nodes
	- C20 - 32 Cores
- 2 7.6TB NVMe Drives


##### Zusammenfassung der Möglichkeiten der Mandantentrennung

- **Hardware Trennung**
	- komplette Racks
	- CPU-Nodes (ist bei uns nicht möglich)
	- GPUs
		- Dedizierte Nodes
		- Dedizierte Karten
		- MIG
	- Speicher
- **Cluster**
	- Komplett eigene Cluster (ist bei uns nicht möglich)
	- Hosted Control Planes (nur 4 möglich)
- **Namespace-Ebene** (mit zusätzlichen Sicherheitsmaßnahmen)
	- Sandboxed Containers
	- CoCo + NCC
	- Subnetze
	- gute RBAC + ACCs