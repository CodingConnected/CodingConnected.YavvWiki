---
title: "Analyse: intensiteit fietsers"
date: 2020-09-04
---

Intensiteit wordt in YAVV/YAVC bepaald middels tellen op de koplus: [zie hier](https://www.codingconnected.eu/yavvwiki/analyse/analyse-intensiteit/). Voor fietsers geeft deze manier van meten niet altijd het juiste of beste beeld: fietsers kunnen zich als groep opstellen bij de stopstreep, waardoor mogelijk meerdere fietsers als één fietser worden geteld.

De intensiteitsmeting speciaal voor fietsers biedt de mogelijkheid meer inzicht te krijgen in de werkelijke intensiteit op fietsrichtingen. De analyse kijkt hiertoe naar het op een richting aanwezige detectieveld, en maakt gebruik van de lussen die het beste beeld geven. Dit werkt als volgt:

- Alleen lussen ingesteld als "koplus" of "verweg lus" worden meegenomen in de analyse.
- Indien er een enkele koplus aanwezig is: tellen op die koplus. De uitkomst zal identiek zijn aan de reguliere intensiteitsmeting.
- Bij aanwezigheid van twee opeenvolgende koplussen, en geen verweg lussen, wordt geteld op basis van de koplus het verste van de stopstreep. Er wordt in dit geval _niet_ richtinggevoelig gemeten, omdat de kans te groot is dat fietsers niet (tijdig) beide lussen aanrijden.
- Indien er een enkele verweg lus aanwezig is: tellen op basis van die verweg lus. De lus of lussen paar bij de stopstreep worden niet bekeken.
- Bij aanwezigheid van twee opeenvolgende verweg lussen: richtinggevoelig meten. Ook dan worden evt. lussen bij de stopstreep niet meegenomen in de analyse. Indien de lussen te ver uit elkaar liggen (zie uitleg bij instellingen hieronder) wordt geteld op basis van de lus het dichtst bij de stopstreep.

De volgende instellingen zijn beschikbaar voor richtinggevoelige metingen (defaults in blokhaken):

- Maximale rijtijd richtinggevoelig \[5\]: de maximale tijdsduur tussen start detectie op de meest verweg gelegen lus, tot start detectie van de navolgende lus, om een fietser te tellen.
- Maximale afstand richtinggevoelig \[2\]: de maximale afstand _tussen het begin_ van twee lussen, om deze lussen als paar te zien.

_Merk op_: de analyse houdt geen rekening met eventuele afslaande fietsers. Dit zou een overschatting kunnen geven wanneer wordt geteld op basis van verweg detectie, en het aandeel afslaande fietsers relatief hoog is. Anderszijds geldt: tellingen op de koplus geven juist weer een mogelijke onderschatting, omdat naast elkaar opgestelde fietsers, of fietsers die als één groep vertrekken, dan slechts éénmaal worden geteld.
