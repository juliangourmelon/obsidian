

#### Gespräch mit Florian 23.08.
- Infos aus ESXi-Team: ungern die Bandbreite erweitern (neue Netzwerkkarte hinzufügen ist aufwändig) -> Team von Arthur Honisch
- Die Artifactory wird aktuell auf VMs gehostet
- Hier ist das hinzufügen mit Schwierigkeiten verbunden, die das Team nicht auf sich nehmen möchte
- Alexander Preuss könnte das Team evtl. zwingen (oder Martin über Willhelm Raus)
- Alternativ gibt es die Option, die Artifactory auf Bare Metal zu deployen
- Alexander Preuss kann mir mehr über die Artifactory und über "Zar" erklären
- 6 Int; 2 freihalten; 4 belegt




#### Schwierigkeiten Netzwerkkarte hinzuzufügen bei VMs:
=> Rausfinden, was wirklich das Problem ist

- Hochverfügbarkeit (Müsste auf mehreren physischen Servern erfolgen)
- PCIes müssten verfügbar sein
- Kühlung und Strom müssen verfügbar sein
- ESXi erkennt den neuen physischen Netzwerkadapter als weitere vmnic. Anschließend muss diese NIC als Uplink dem passenden virtuellen bzw. verteilten VMware-Switch zugeordnet werden. Zusätzlich müssen gegebenenfalls die Teaming- und Failover-Einstellungen angepasst werden. Broadcom weist ausdrücklich darauf hin, dass beim Austausch oder Hinzufügen physischer Netzwerkadapter eine Neuzuordnung der physischen vmnic-Geräte zu den Uplinks eines VMware Distributed Switch (VDS) erforderlich sein kann. In bestimmten Konfigurationen kann das Hinzufügen neuer Hardware sogar dazu führen, dass sich die Nummerierung der vmnic-Schnittstellen ändert. Wenn das nicht korrekt berücksichtigt wird, können bestehende Zuordnungen dadurch ungültig werden oder nicht mehr funktionieren.



#### Fragen:
- Wie viele PCIes sind verfügbar?
- What Switch-Ports are available?
- Sind wirklich die NCIs das Bottleneck?



#### Gespräch Alexander Preuss 31.08.2026

- 100 Gbit Bandbreite ins Internet wird aktuell nicht funktionieren. Proxy wird durch andere Abteilung gemanaged und aktuell gibt es nur eine 1-5 Gbit-Verbindung, die mit anderen Abteilungen geteilt wird.
- Artifactory -> Fusion: 100 Gbit wird es auch erstmal nicht geben. Erst, wenn die Migration auf Bare Metal durchgeführt wird (im März 2027). Aktuell ist es mit dem VMWare-Cluster nicht möglich mehr als 10 Gbit umzusetzen. VMWare bietet nicht mehr Durchsatz, das ist ein harter Cut.