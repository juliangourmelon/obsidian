
- API Load verbessern
- Snapshots aus Bronze selber holen
- Expectations einfügen (auch schon in bronze)
- schemaEvolutionMode in Bronze und Silber einfügen
	- `# Allow Auto Loader to add newly appearing fields .option( "cloudFiles.schemaEvolutionMode", "addNewColumns" )`
	- addNewColumnsWithTypeWidening
	- .option("rescuedDataColumn", "_rescued_data")
- Rescued Data Field





- ~~API Load verbessern (mit Notebook von Steffen anschauen)~~
- ~~Auto Loader auf File Hierarchy~~
- ~~max Files auf 5 Stellen~~
- ~~Health Check für SCD2 ausbauen~~
- ~~Data Cleaning Step 2 in Silber)~~
- ~~Qualys (Gemeinsam)~~
	- ~~Type schon in Bronze auf "Confirmed" filtern~~
	- ~~Port~~
	- ~~Last / First~~
	- ~~Result~~
- ~~RAHCS~~
- Metadatensteuerung
- ~~Pipeline Architektur (eine Pipeline für alle Bronze Tabellen?) -> Julian~~
- ~~Kanban Board aufmachen~~
- ~~utils.py vereinheitlichen (eine Funktion, der je nach Quellsystem Variablen übergeben werden)~~
	- ~~Snapshots aus der Bronze Tabelle lesen, nicht aus den Dateinamen~~
- ~~Filesystem vereinheitlichen:~~ 
	- ~~Auf konkreten Pfad einigen~~ 
	- ~~Dateinamen vereinheitlichen~~
- ~~API-Downloads als Task einfügen~~
- ~~Dateien im Workspace ordnen~~
- ~~SChema hints einfügen~~
- ~~Hash für finding_key~~
- ~~Expect or drop (aus Bronze gelöscht?)~~
- ~~Qualys duplicate keys in Quarantäne Tabelle?~~
- ~~Überlegen, ob Bronze-Pipelines getrennt werden sollten~~
- ~~Arbeitstermin (Historisierung Vorbereiten)~~
- ~~Serverless evaluieren~~



