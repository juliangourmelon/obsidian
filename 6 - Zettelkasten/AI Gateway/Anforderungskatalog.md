Tags: [[AI_GATEWAY]] [[MCP_GATEWAY]]


- Integration des MCP-Gateways
- Messen von:
	- Input Tokens
	- Output Tokens
	- Latenz
	- Time to first token
	- Error Rate
- Eigener Systemprompt pro Modell
- Weiterleitung an interne und externe Modelle (hybride Strategie)
- Unterschiedliche Angebote von Modellen für unterschiedliche User
- Eigene Modelle hinzudeployen -> nur ich habe dann darauf Zugriff, außer ich möchte den Zugriff weitergeben
- Selbst deploytes Modell muss auch zur eigenen Rechnung dazuzählen
- Einbindung von Governance (e.g. Guardrails wie Prompt Shield zum Filtern von PII Daten in NonProd oder Output Controls im Sinne von LLM as a judge) ist möglich für die User
- Einbindung von Governance ist möglich für uns an zentraler Stelle
- Governance Einbindung kann feingranular eingestellt werden (bestimmte Guardrails für bestimmte Mandanten oder HCPs)
- (GPU-Größe selbst wählen)
- **Neu ab 10.06.**
- Deployment muss mit ArgoCD automatisierbar sein
- Wie die User ihre Zusätze (Guardrails) deployen ist noch offen:
	- Eigene ArgoCD Instanz (aktuell bevorzugt)
	- Konfiguration per UI hinzufügen (könnte schwierig werden)
	- Zusätzliches eigenes Gateway im eigenen Tenant (könnte schwierig werden)
	- Merge Request an uns stellen (sehe ich auch eher schwierig)
- Gateway muss hoch-verfügbar sein
- Gateway muss KV-Cloak implementieren können
- Muss auch sonstige Custom-Guardrails hinzufügen können
- Muss verschiedene IPs zur Verfügung stellen, damit unterschiedliche User auf das Gateway über unterschiedliche Firewallfreischaltungen zugreifen können
- Gateway muss viele gleichzeitige Requests handeln können

## Kategorien: 

### Routing (API-Gateway Funktionalitäten)

- Weiterleitung an interne und externe Modelle
- User Authentifizierung

### Governance

- Einbindung von Governance ist möglich für uns an zentraler Stelle

#### Allgemein

- Logging für Auditierung
	- Anfragen
	- User
	- Errors
	- Prompts
	- Responses

#### Guardrails

- Einbindung von Guardrails durch uns
	- Prompt Shield zum Filtern von PII Daten in NonProd
	- Output Controls (e.g. LLM as a judge)
- Einbindung von Guardrails durch User
	- Ergänzend zu unseren Guardrails
- Governance Einbindung kann feingranular eingestellt werden (bestimmte Guardrails für bestimmte Mandanten oder HCPs)

### Metriken

	- Input Tokens
	- Output Tokens
	- Latenz
	- Time to first token
	- Error Rate

### Mandantentrennung

- Gateway darf die Mandantentrennung nicht "brechen" 
	- User dürfen nur auf ihre eigenen Modellendpunkte weitergeleitet werden
- Mandantentrennung muss weiterhin an zentraler Stelle kontrollierbar sein

### Zukunftsfähigkeit

- Integration eines MCP Gateways

### User Self-Service und Betriebsmodelle

- Eigene Modelle dazu deployen -> nur ich habe dann darauf Zugriff, außer ich möchte den Zugriff weitergeben
- Selbst deploytes Modell muss auch zur eigenen Rechnung dazuzählen
- (Eigener Systemprompt pro Modell) [[Watson X Gateway#^56894c]]]
- GPU-Größe selbst wählen


### Nice to haves:

- Effizientes Routing (bestimmte Anfragen gehen an bestimmte Modelle)