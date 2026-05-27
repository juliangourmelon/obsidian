Tags: [[AI_GATEWAY]]

Links: [[LiteLLM]]


- MaaS-Interface on top of LiteLLM
- Self-Service Portal; [[LiteLLM]] ist das eigentliche Gateway


##### LiteMaaS Portal: 
- Modellkatalog  
- Subscriptions  
- API Keys  
- Budgets / Usage  
- RBAC  

##### LiteLLM Proxy / AI Gateway: 
- Routing zu internen & externen Modellen  
- Token-/Kostenmessung  
- Guardrails  
- MCP Gateway  
- Logging / Metrics


## Bewertung gegen den Anforderungskatalog (Stand 25.05.)

| Anforderung                                            | Einschätzung mit LiteMaaS/LiteLLM                                                                                                                                                                                                                                |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Integration des [[MCP-Gateways]]**                   | **Gut möglich über LiteLLM.** LiteLLM bietet ein MCP Gateway mit festem Endpoint für MCP Tools sowie Access Control nach Key, Team und Organization. Unterstützt werden u. a. Tool Listing, Tool Calls, Prompts, Resources sowie Streamable HTTP, SSE und stdio. |
| **Input Tokens / Output Tokens messen**                | **Ja.** LiteMaaS nennt Token Consumption und Costs in User- und Admin-Views; LiteLLM bietet Usage/Spend Tracking und Prometheus-Metriken.                                                                                                                        |
| **Latenz messen**                                      | **Ja, Gateway-seitig.** LiteLLM/Datadog-Integration nennt Request Volume, Latency, Errors, Fallbacks, Token Usage und Costs.                                                                                                                                     |
| **Time to First Token**                                | **Teilweise.** Für selbst gehostete vLLM-Modelle ist TTFT nativ als vLLM-Metrik verfügbar. Gateway-seitig hängt es davon ab, ob Streaming sauber instrumentiert wird.                                                                                            |
| **Error Rate**                                         | **Ja.** Über Gateway-Logs/Metriken, Datadog/Prometheus und Provider-Fehler.                                                                                                                                                                                      |
| **Eigener Systemprompt pro Modell**                    | **Möglich, aber sauber designen.** LiteLLM hat Prompt Management und Developer/System Instructions; für Modell-spezifische Standardprompts würde ich eher Prompt Management oder einen Custom Prompt Manager nutzen, nicht „hart“ im Modellrouting verstecken.   |
| **Weiterleitung an interne und externe Modelle**       | **Sehr passend.** LiteLLM routet zu vielen externen Providern und kann interne OpenAI-kompatible Endpunkte wie vLLM/RHOAI/KServe anbinden.                                                                                                                       |
| **Unterschiedliche Modellangebote je User**            | **Ja.** LiteMaaS bietet Subscriptions, Restricted Access Models und RBAC; LiteLLM bietet Virtual Keys, Teams, Budgets, Rate Limits und Model Access.                                                                                                             |
| **Eigene Modelle hinzudeployen, nur eigener Zugriff**  | **Architektonisch ja.** Das Modell wird als eigener Endpoint deployed und nur bestimmten Keys/Teams/Subscribers freigegeben. LiteMaaS müsste hier den Self-Service-Workflow abbilden.                                                                            |
| **Zugriff später weitergeben**                         | **Ja.** Über Subscription Approval, Team-Zuordnung, Key-Scopes oder Admin-Freigabe.                                                                                                                                                                              |
| **Selbst deploytes Modell zählt zur eigenen Rechnung** | **Ja, aber mit Zusatzlogik.** LiteLLM kann Spend/Budget pro Key/Team tracken; bei internen Modellen braucht ihr ein internes Pricing-Modell, z. B. €/1k Token, GPU-Minuten, Deployment-Größe oder Reservationskosten.                                            |
| **User können Governance/Guardrails einbinden**        | **Ja.** LiteLLM unterstützt Guardrails u. a. für Prompt Injection Detection und PII Masking; Guardrails können pre-call und post-call laufen.                                                                                                                    |
| **Zentrale Governance durch Plattformteam**            | **Ja.** Zentral im LiteLLM Proxy als Pflicht-Guardrails, Logging, Policies, Routing, Budgets und Rate Limits.                                                                                                                                                    |
| **Feingranulare Governance je Mandant/HCP**            | **Grundsätzlich ja.** LiteLLM kann Zugriffe nach Key/Team/Org steuern; JWT-to-Virtual-Key-Mapping erlaubt granular controls wie model restrictions, spend limits, rate limits, guardrails und spend tracking, ist aber als Enterprise Feature gekennzeichnet.    |
| **GPU-Größe selbst wählen**                            | **Nicht Kernfunktion von LiteMaaS/LiteLLM.** Das gehört eher in RHOAI/KServe/OpenShift Scheduling: User wählt Deployment-T-Shirt-Size, dahinter werden GPU Requests, Node Pools, MIG/vGPU/dedizierte GPU und Autoscaling gemappt.                                |


