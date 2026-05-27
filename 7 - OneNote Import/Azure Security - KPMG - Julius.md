Tags: [[AI_GOVERNANCE]]; [[AI_SECURITY]]


Dienstag, 14. April 2026
16:56
 
Model / Runtime Protection sollte nicht ausgelagert werden
 
(AI BOM)
 
Modelcar -> Logging / Audit 
 
 
 
Azure Foundry kann kompletten MLOps Zyklus abbilden. Kann benutzt werden?
 
User mit Input 
 
#### AI Gateway:
•	API
•	Prompt Shield (kann im OpenAI Service direkt integriert werden)
•	(Azure Functions: Custom Input Controls)
 
OpenAI / anderes LLM (mit prompt Logging enabled)
 
#### Output Controls:
•	Azure AI Content Safety kann in OpenAI Service enabled werden
o	Filter für typische Probleme: Sexuelle oder gewalttätige Inhalte, Policy Verletzungen
o	Kann auch für andere LLMs als API-Call zur Verfügung gestellt werden
•	LLM-as-a-Judge: kann direkt über OpenAI Service zur Verfügung gestellt werden, oder muss selbstständig implementiert werden (custom Aufwand)
o	Halluzination testen
o	RAG-Validation
o	Compliance Scoring
•	Confidance Score Validation: Wie sicher ist die Antwort des Modells? Wenn nicht sicher genug: Antwort blockiert oder geändert
•	Human in the loop (notwendig für viele AI Systeme nach EU AI Act!!!):
o	Azure Monitor
o	Application Insights
o	Logging Overviews (Geblockte Antworten werden analysiert)
•	Grounding / RAG Validation 
o	Azure AI Foundry
 
 
Generell wichtig: 
-> Sicherheitschecks!
-> Listen von bekannten gefährlichen oder unsicheren Prompts gegen System schicken
-> besonders wichtig, wenn es Custom Input oder Output Checks gibt
 
 
Typical Model Attack Vectors: 
•	Check Model Card
•	OpenAI transparency note
•	OpenAI system cards
 
-> Run Azure AI Evaluation & Azure Red Teaming Agent against the complete model flow with the the stated typical attacks that the model is known to be vulnerable against
 
 
 
 
 
User -> APIM -> Retrieval -> LLM -> Grounding check -> Custom validation -> Return / block / retry
 
#### Groundedness:
-> System Prompt kann helfen
-> Modell kann strukturierten Output zurückgeben
-> Azure AI Content Safety kann groundedness checks durchführen:
Run a groundedness check on the answer
Send:
•	query 
•	concatenated retrieved context 
•	generated answer 
to Azure AI Content Safety groundedness detection. The service is designed to detect when the response deviates from the provided source materials
 
Do not rely on one score alone. Add deterministic checks in your app:
•	every citation returned by the model must refer to one of the retrieved chunks 
•	every chunk cited must actually have been retrieved for this request 
•	if no citations are present, reject 
•	if retrieval returns weak evidence, either lower confidence or refuse 
•	if the answer contains named entities, dates, amounts, or IDs that do not appear in retrieved chunks, mark as suspicious 
That last rule catches a lot of hallucinations cheaply.
 
-> Wenn strukturierter Output:
1. Schema validation
Require structured output and validate it against your expected schema before doing anything else. Azure structured outputs help the model conform to the schema, but you should still validate server-side. Structured outputs support strict schema-driven generation; JSON mode alone only guarantees valid JSON, not schema compliance. 
2. Citation validation
For each cited chunk_id:
•	must exist in retrieved set 
•	must map to a known document 
•	must meet minimum retrieval score 
•	optionally require at least one citation per major claim 
3. Domain policy validation
This is your custom rules engine. Examples:
•	reject answers mentioning internal table names 
•	reject answers exposing email, IBAN, token-like strings, or customer IDs 
•	reject if answer contains prohibited business advice 
•	reject if answer exceeds confidence boundaries for regulated use cases
 
Keep fallback behavior explicit and predictable:
•	Grounding failed: “I can’t support that answer from the retrieved sources.” 
•	Schema failed: retry once with stricter schema reminder 
•	Business rule failed: return sanitized answer or refusal 
•	Sensitive data detected: redact and log
 
=> Integration Tests
 
 
#### LLM-as-a-Judge:
-> noch etwas mehr als groundedness check
-> custom business rules können getestet werden
-> coherence, fluency, relevance, groundedness, retrieval quality, or safety
 
Online (Tests) und Runtime Evaluation möglich
 
Direkt in Azure AI Foundry
Azure OpenAI API
Selber deployen
 
At a high level, the judge gets some combination of:
•	the user query 
•	the model answer 
•	optionally the retrieved context 
•	optionally the expected answer or ground truth 
•	a rubric 
Then it returns something like:
•	a score, for example 1–5 
•	pass/fail 
•	explanation or rationale 
•	sometimes per-criterion scores 
That matches how Azure frames evaluators: some are reference-free and judge the answer on its own or against the question, while others are reference-based, comparing the answer to source documents or a ground-truth answer.
 
 
#### Confidence Scores: 
-> Können durch LLM-as-a-Judge geliefert werden
-> bei klassischen ML Modellen 
-> sehr vorsichtig sein bei Word Probability!!!
 
•	No, most LLMs do not return default confidence scores for answers. 
•	Some expose token probabilities, but that is not true confidence. 
•	Real confidence is usually engineered from: 
•	retrieval strength 
•	grounding checks 
•	judge scoring 
•	validator outcomes 
•	consensus methods
 
 
OWASP GENAI Security Project:
 
 
Purview ist der zentrale hub für data governance.
Inhaltlich überprüfte Dokumente können dort markiert werden
 
#### RAG Security: 
•	Who can reach the system?
•	What data retrieval is allowed?
•	What is the model allowed to see and run?
 
Azure AI Search hinter private endpoints / lieber managed identities für Zugriff, als API Keys wenn möglich
Document Level Access Control in Azure AI Search
 
 
A secure Azure RAG system should guarantee:
•	only authenticated users and services can call it 
•	users only retrieve documents they are entitled to see 
•	prompts and indexed documents cannot easily inject hidden instructions 
•	sensitive data is not exposed through citations, answers, logs, or debugging 
•	abuse is throttled and observable
 
Do not build RAG around shared admin keys. Use:
•	Microsoft Entra ID for users 
•	Managed identities for service-to-service access 
•	Azure RBAC on Azure AI Search and other components
 
For enterprise RAG, also add:
•	citation-only answers for sensitive domains 
•	“no answer” when retrieval confidence is low 
•	redaction before response display 
•	policy checks before exposing raw snippets
 
4. Secure ingestion and indexing
Many teams protect the chat endpoint but forget ingestion.
During ingestion:
•	validate file type and source 
•	scan documents before indexing 
•	attach ACL metadata to each document/chunk 
•	avoid indexing secrets by default 
•	keep the original source URI, owner, classification, and retention metadata 
Azure AI Search’s document-level access model is most effective when authorization metadata is attached from ingestion through query execution. 
5. Log safely
Do not log full prompts, retrieved chunks, or model outputs indiscriminately in production if they may contain confidential data.
Log:
•	request ID 
•	user/app identity 
•	document IDs retrieved 
•	filter decisions 
•	policy hits 
•	latency and token usage 
Be careful with:
•	raw prompt bodies 
•	full search results 
•	quoted source content 
•	chat transcripts containing personal or regulated data
 
 
 
Fragen: 
Von wo sollten sich User Modelle und Software runterladen? Warum ist das im aktuellen Setup relevant?
Gibt es eigene Modelle, die deployed werden, oder können auch Modelle aus Foundry verwendet werden?
Sollen nur vorgefertigte Services verwendet werden, oder ist es auch möglich, Custom Code zu schreiben?
 
Posture Management?
PII Scanning nicht möglich mit Prompt Shield?
zScaler / Prisma Access
Azure Sentinel
Azure Shield

