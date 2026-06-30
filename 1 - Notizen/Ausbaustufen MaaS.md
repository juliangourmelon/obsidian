

Ausbaustufe

###### Stufe 1:

Jeder Bedarfsträger hat noch eigenen Node

Aller Traffic geht über API-Gateway (liteLLM) -> mit entsprechender Sicherung (dedizierte virtuelle IP; Reverse Proxy; evtl. eigenes Gateway im eigenen Tenant)

Grundlegendes Logging und Monitoring sind implementiert
Anforderungsanalyse des AI-Gateways ist abgeschlossen und eine diesbezügliche Bewertung der möglichen technischen Lösungen (WatsonX Gateway; Kong; liteLLM + liteMaaS) ist abgeschlossen

Zukunftsfähiger Modellfreigabeprozess ist implementiert

###### Stufe 2:

Bedarfsträger nutzen noch eigenen Nodes / dedizierte GPUs
NonProd und Prod sind hardwaretechnisch getrennt
AI-Gateway ist implementiert und stellt ein Zugriffskonzept, zentrales Logging, sowie die notwendigen Guardrails zur Verfügung
Logging und Monitoring folgen den EU AI Act- & DSGVO-Anforderungen 
User können eigene Guardrails einstellen (entweder im eigenen Gateway oder in unserem)
Die Use Cases sind nach Aufwand, Priorität, EU-AI Act und Datenschutzbedarfsstufe eingeordnet

**Produktivsetzung**
###### Stufe 3:

Bedarfsträger nutzen geteilte GPU-Hardware. Besonders kritische Endpunkte werden auf dedizierten MIG-Partitionen zur Verfügung gestellt
AI-Gateway implementiert entsprechende Guardrails, um das Problem mit dem KV-Cache zu lösen
Generell sind die entsprechenden Maßnahmen zur Mittigierung des Cache Problems bewertet und umgesetzt
Mit Hilfe des Monitorings wird kontinuierlich weiter an der Effizienzsteigerung der GPU und sonstigen Hardware gearbeitet
AI-Gateway ist echter Self-Service: Bedarfsträger können (in ihrem Rahmen) eigene Rollen und Rechte vergeben, Modelle starten und Feedback über ihre eigene Token-Nutzung erhalten
Fester Prozess für die Umsetzung neuer Use Cases ist eingerichtet



#### Noch nicht umgesetzt:

-> Sonderlösung: Der Bedarf nach Token wächst so schnell, dass bereits frühzeitig eine effizientere Nutzung der Hardware vorgenommen werden muss: die Use Cases müssen schneller bewertet werden, um solche mit "normalem" Schutzbedarf direkt auf geteilte Endpunkte (mit geteilter Hardware auszulagern).


-> Produktivsetzung


-> Human-in-the-loop im AI-Gateway

-> Data Classification Policies (bestimmte PII-Daten werden automatisch erkannt und entsprechende Modelle geblockt)
-> Prompt Shield: prompt injection, jailbreak attempts, malware generation, data exfiltration attempts are blocked

-> Data Residency Control (in unserem Fall ähnlich zu Data Classification Policies: welche Daten dürfen wo hin geschickt werden?)

-> Human-in-the-Loop Gateway

