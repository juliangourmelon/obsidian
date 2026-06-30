Tags:  [[MAAS]]
Links: [[Mandantentrennung]]


##### Gespräch mit Jens:

- [ ] Rausfinden, ob es bisher schon viele PaaS Use Cases gibt (eigenes Modell-Training) -> Master-Liste kann hier Aufschluss geben
- Evtl. wäre Training in der Nacht möglich
- Mehrere Gateways? -> pro Kunde ein eigenes Gateway bzw. einen Proxy (Ursprünglicher Vorschlag von Jens)
- Wo sollen die Gateways deployed werden?
	- Auf der Fusion?
	- Außerhalb der Fusion but innerhalb unserer Kontrolle?
	- Beim Kunden?
- Wir brauchen mindestens 2 "Verteidigungslinien" -> Zugriffssteuerung + spezielle Freischaltung auf bestimmte IPs
- 1 IP pro Kunde (und Pro Umgebung), dann spezifische Freischaltung
- "Selbst wenn Kunde A bei Kunde B zu besuch ist, kann er nicht auf dessen IP zugreifen"
- [x] Recherchieren, wie die zweite Verteidigungslinie über IPs funktioniert ✅ 2026-06-30


##### Gespräch mit Mohammad

- Bei Kong ist es möglich für unterschiedliche User unterschiedliche Pfade zu demselben Modellendpoint zu generieren
- [x] Recherchieren, was mir "unterschiedliche Pfade für unterschiedliche User" nutzen (Kong - Hinweis von Mohammad) ✅ 2026-06-30
- Besonders wichtige Modelle könnten auf eigene Endpunkte auf eigene GPUs ausgelagert werden (oder bei kleinen Modellen auch auf MIG)
- KV-Cache wird mit Session ID verknüpft (oder mit Request ID) -> So werden Anfragen nicht im KV-Cache vermischt
- Eigentliches Problem: KV-Cache speichert Zwischenergebnisse und verwendet diese wieder. dadurch können GPUs extrem effizient verwendet werden. Es werden aber (je nach konkreter Einstellung) teils auch Zwischenergebnisse aus anderen Sessions wiederverwendet. Wenn Beispielsweise zwei verschiedene Mandanten eine ähnliche Anfrage zu einem ähnlichen Versicherungsfall von aber einer anderen Person stellen, könnten die sensiblen Daten der einen Person theoretisch im Output der anderen Person landen
- Gateway kann auch im selben Cluster gehostet sein: vermindert Overhead
