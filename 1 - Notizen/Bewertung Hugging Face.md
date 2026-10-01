

Zusätzliche Gefahr durch den Angriff im Juli: 
- Repos könnten manipuliert worden sein, was eine Gefahr für unsere Lieferkette darstellt
- Hierüber könnte schädlicher Code in unsere Plattform geraten
- Hugging Face hat allerdings keine Hinweise auf einen solchen Vorfall gefunden





#### Offene Fragen:
- Können wir Modelle theoretisch von anderen Quellen beziehen?
- Können wir theoretisch schon geprüfte Modelle (von anderem Unternehmen) nutzen?
- Red Hat AI-Modelle?
- JFrog-Modelle?
- NVIDIA NGC?
- Können wir Modelle aus der Red Hat Registry als Model Car beziehen?



Microsoft Foundry:
-> Eigene Pipeline


Model Car Images





                    EXTERNE QUELLE
                         │
                  Model + Model Card
                         │
                         ▼
                ┌─────────────────┐
                │ 1. PROVENANCE   │
                │                 │
                │ Signature       │
                │ Hash            │
                │ Publisher       │
                └────────┬────────┘
                         ▼
                ┌─────────────────┐
                │ 2. ARTIFACT     │
                │    SECURITY     │
                │                 │
                │ JFrog Xray      │
                │ Malware / RCE   │
                │ Dependencies    │
                └────────┬────────┘
                         ▼
                ┌─────────────────┐
                │ 3. VALIDATION   │
                │                 │
                │ Accuracy        │
                │ Performance     │
                │ RHOAI / vLLM    │
                └────────┬────────┘
                         ▼
             ┌────────────────────────┐
             │ 4. BEHAVIORAL SECURITY│
             │                        │
             │ Garak                  │
             │ Jailbreak tests        │
             │ Prompt injection       │
             │ Harmful content        │
             │ Data leakage           │
             │ Tool abuse             │
             └───────────┬────────────┘
                         ▼
                 SECURITY REPORT
                         │
                   Approval Gate
                         │
                         ▼
                  Artifactory
                         │
                         ▼
                       RHOAI



**1. Provenance:** Woher stammt es? Signatur? Hash? Publisher?

**2. Artifact Security:** Malware, Pickle/RCE, Dependencies, Remote Code?

**3. Technical Validation:** Funktioniert es auf RHOAI/vLLM/NIM? Accuracy und Performance?

**4. Model Safety Evaluation:** Jailbreaks, Harmful Content, Data Leakage, Prompt Injection etc.?

**5. Application Security Evaluation:** RAG Prompt Injection, Tool Abuse, MCP-/Tool-Berechtigungen, System-Prompt Leakage, ABAC/RBAC-Bypass etc.?