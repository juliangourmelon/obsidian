
Montag, 4. Mai 2026
13:32
 
•	Bedarfsträger = Ein Team innerhalb eines Mandanten
•	Mandant = Ein Träger innerhalb des DRV (juristische Person)
•	User = Ein einzelne Person (Data Scientist, Data Engineer, etc.), die einem Bedarfsträger zugehört
•	Stakeholder = Mandanten + Management der DRV + Security Abteilungen (generell alle Abteilungen, die über uns stehen)
•	Use Case = Anwendungsfall für ein LLM-Modell der durch die Bedarfsträger eingebracht wird.
•	Tenant = Eigener Abschnitt der Rechenzentrums. Netzwerktechnisch getrennt von anderen Tenants.
•	Service-Schnitt = Das Level an Unterstützung oder technischen Artefakten, dass wir den Bedarfsträgern bieten? Beispiel: Wie viele Guardrails stellen wir zur Verfügung? Erhalten Teams nur Zugang auf RHOAI oder stellen wir auch Images, Pipelines, etc. zur Verfügung?
•	PaaS = Cloud-Modell bei dem den Usern eine fertige Plattform bereitgestellt wird, auf der sie arbeiten können. (In unserem Fall RHOAI.)
•	MaaS = KI-Modelle werden als Endpunkte über eine API zur Verfügung gestellt. In unserem Fall ist diese API Teil eines AI Gateways 
•	AI Gateway = zentrale Zugriffsschicht zwischen Usern/ Bedarfsträgern und verschiedenen KI-Modellen (Endpunkte auf der Fusion & externe Modelle), die Anfragen bündelt, steuert und überwacht. Übernimmt Routing, Authentifizierung, Kostenkontrolle, Logging sowie das Durchsetzen von Guardrails. [[AI_GATEWAY]]
•	Custom Notebook Images = Umgebungen für RHOAI Workbenches, die eigens von uns erstellt wurden. Bsp. Python Base Image + zusätzliche Packages)
•	Data Science Piepeline = Kubeflow-Pipeline in RHOAI, die verschiedene Schritte der KI-Trainings- oder Deployment-Prozesses durchführt
•	LLM Inference Security = Alle Maßnahmen, die helfen ein LLM in Verwendung (User senden Prompts) sicher zu gestalten. Beinhaltet die entsprechenden Guardrails, die Runtime Security von vLLM/ KServe, als auch die Governance der verwendeten Trainings- oder RAG-Daten
•	Guardrails = Maßnahmen die Ausgaben eines LLMs begrenzen und lenken, um Sicherheit, Korrektheit und gewünschtes Verhalten zu gewährleisten. (Content-Filter; Output-Formatierung; Grounding = Modell darf nur auf bestimmte Daten zugreifen) [[AI_GOVERNANCE]]
•	Anforderung = Beschreibt was ein Softwaresystem (in unserem Fall die RHOAI-Plattform auf der Fusion) leisten soll. In unserem Fall getrennt nach Anforderungen aus Use Case und Anforderungen aus Plattform Sicht. [[Anforderungskatalog]]
