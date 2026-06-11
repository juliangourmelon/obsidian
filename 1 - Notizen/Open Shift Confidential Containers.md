
Tags: [[GPU]]; [[GPU Mandantentrennung]]
Links: [[Mandantentrennung]]; [[6 - Zettelkasten/Mandantentrennung/NVIDIA Confidential Computing|NVIDIA Confidential Computing]]

- Kata Containers + Verschlüsselte Verarbeitung 
- Linux Kernel sind bereits durch VMs getrennt
- CoCo bringt Confidential Computing dazu
- Verhindert, dass Cluster Admin / Jemand mit Root Rechten auf die zugrunde liegenden Daten zugreifen darf
- Eine Confidential VM (CVM) ist eine VM mit zusätzlichem Hardware-Schutz.

Je nach CPU:
- AMD SEV-SNP
- Intel TDX


- Kann aktuell theoretisch zusammen mit NVIDIA Confidential Computing verwendet werden, ist allerdings noch im Tech-Preview

CoCo schützt gegen:
- Host Root (selbst Root auf dem Container sieht die Daten nicht)
- Hypervisor
- Cluster-Admin


Schutz reicht für KI allerdings nicht aus: sobald die Daten auf die GPU kopiert werden, endet der Schutz. -> Darum ist es prinzipiell eine gute Idee mit NCC zu kombinieren.


Ist primär Schutz vor dem Host / Hypervisor, nicht so super wichtig für Mandantentrennung. (Anmerkung Julian: Laterales Movement könnte verhindert werden, wenn Host kompromittiert) 