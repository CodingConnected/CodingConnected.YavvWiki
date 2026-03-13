---
title: "Analyse: snelheidsprofiel"
date: 2020-09-09
---

Wanneer bekend is waar lussen ten opzicht van elkaar liggen, is het mogelijk een inschatting te maken van de gereden snelheid.

_Let op!_ Een opmerking vooraf: er gelden een aantal beperkingen en overwegingen bij het meten van snelheid op basis van VLOG data:

- De meting betreft **_altijd_ een inschatting**
- Of een meting correct is hangt in hoge mate af van de juistheid van de instellingen: wijkt de ligging op straat af van die zoals die is geconfigureerd, dan kan er sprake zijn van grote afwijkingen tussen de berekende snelheid en de werkelijk gereden snelheid
- Zelfs bij een correcte configuratie is er sprake van een inschatting: de resolutie van VLOG is een tiende seconde; een meting 'start detectie' op 00:00:00.5 kan dus feitelijk gebeurd zijn om 00:00:00.4001.

Functionele werking van de meting:

- Enkel kop, lange en verweg lussen worden meegenomen in de meting
- Er wordt uitsluitend gemeten wanneer een melding op lus 1 met grote zekerheid gekoppeld kan worden met lus 2 op een rijstrook.
- Gegeven dat:
    - Lus 1 is de eerste lus waar een voertuig richting de stopstreep langs rijdt
    - Lus 2 is de lus het dichtst bij de stopstreep (tenzij is ingesteld dat de 2 meest verweg gelegen lussen moeten worden gebruikt)
    - Gemeten wordt de tijd van start detectie op lus 1 tot start detectie op lus 2
- De snelheid wordt bepaald door te kijken naar de afstand start lus 1 (afstand tot stopstreep + lengte) tot start lus 2. Doot de afstand te delen op de tijd krijgen we de meetwaarde.
    - **Let op!** Er worden geen marges toegepast; de werkelijke waarde kan dus altijd hoger of lager liggen dan de berekende waarde.
- Indien er meerdere detectoren op de rijbaan liggen, wordt bijgehouden of deze in de juiste volgorde worden aangereden; raakt het patroon verstoord, dan wordt de meting afgebroken

Beschikbare instellingen (defaults in blokhaken):

- Maximale snelheid meting \[250\]: dit kan worden gebruikt om te voorkomen dat extreme meetwaarden het beeld vervuilen. De huidige implementatie van het algoritme voorkomt extreme waarden al bijna altijd.
- Minimale tijd geen D \[5.0 sec.\]: indien minder dan deze tijd geleden er actie is gemeten op een detector op een rijbaan, kan geen nieuwe meting starten
- Maximale tijd tussen SD \[8.0 sec.\]: indien SD momenten van opeenvolgende lussen meer dan deze tijd uit elkaar liggen, wordt een meting afgebroken
- Meten op eerste 2 detectoren \[uit\]: gebruik de twee meest verweg gelegen detectoren in plaats van de eerste en laatste voor de meting
- Inperken duur meting \[uit\]: hiermee kan worden aangegeven dat alleen gedurende een bepaalde periode gemeten kan worden, zie volgende twee instellingen
- Percentage groentijd \[25%\]: indien ingeschakeld, wordt pas gemeten nadat dit percentage groentijd voorbij is
- Seconden in rood \[3 sec.\]: indien ingeschakeld, wordt slechts gemeten wanneer het maximaal zo lang rood is
