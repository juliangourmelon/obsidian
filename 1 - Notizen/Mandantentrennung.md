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

- GPU-Trennung
	- Ebene der Trennung
		- Node
		- GPU(-Karte)
		- MiG
		- Shared GPU (keine Option in Prod)
	- Zusätzliche Härtung der Sicherheit
		- NVIDIA Confidential Computing
		- OpenShift CoCo
- Sonstige Mandantentrennung:
	- Trennung auf Hardware-Ebene
	- Trennung auf HCP-Ebene
	- Weitere Maßnahmen, um Mandantentrennung zu härten:
		- Sandboxed Containers (Kata Container)
		- Verbesserte Netzwerktrennung
		- ... (weitere Vorschläge von Steffen Lützenkirchen, etc.)





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