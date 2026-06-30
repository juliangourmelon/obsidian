
- [ ] Fragen an Florian: Wäre es auch möglich, die Verbindung zwischen den beiden Fusions hochzuschrauben? 📅 2026-06-09 
- [ ] Florian fragen, ob es ein Problem ist, dass alles was bei der Fusion Hardware-technisch gemacht werden muss, durch einen IBM-Techniker geschehen muss? 📅 2026-06-08 
- [ ] Florian fragen, ob Meeting mit mir und Daniel
- [ ] Eigene Gateways bei den Bedarfsträgern!!! 📅 2026-06-12 


Der entscheidende Unterschied ist, dass Mandanten nur noch über das AI-Gateway per Prompt auf die Plattform zugreifen können. Es können keine eigenen Container IN der Plattform gestartet werden in denen potentiell gefährlicher Code ausgeführt werden könnte. Natürlich können auch über Prompts diverse Angriffe ausgeführt werden: das wäre allerdings im ursprünglichen Modell ebenfalls ein Thema. Hier ist es allerdings noch relevanter, da oftmals mehrere Mandanten dasselbe Modell benutzen. Angriffe über Prompts können über das AI-Gateway (und entsprechende Sicherheit innerhalb der Modelle) abgefangen werden. (KV-Cache)



•Sehr hohe generelle Sicherheit, da die Mandanten / Bedarfsträger nicht direkt auf die Plattform zugreifen (z.B. keine eigenen Container starten, in denen sie gefährlichen Code ausführen könnten)

•Sehr effiziente Nutzung der GPUs

•Zugriffe / Tokennutzung / Rückverrechnung / etc. könnten sehr effizient über das AI-Gateway gesteuert werden

•Compliance im Sinne des EU AI-Acts kann sehr individuell eingestellt werden (Verschiedene Use Cases können je nach Risikoklassifizierung unterschiedliche Guardrails erhalten, auch wenn derselbe Modellendpunkt genutzt wird)

•Wir können zentral Guardrails einstellen (z.B. Bestimmten Teams / Bedarfsträgern die nutzung bestimmter Daten einschränken)

•Architektur kann in Zukunft zur Agenten-Plattform weiterentwickelt werden



•Wie groß ist die Gefahr des “Shadow in the Cache” tatsächlich in unserem Fall?

•Wie sehr lässt sich diese mittigieren?

•Guardrails im Gateway

•Confidential Computing

•KV-Cloak

•KV-Shield

•Getrennte Endpoints (auf derselben GPU)

•Zunächst auch hier GPU-Nodes/ Karten dedizieren bis das Problem gelöst ist und mehr als 4 Mandanten auf die Plattform kommen

•Wie groß ist die Gefahr im Vergleich zu Risiken der Mandantentrennung auf OpenShift Ebene?

•Kommen wir mit dieser Lösung durch den ISIP?