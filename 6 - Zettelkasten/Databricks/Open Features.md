
- API Load verbessern
- Snapshots aus Bronze selber holen
- Expectations einfügen (auch schon in bronze)
- schemaEvolutionMode in Bronze und Silber einfügen
	- `# Allow Auto Loader to add newly appearing fields .option( "cloudFiles.schemaEvolutionMode", "addNewColumns" )`
	- addNewColumnsWithTypeWidening
	- .option("rescuedDataColumn", "_rescued_data")
- Rescued Data Field





- API Load verbessern (mit Notebook von Steffen anschauen)
- Auto Loader auf File Hierarchy
- max Files auf 5 Stellen
- Health Check für SCD2 ausbauen
- Data Cleaning Step 2 in Silber)
- Qualys (Gemeinsam)
	- Type schon in Bronze auf "Confirmed" filtern
	- Port
	- Last / First
	- REsult
- RAHCS
- Metadatensteuerung
- Pipeline Architektur (eine Pipeline für alle Bronze Tabellen?) -> Julian
- Kanban Board aufmachen