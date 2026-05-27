Tags: [[AI_GATEWAY]]

Links: [[LiteMaaS]]



Features: 
- Model Fallbacks: (Fehler in einem Modell -> Anfrage wird an anderes Modell weitergeleitet)
- Cost Aware Routing:
- Hybrid Routing: 
	- PII Daten -> internes Modell
	- öffentliche Daten -> externen Modell
- Mit Prometheus / Grafana integrierbar
- Observability: 
	- Input Tokens
	- Output Tokens
	- Total Cost
	- RPM / TPM
	- Latency
	- Error Rate
	- Provider Errors
	- Cache Hits
	- Budget Usage
- Security & Governance:
	- JWT Auth
	- RBAC
	- SSO
	- Audit Logs
	- Guardrails
	- PII Masking
	- Prompt Injection Detection
	- Budget Limits
	- Team Isolation
	- IP Allow Lists
- LiteLLM kann auch als MCP Gateway agieren