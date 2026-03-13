---
title: "YAVV / YAVC-client fout na update"
date: 2021-03-24
---

Bij gebruik van YAVV of YAVC-client via de setup verloopt een update in principe automatisch. Bij uitvoeren van de setup wordt de oude applicatie verwijderd, en de nieuwe applicatie nadien geïnstalleerd. Het kan echter voor komen dat data van de oude versie blijft hangen. Er ontstaat dan een mismatch tussen functie-bibliotheken uit de oude applicatie en wat de nieuwe applicatie verwacht. Dit levert fouten op zoals:

- Meestal: MissingMethodException
- Soms: FileNotFoundException of NullReferenceException of TypeLoadException

Om dit te verhelpen:

- Deïnstalleer de geïnstalleerde versie handmatig via Control Panel > Programma verwijderen
- Ga naar de map C:\\Program Files (x86)\\YAVV (of de map waar YAVV was geïnstalleerd) en controlleer of deze leeg is; verwijderen eventuele achtergebleven data
    - Merk op: instellingen gaan **niet** verloren!
- Installeer de applicatie opnieuw
