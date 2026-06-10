Links: [[Artifactory Ticket]]

-> evtl. mehrere Teams, die eigene Modelle entwickeln oder finetunen.
-> Große Modelle mit hoher Precision verbrauchen teils mehrere hundert GB.
-> Wenn dasselbe Modell für unterschiedliche Mandanten zur Verfügung gestellt wird, muss es evtl. mehrfach gespeichert werden.
-> Auch Modelle die aktuell nicht benötigt werden, sollen unter Umständen kurzzeitig auf der Artifactory gespeichert bleiben. (Natürlich wollen wir aber keinen "Modellfriedhof" auf der Artifactory haben.)
-> Evtl. müssten wir den Speicher fix zwischen den Mandanten aufteilen. Dann hätten wir 4 mal die Gefahr, dass der Speicher ausgeht.
-> Speicher wird unter Umständen nicht nur für Modelle benutzt, sondern auch andere Artefakte.