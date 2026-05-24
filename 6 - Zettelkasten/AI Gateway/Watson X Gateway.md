Tags: [[AI_GATEWAY]]

## Demo IBM 21.05.2026 
vergleiche: [[Anforderungskatalog]]

- Am 10. Juni ist nächstes Release (Features dann auch on-prem)
- watsonx.ai wird zukünftig mehr auf red hat Technologien basieren
- DRV müsste für Lizenzen nichts extra bezahlen (DRV hat eh schon für den Softwarekatalog bezahlt -> ist wie prepaid katalog)
- Gateway hat infrastrukturtechnisch sehr kleinen Footprint (Governance auch)
- red hat openshift ai wird model privider ab Juni
- ansonsten alles möglich, was OpenAI kompatible Schnittstelle hat -> ist das bei IONOS alles kompatibel
- wenn wir Requirements haben, können bestimmte Features auch für uns auf die Roadmap gelangen
- Gibt Load Balancer (mit round robin und anderen Funktionalitäten)
- Azure AD Group kann hinzugefügt werden, dann gibt es Zugriff auf bestimmten Loadbalancer / oder bestimmte Models
- Gateway Deployment ist Operator (über IBM Softwarehub)
- Wie stellen wir ein, dass User nur über AI Gateway auf genau die Modelle in ihrem Namespace weiterleiten: 
	- Kommt mit Softwarehub: bringt auch multi tenancy features
	- Müssen aufpassen, dass das nicht unsere Multi-Tenancy bricht!
	- Aktuell eigene Routen pro Mandant -> darüber könnten wir filtern (mandant/namespacename/modell)
- Aktuell kann ich noch keine Input / Output Token messen -> allerdings geht das, wenn ich es mit watsonx.governance kombiniere -> model health => wird zusammenfürhung geben
- Governance ist Datenbank, die alle möglichen Artefakte speichern; Monitoring speichert alle Requests; LLM as a judge ist möglich
	- Guardrail Manager
	- Guardrail Manager ranked richtig hoch auch auf Deutsch
	- Kann bestimmte Guardrails implementieren
	- Modelle für beispielsweise Prompt-Shield können lokal deployed werden
	- (Idee Julian: Mit prompt shield oder ähnlichen Guardrails können wir die Einhaltung der Regeln auf der NonProd Umgebung garantieren, bzw. enforcen -> Prompts, die PII Daten enthalten werden automatisch geblockt) [[AI_GOVERNANCE]]
- Unterschiedliche Systemprompts pro Bedarfsträger sind aktuell nicht möglich -> müsste eher im Backend implementiert werden ^56894c
- Langfristig soll Gateway eine zentrale Controlplane für Modelle, Tools und Agenten werden
- Payload und audit logging soll implementiert werden (hier gibt mir Michael nochmal mehr Infos, wie das genau aussieht)
- Guardrails sollen auch direkt im Gateway implementierbar sein
- FinOps wird mit implementiert werden (chargeback)
- watsonx.ai würde es ermöglichen, llama modelle zu benutzen (ebenso bei mistral)
- Lizenzen für IBM und Red Hat werden konsolidiert (Red Hat AI Enterprise)
- würde wenige 10k an Lizenzkosten verbrauchen (Governance käme dazu und wäre nochmal teurer) -> Michael sendet uns genaue Kosten zu