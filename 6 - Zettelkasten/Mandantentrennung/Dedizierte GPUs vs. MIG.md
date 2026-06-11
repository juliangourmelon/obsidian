Tags: [[GPU]]; [[AI_SECURITY]]
Links: [[Dedizierte GPUs vs. MIG]]; [[Mandantentrennung]]; [[6 - Zettelkasten/Mandantentrennung/NVIDIA Confidential Computing|NVIDIA Confidential Computing]]; [[Open Shift Confidential Containers]]

Konkrete Gefahren, die bei bei MIG auftreten, allerdings nicht bei dedizierten GPUs:
- GPU-interne Side Channels
- Scheduler-Effekte
- GPU-interne Timing-Effekte
- MIG-Konfigurationsfehler


Der reale Sicherheitsunterschied ist nicht riesig, Vorteile liegen vor allem in der leichteren Begründbarkeit vor Auditoren: Es klingt erstmal plausibler, dass die Hardware getrennt vorliegt.