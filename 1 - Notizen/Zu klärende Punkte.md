
- [ ] Wir müssen uns überlegen, wie viel Speicherplatz wir in der Artifactory brauchen und wie viel Speicher wir den jeweiligen Bedarfsträgern zugestehen [[Artifactory#^125f05]]
- [x] Probleme beim Networking beheben ✅ 2026-05-27
	- Internet -> Artifactory
	- (Artifactory -> Fusion)
- Modelle von Artifactory -> Fusion
	- Wie oft werden die Modelle von dort gezogen?
		- jeden Tag wegen BSI?
		- immer wenn Endpunkt das erste Mal an dem Tag angesprochen wird?
	- Lohnt es sich, Modelle auf der Fusion zwischenzuspeichern? Wenn ja, welche? (klein, groß, häufig verwendet)
- [ ] Wann und wie werden Modelle in der Artifactory gescannt? #ongoing
	- beim Download?
	- gibt es bereits fertige Tekton Build Pipelines?
	- jedes Mal, wenn sie gezogen werden aus der Artifactory? (ist ja irgendwie Overkill, wenn sie dort unverändert liegen, aber evtl. BSI-technisch relevant?) 
- Wie schaffen wir es, die Mandantentrennung nicht zu brechen mit dem AI-Gateway? [[Anforderungskatalog#Mandantentrennung]]



- [ ] Architekturkonzept #ongoing
- [ ] Erhöhung Bandbreite Artifactory -> Fusion #ongoing 
- [ ] Anforderungsliste AI-Gateway #ongoing 