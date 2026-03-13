---
title: "Analyse: voertuigverliesuren"
date: 2021-04-28
---

Bij voertuigverliesuren (VVU) gaat het om het totaal aan verloren tijd als gevolg van wachten voor een verkeerslicht voor een bepaalde richting of kruising gedurende een bepaalde periode. Elk afzonderlijk voertuig heeft een bepaalde verliestijd, bijvoorbeeld 10 of 20 seconden. De totale verliestijd voor een bepaald tijdvak omgerekend naar uren geeft de hoeveelheid "voertuigverliesuren".

Op basis van detectie data zoals deze in de VLOG data zit kan de exacte verliestijd nooit worden bepaald. Immers, het exacte aankomst proces is onbekend. Er zal dus een versimpelde inschatting moeten worden gemaakt. YAVV/YAVC doet dit als volgt:

- Verzamelen data:
    - Bepalen wachttijd eerstwachtende
    - Bepalen tijdsduur afrijden wachtrij: dit is de tijd na startgroen tot er een voldoende groot hiaat valt
    - Tellen aantal voertuigen in de wachtrij: voertuigen worden geteld vanaf startgroen tot er een voldoende groot hiaat valt
    - Voertuigen die afrijden nadat de wachtrij is afgereden hebben een veronderstelde verliestijd van 0 seconden.
- Gegeven de verzamelde data:
    - Het aantal voertuigen in de wachtrij is `[N]`
    - Delen van de wachttijd eerstwachtende op het aantal voertuigen uit de wachtrij: dit is `[A]`
    - Delen van de tijdsduur afrijden wachtrij op het aantal voertuigen uit de wachtrij: dit is `[B]`
    - Met deze drie grootheden wordt de verliestijd per voertuig bepaald:
        - Voertuig n heeft een verliestijd van `[A] * ([N] - n) + [B] * n`
        - Uitleg:
            - er wordt van uitgegaan dat een voertuig met plaats n in de wachtrij een recht onevenredig aandeel van de wachttijd eerstwachtende heeft gewacht.
            - er wordt van uitgegaan dat een voertuig met plaats n in de wachtrij een recht evenredig aandeel van de totale tijdsduur afrijden wachtrij heeft gewacht.
            - de som van deze twee waarden levert de complete verliestijd per voertuig
    - De totale verliestijd gedeeld door 3600 levert de VVU waarde.
- De totale verliestijd van alle voertuigen uit de wachtrij die zijn afgereden levert een waarde per realisatie. Momenteel wordt die waarde weggeschreven op start rood. Bij opdelen van de metingen in intervallen wordt de complete verliestijd waarde op basis van dit tijdstip aan een interval toegedeeld.
- Overstaan wordt bepaald door te kijken naar het vallen van een voldoende groot hiaat op de korte of lange lus; gebeurt dit niet, dan wordt de totale verliestijd van de cyclus meegenomen naar de volgende cyclus. Er wordt afgevlakt, en vervolgens krijgt elk voertuig uit de volgende cyclus de afgevlakte verliestijd erbij. Bij meerdere opeenvolgende realisaties met continu overstaan cummuleert zo de berekende verliestijd (met afvlakking).
    - Merk nog op: deze aanpak kent beperkingen, zie ook hieronder.

## Beperkingen

Zoals hierboven reeds benoemd: het gaat bij VVU's op basis van detectie data _altijd_ op een inschatting. Het algoritme is een extreme versimpeling van de werklijkheid. Deels zal er sprake zijn van onderschatting, deels van overschatting. Middels microsimulaties (met [SUMO](https://www.eclipse.org/sumo/)) is bekeken hoe accuraat het algoritme functioneert. Over het algemeen komt het algoritme redelijk in de buurt van de werkelijke (=in de simulatie gemeten) verliestijden. Bij een normale vormgeving en normale omstandigheden is de afwijking doorgaans niet groter dan 5-10 %.

In de praktijk is er soms sprake van bijzonderheden, waar het algoritme geen rekening mee kan houden. Dit gaat bijvoorbeeld om:

- Korte opstelvakken: wanneer verkeer het opstelvak, en dus de detectie, van een richting niet kan bereiken, bijvoorbeeld vanwege een wachtrij bij een aangrenzende richting, zal sprake zijn van een onderschatting van de werkelijke verliestijden.
- Overstaan: de analyse houdt rekening met overstaan, maar bij structureel overstaan zal de huidige implementatie komen tot een overschatting van de werkelijke verliestijden; de reden is dat in de praktijk er een maximale wachtrij zal ontstaan, terwijl het algoritme bij opeenvolgend overstaan de wachttijden continu (afgevlakt) cummuleert.

Desalniettemin: wordt rekening gehouden met de genoemde beperkingen, dan biedt de analyse een goede basis om te komen een beoordeling van een kruispunt, en/of een vergelijking te maken tussen een oude en nieuwe situatie.

## Instellingen

De volgende instellingen zijn beschikbaar voor deze analyse (default in \[blokhaken\]):

- Minimaal hiaat \[1,2 sec.\]: het minimale hiaat op de koplus (tussen voertuigen) om de wachtrijmeting (tijdens groen, gedurende het afrijden) af te ronden
- Minimaal hiaat korte/lange lus \[3.0 sec. / 0.5 sec.\]: indien minimaal dit hiaat valt op de korte/lange lus, wordt geconcludeert dat er géén sprake is van overstaan de betreffende realisatie
- Afvlak factor overstaan \[0.75\]: de mate waarin de gecummuleerde verliestijd wordt afgevlakt gedurende overstaan
- Check overstaan \[waar\]: wel/niet kijken naar overstaan
- Check status regelen \[waar\]: indien dit uit staat, loopt de meting door ongeacht de regelstatus \[WPS\]
