---
title: "Analyse: controle werking wachttijdvoorspellers"
date: 2023-10-09
---

Middels YAVV is het mogelijk geautomatiseerd de juiste werking van wachttijdvoorspellers te controleren. Onder 'juiste werking' wordt in deze context verstaan:

- Het aantal LEDs dat wordt aangestuurd neemt altijd af
    - Een toename van één LED wordt gezien als acceptabel, omdat de laatste LED vaak gaat knipperen tijdens een OV of HD ingreep

- De duur tussen het doven van LEDs neemt nooit meer toe dan een bepaalde marge; een voorspeller die vertraagd gedurende het aflopen is voor weggebruikers verwarrend en geeft een onbetrouwbaar beeld

Door te kijken naar de aansturing van de wachttijdvoorspellers middels uitgangen (serieel via 5 uitgangen of via één multivalente uitgang) voert YAVV een controle uit of aan bovenstaande voorwaarden wordt voldaan. Is dat niet zo, dan wordt een analyse resultaat aangemaakt. Het is op deze wijze dus eenvoudig mogelijk is de fasenlog die momenten te vinden, waar er sprake is van een vertragend of foutief voorspel patroon.

Om de analyse te kunnen gebruiken moet worden voldaan aan een aantal voorwaarden:

- De voorspeller wordt aangestuurd via één multivalente uitgang, OF

- De voorspeller wordt serieel aangestuurd middels 5 uitgangen die in de VLOG opeenvolgend zijn; de volgorde (oplopend of aflopen, is instelbaar). Bijvoorbeeld: voor signaalgroep 26 zijn er 5 uitgangen, namelijk uitgang wtv26\_0 met index 56, wtv26\_1 met index 57, etc. Of juist bv uitgang wtv26\_4 met index 56, wtv26\_3 met index 57, etc.; dan is de rangering dus omgekeerd.

- Uitgangspunt tijdens ingrepen in het regelproces waarbij de voorspelling wordt gehalteerd, is dat de laatste LED gaat knipperen; is dit niet zo, dan worden in dit geval mogelijk onterechte analyse resultaten aangemaakt

Voor deze analyse zijn de volgende instellingen beschikbaar (defaults in \[blokhaken\]):

- Een lijst met signaalgroepen die geanalyseerd moeten worden \[default: leeg\]. Per signaalgroep is instelbaar:
    - De signaalgroep (kiezen uit een lijst)
    
    - De uitgang (kiezen uit een lijst); hier wordt de multivalente uitgang ingesteld, of in geval van seriële aansturing, de uitgang met de laagste index (bv: wtv26\_0 of wtv26\_4)
    
    - Multivalent of niet?
    
    - Omgekeerde volgorde of niet? Indien de uitgang met het meest significante bit (doorgaans de uitgang met een naam eindigend op "\_4" als eerste in de lijst met items staat (dus laagste index nummer), is sprake van omgekeerde volgorde.

- Drempelwaarde % wachttijd stijging \[25%\]: minimale relatieve hoeveelheid dat de wachttijd tussen opeenvolgende LEDs moet stijgen, om een resultaat aan te maken; bijvoorbeeld eerst duurt het 2 seconden, en dan 3 seconden, dan is er 50% stijging

- Drempelwaarde wachttijd stijging absoluut \[0.2 sec.\]: minimale absolute hoeveelheid dat er sprake moet zijn van een stijging in de wachttijd tussen opeenvolgende LEDs, om een resultaat aan te maken
    - De absolute en relatieve stijgings drempelwaarden gelden beide: aan _beide_ moet zijn voldaan voor een analyse resultaat wordt aangemaakt.

- Drempelwaarde reset meting \[8 sec.\]: indien er langer dan deze instelling niets in gebeurd, wordt de meting gereset

In de praktijk is er vaak sprake van 50% stijging of meer, omdat de resolutie van VLOG 0.1 seconde is: dan komt vaak voor dat het eerst 0.1 seconde, en dan 0.2 sec.; om dit te ondervangen wordt dus óók gekeken naar absolute stijging.

Bij deze analyse is het meest nuttige overzicht bij de visualisatie van analyse data de "lijst met alle metingen". Door gebruik te maken van [de multivenster omgeving van YAVV](https://www.codingconnected.eu/yavvwiki/algemeen/werkbladen-en-gebruikersinterface-van-yavv/) en het analyse tabblad naast/boven/onder de fasenlog te plaatsen, en vervolgens dubbel te klikken op items in de lijst (of enter toets), kan snel worden gekeken wat er aan de hand is.
