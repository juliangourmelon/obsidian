- [x] Infos und Fragen zu dem Problem mit dem Modell-Download an Florian / Jens [[Networking Rechenzentrum#^c3e4b1]] ✅ 2026-05-27

- [x] Daniel zum Model Repository befragen [[Artifactory#^f81aa3]] ✅ 2026-05-27

- [x] Repo-Größe erhöhen -> Frage an Florian ✅ 2026-05-27

- [x] Frage an Daniel: welche git-Plattform wird verwendet? ✅ 2026-05-27

- [x] Daniel nachfragen zu aktuellem Stand der Mandantentrennung (Dokumentation) ✅ 2026-05-27

- [x] Anforderungen: Norbert gibt mir ein Template, ich erstelle dann das Anforderungsdokument. Dann an Jens Brandenburg schicken (JEns fragen, ob er ein Template hat) ✅ 2026-09-17


- [x] Arbeitspakete: In DIMA dokumentieren; dann wenn Änderungen: Change-Request. An Caprice schicken -> Stand wie er beim Kick-Off war. Caprice soll Struktur bauen, die Arbeitspakete anzulegen und auch ändern zu können. (evtl. Arbeitspakete als Jira-Tickets. Aktuell aber erstmal in Confluence.) ✅ 2026-05-27


- [x] LLM-Metriken möglichst schnell in das Architekturkonzept übernehmen. Was wollen wir messen; was wollen wir nicht messen -> In Arbeitssessions pro/contra durchgehen; (Prio 2) ✅ 2026-09-17

- [x] An Anforderungsliste für AI-Gateway weiterarbeiten. Und nochmal Blick auf die Open Shift Version werfen. -> Red Hat Technologien haben prio ✅ 2026-09-17


- [x] Beantragen, mehr Speicherplatz zu bekommen in der Artifactory ✅ 2026-09-17

- [x] Mehr Bandbreite für Fusion -> Artifactory ✅ 2026-09-17


- [x] Bei Florian nachhaken, warum download in Artifactory nicht gut läuft. (wir gehen wohl über legacy artifactory -> das ist der erste Proxy). ✅ 2026-05-27

- [x] An Daniel und Tedi: Können uns auch mal anschauen, wie die Bandbreite bei rvEvo aussieht. Gibt es bereits erste Indikationen für Bottlenecks ✅ 2026-05-27


- [x] Hat Jens Brandenburg eine Struktur für ein Architekturkonzept? ✅ 2026-09-17

- [x] Folgetermin mit Ralf und Martin (Themen mit Martin vorbereiten) 📅 2026-06-02 ✅ 2026-09-17
- [x] Ist der Intelligent Assistant Service kostenpflichtig? 📅 2026-05-31 ✅ 2026-06-02
- [x] Mit Daniel sprechen zur Freischaltung des granite Endpoints 📅 2026-06-01 ✅ 2026-06-01
- [x] Ansible Lightspeed Use Case in Masterliste übernehmen 📅 2026-06-01 ✅ 2026-06-02
- [x] Rausfinden, welche Availability wir brauchen für AAP (sonst können wir die Fusion Systemtest benutzen) ✅ 2026-09-17
- [x] 25 GiB Leitung Recherche ✅ 2026-06-01
- [x] Wir brauchen Work Order für netzwerk zur Artifactory (nach außen nur 25 Gigabit nicht mit 50 wir können auf 100 gehen mit workorder an Artifactory) ✅ 2026-06-30

- [x] Use Case Liste durchlesen ✅ 2026-06-30
- [x] Morgenroutine #sonstiges ✅ 2026-09-17
I think we might have overengineered this problem a little too much. Let's take a step back and leave out the watermark tables and the API retries for now.

I would still like the basic logic where I do an initial full load and then delta loads (and every two weeks a reconciliation loop = full load again). Let's image I do the extra step of first downloading everything as .gz files. Then I would load it into bronze and then do the silver scd2 historization.

Am I right in the assumption that I will need two different forms of historization for silver (AUTO CDC for the delta loads and AUTO CDC FROM SNAPSHOT for the reconcilliation loop)? Are there two different API versions for the defender knowledge base too? One where I get the current state for the full loads and one where I get changes since a specific date? Will those changes already have a column I need for AUTO CDC (deleted, changed, new)? Does it then make sense to have two different bronze tables?