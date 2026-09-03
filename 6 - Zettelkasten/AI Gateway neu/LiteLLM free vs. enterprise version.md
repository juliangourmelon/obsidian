Tags: [[AI_GATEWAY]]

|Area|LiteLLM OSS / Free|LiteLLM Enterprise|Why Enterprise matters|
|---|---|---|---|
|Model gateway / OpenAI-compatible API|✅|✅|No major reason to buy Enterprise just for routing|
|Virtual keys|✅|✅|Free already provides good application-level access keys|
|Users & teams|✅|✅|Basic multi-tenancy is already possible|
|Budgets / RPM / TPM limits|✅|✅|Cost/rate governance does not require Enterprise|
|Spend tracking|✅ key/user/team|✅ including richer org/tag use|Useful for chargeback across business units|
|Guardrails|✅|✅|Guardrails themselves are **not an Enterprise-only capability**|
|Logging|✅|✅|Basic request/response logging available in OSS|
|Prometheus|✅|✅|Monitoring itself doesn't require Enterprise|
|**SSO**|❌ / limited|✅|Users can log in with your corporate IdP|
|**SCIM**|❌|✅|Automatic user/team provisioning/deprovisioning|
|**OIDC/JWT authentication**|Enterprise feature|✅|Important when integrating existing identity infrastructure|
|**Hierarchical RBAC / Org admins**|limited|✅|Delegated administration for multiple departments|
|**Audit logs**|❌|✅|Important for security/compliance investigations|
|**Secret Manager integration + key rotation**|limited|✅|Better lifecycle management of provider/API secrets|
|**Multi-region control plane**|❌|✅|Useful for highly available / geographically distributed deployments|
|**Air-gapped enterprise deployment**|Enterprise offering|✅|Particularly relevant for restricted environments|
|Vendor support|Community|✅ SLA / up to 24×7|Major operational advantage|
|Dedicated onboarding|❌|✅|Useful during platform rollout|
|Commercial SLA|❌|✅|Important if LiteLLM becomes critical infrastructure|


Besonders wichtig meiner Meinung nach: Audit Logs und SSO

- Sandro hat gesagt, dass SSO anderweitig integrierbar wäre?
- Können wir das Problem mit dem fehlenden Multi-Region-Cluster Support umgehen? => wir sind eh nicht KRITIS?


