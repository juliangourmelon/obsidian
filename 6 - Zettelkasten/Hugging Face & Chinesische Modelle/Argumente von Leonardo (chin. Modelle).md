Links: [[Argumente für die Freischaltung von Hugging Face|Argumente für die Freischaltung von Hugging Face]]


- chinesische Modelle sind größtenteils auf denselben Datensätzen trainiert wie amerikanische Modelle
- auch amerikanische Modelle legen nicht alle Daten offen, mit denen die Modelle trainiert werden
- chinesische Modelle scoren hoch in Benchmarks, die faktische Korrektheit überprüfen
- wir würden allgemeine Sicherheitsstandards einhalten (fixierte Versionen; nur safetensors) -> Mögliche Angriffe könnten nur über das Verhalten des Modells stattfinden
- chinesische Modelle werden nur in Airgapped Environments verwendet und unter Human-in-the-Loop (jede Entscheidung des Modells muss von einem Menschen bestätigt werden)
- für bestimmte Cases sind chinesische Modelle die beste oder sogar die einzig valide Wahl


-> Möglich wäre die Entwicklung eines standardisierten Überprüfungsprozesses (SIKO)