Tags: [[AAP]]

Links: [[Ansible Intelligent Assistant Use Case]]


Hier eine Kurzzusammenfassung der Ansible Lightspeed Use Cases:

1) Unterstützung bei der operativen Arbeit mit Ansible Workflows, Automatisierungen und Serverwartung (sehr wichtig: Prio 1) [[Ansible Intelligent Assistant Use Case]]

2) Git-Lab Review-Hilfe von Ansible Code (sehr interessant: Prio 2)

3) Einbindung Visual Studio Code zur Erklärung von Code, bzw. abstrahierten Python Packages, die für den Entwickler nicht direkt einsichtig sind (erstmal nicht stark priorisiert)

4) Unterstützung für die Arbeit mit checkmk und den Loadbalancern (aktuell auch nicht so wichtig)

Bzgl. der User und des Business Values bin ich mir unsicher, ob ich mich korrekt erinnere (wir hatten parallel auch einige wichtige andere Themen in den Telefonaten besprochen). Aktuell hat Florian wohl ein Team aus 4 Entwicklern, das große Teile des Rechenzentrums mit Ansible-Automation serviciert und mit dem Workload nicht mehr hinterherkommt. Müssen wir dann im Gespräch erfragen.

Anmerkungen zu den Use Cases:

Generell hat Ansible Lightspeed diese Zwei Komponenten:

**The Ansible Lightspeed** with IBM watsonx Code Assistant, which helps automation developers create content for single tasks, multiple tasks, Ansible Playbooks, and Ansible Roles.

**The Ansible Lightspeed intelligent assistant**, which guides administrators to install, configure, maintain, and optimize Ansible Automation Platform while helping IT operators analyze, troubleshoot, and optimize automation jobs and workflows.

Use Case 1 und 4 benötigen den **Intelligent Assistant**, Use Case 2 und 3 benötigen den **Code Assistant.** sdaDer Code Assistant soll allerdings nur für den Review und die Erklärung von Code verwendet werden. Ihn eigenen Code erzeugen zu lassen, hält Florian für zu riskant.

Erste technische Einschätzung von mir (ohne Gewähr): Der Coding Assistant würde auf der Fusion sowohl die IBM watsonx Code Assistant API als auch ein speziell fine-getuntes Modell (granite) benötigen. Der Intelligent Assistant benötigt auf der Fusion erstmal nur einen granite-Endpoint (den wir ja theoretisch schon haben). Der entsprechende Service müsste auf Seite von Florian installiert werden.