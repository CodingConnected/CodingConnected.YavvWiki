---
title: "Analyse: stopkans"
date: 2023-02-17
---

Bij stopkans gaat het om de kans die een passerend voertuig heeft voor een verkeerslicht tot stilstand te moeten komen. Deze kans wordt bepaald door enerzijds de kans om op de koplus tot stilstand te komen, en anderzijds de kans om aan te komen tijdens rood:

- De kans om tot stilstand te komen wordt bepaald door te kijken of de koplus van een richting gedurende een realisatie langer dan X sec. bezet is geweest; is dit zo, dan is er gestopt, en anders niet; gemeten over meerdere realisaties geeft dit een fractie, dit is de kans per realisatie dat er sprake is van stilstand
- Is er gestopt gedurende een realisatie, dan is voor een willekeurig voertuig dat gedurende die realisatie is afgereden nog de vraag hoe groot de kans was dat het daadwerkelijk moest stoppen; hiertoe wordt gekeken naar de fractie roodtijd

Door deze twee kansen te vermenigvuldigen wordt de stopkans ingeschat. De formule is dus:

\[latexpage\] \\\[P\_{stop} = {T\_{tdb} \\ge T\_{tdbmin} \\over C\_{reals}} \\cdot {T\_{groen} \\over T\_{geel} + T\_{rood} + T\_{rood}}\\\]

Het gaat hier uitdrukkelijk om een schatting, omdat de stopkans op basis VLOG data niet exact kan worden bepaald (zoals geldt voor alle analyse grootheden).

Binnen YAVV/YAVC is het ook mogelijk een schatting van het aantal stops weer te geven. Hiertoe vermenigvuldigt de applicatie de berekende stopkans voor een bepaald tijdsinterval met de intensiteit voor dat interval. Dit geeft een grove indicatie van het aantal stop; voor een normale situatie zal dit gemiddeld redelijk in de buurt komen van de situatie op straat.

Instellingen (defaults in blokhaken):

- Minimale tijd koplus bezet \[3.6\]: minimale tijd in seconden dat de koplus bezet moet zijn geweest om gedurende een realisatie een gestopt voertuig te meten
- Controleer status regelen \[waar\]: wel/niet kijken of WPS op regelen staat om metingen uit te voeren
