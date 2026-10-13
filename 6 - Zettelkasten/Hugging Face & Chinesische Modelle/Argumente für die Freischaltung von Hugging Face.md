
- Keine Angriffe auf User bekannt.
- Hugging Face hat Konsequenzen aus dem Angriff gezogen und Maßnahmen eingeleitet ähnliche Angriffe in Zukunft abzuwehren.
- Das für uns gefährlichste Szenario (Angreifen tauscht Safetensors und zugehörige Signatur aus) wurde nicht von HF bestätigt.
- Wir würden fixierte Versionen ziehen und diese mehrere Tage bis Wochen in Quarantäne halten. Sollte sich herausstellen, dass der extrem unwahrscheinliche Fall eingetreten ist, dass sowohl Safetensors und Signatur ausgetauscht wurden, würden wir das bis dahin mitbekommen haben.
- Wir haben sowieso extrem hohe Sicherheitsvorkehrungen beim Download von Hugging Face (nur Safetensors, fixierte Versionen, Download über Proxy)