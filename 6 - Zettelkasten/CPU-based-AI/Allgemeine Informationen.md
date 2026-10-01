

### Typische KI-Anwendungen ohne GPU

|Anwendung|CPU-Eignung|Typische Modelle/Technologien|
|---|---|---|
|**Embedding-Erzeugung**|sehr gut|BGE-small/base, E5-small/base, kleinere Sentence Transformers|
|**Reranking**|gut bis sehr gut|kleine Cross-Encoder, MiniLM-basierte Reranker|
|**Vector Search**|sehr gut|FAISS, pgvector, OpenSearch, Milvus CPU|
|**Textklassifikation**|sehr gut|BERT-small, DistilBERT, klassische NLP-Modelle|
|**NER / PII Detection**|sehr gut|spaCy, BERT/DistilBERT, Presidio|
|**Content Moderation**|sehr gut|kleine Transformer/Klassifikatoren|
|**klassisches Machine Learning**|hervorragend|XGBoost, LightGBM, Random Forest, sklearn|
|**Anomalie-/Fraud Detection**|sehr gut|XGBoost, Isolation Forest etc.|
|**Predictive Maintenance**|sehr gut|klassische ML- und kleinere DL-Modelle|
|**OCR / Dokumentenklassifikation**|gut|OCR + kleine Layout-/Classifier-Modelle|
|**Offline Speech-to-Text**|teilweise gut|kleine Whisper-Varianten|
|**kleine LLMs / SLMs**|gut bei moderaten Anforderungen|ca. 1B–8B, teilweise größer, quantisiert|
|**LLM Guardrails**|häufig sehr gut|PII, Prompt-Injection-Classifier, Toxicity|
|**Agent-/RAG-Infrastruktur**|überwiegend CPU|Retrieval, Tool-Calling, Gateway, Policy Engines|