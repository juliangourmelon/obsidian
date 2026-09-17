
Link: [[Mandantentrennung]]

- Die GPUs sind in mit NVLink miteinander verbunden: eventuell ist das ein Problem
- [x] Rausfinden, ob die Verbindung der GPUs per NVLink für die Mandantentrennung auf GPU Ebene ein Problem ist 📅 2026-06-09 ✅ 2026-09-17
- [x] Recherche: was genau ist der Lizenz-Server, VM-Ware vs. Bare Metal Cluster ✅ 2026-09-17
- [x] Dokumente von Ralf durchlesen 📅 2026-06-09 ✅ 2026-09-17
- Wenn wir ein dediziertes MaaS Cluster haben, in dem wir alle Container selber kontrollieren, evtl. ist es dann nicht mehr so schlimm, dass wir keine Mandantentrennung auf Hardware-Ebene haben
- [x] Mohammed zu MaaS mit verschiedenen Mandanten und hohem Schutzbedarf befragen 📅 2026-06-09 ✅ 2026-09-17
- [x] Termin mit Ilonka und Ralf einstellen 📅 2026-06-09 ✅ 2026-09-17
- Es gäbe noch die Lösung auf dem Bare Metal Server (Fusion) VM Ware zu installieren, und dann virtuelle Maschinen über MIG zu starten (siehe Word Dokument von Ralf)
- Die Virtualisierung innerhalb von Mandanten wäre natürlich möglich.
- Ralf sagt, dass MIG-Partitionierung für Mandantentrennung nicht gut ist [[Notizen GPU-Gespräch Leonardo]]
- Die Configuration von MIGs ist natürlich nicht so einfach, es gibt wohl Möglichkeiten, das aber mittlerweile direkt aus der Container-Umgebung heraus zu machen

