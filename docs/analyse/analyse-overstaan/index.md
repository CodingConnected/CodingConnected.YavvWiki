---
title: "Analyse: overstaan"
date: 2020-09-14
---

Met overstaan wordt bedoeld: de tijdens rood opgebouwde wachtrij bij een signaalgroep kan tijdens groen niet geheel afrijden, waardoor een deel van de voertuigen meer dan één cyclus moeten wachten.

Alternatieve realisaties worden bij het bepalen van overstaan in de regel buiten beschouwing gelaten. Omdat in YAVV/YAVC voor overstaan uitsluitend wordt gekeken naar de externe signaalgroep status, wordt er gewerkt met grenswaarden om alternatieve realsaties te kunnen filteren.

Om te bepalen of op een richting sprake is van overstaan, wordt gekeken naar de bezetting van de koplus. Indien in de periode start groen tot het volgende startgroen moment op de koplus géén gat valt groter dan X, én de betreffende realisatie betreft minimaal Y tijd groen, wordt overstaan geregistreerd.

In geval van **meerdere rijstroken**, wordt default alleen dan overstaan gemeten wanneer aan de voorwaarden wordt voldaan op alle stroken. Instelbaar kan worden bepaald dat ook bij overstaan op afzonderlijke rijstroken reeds een analyse resultaat overstaan wordt geregistreerd. Uiteraard zal dit leiden tot een groter aantal analyse resultaten.

Hierbij gelden de volgende instellingen (defaults in blokhaken):

- Maximale volg tijd \[5.0\]: indien er een gat valt op de koplus groter dan deze waarde, wordt een lopende meting afgebroken
- Minimale groentijd \[10.0\]: indien de groentijd kleiner was dan deze waarde, wordt een eventueel lopende meting afgebroken op einde groen (waardoor bij het volgende stargroen moment niets gemeten zal worden)
- Meten per rijstrook \[onwaar\]: indien waar, wordt óók overstaan gemeten indien er slechts sprake is van overstaan op een enkele rijstrook. Staat deze optie uit (dat is de default) dan wordt enkel dan overstaan gemeten wanneer op alle rijstroken overstaan is gezien.
