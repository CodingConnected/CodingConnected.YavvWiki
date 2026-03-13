---
title: "Queries met VLOG data"
date: 2020-08-06
---

## Algemeen

Met YAVC (en binnenkort ook met YAVV met een addon) is het mogelijk middels eigen queries VLOG data te doorzoeken naar optreden van bepaalde events of situaties. Dit in een notendop als volgt:

- De gebruiker kan in de UI (user interface) in een boomstructuur een set voorwaarden opbouwen. Bijvoorbeeld: het waar zijn van een bepaalde ingang, rood zijn van een bepaalde signaalgroep of het opkomen van een detector.
- Wanneer er een pad in de structuur als geheel waar wordt bij het doorlopen van de data, levert dit een resultaat op.

## Achtergrond

VLOG data bestaat uit een serie opeenvolgende berichten waarin de status van items wordt doorgegeven. VLOG logging kent een cyclus, waarbij elke 5 minuten de complete status van alle elementen wordt weggeschreven. Gedurende de genoemde 5 minuten worden uitsluitend status wijzigingen doorgegeven.

Vanuit het perspectief van queries en analyse is uitsluitend de actuele status van belang; steeds bij een _wijziging_ in status van een element moeten we kijken of aan de gestelde voorwaarden wordt voldaan. Een VLOG bericht met dezelfde status als voorheen is daarbij dus irrelevant. Het feit dat er enkel wijzigingen worden bekeken heeft als consequentie dat we in de VLOG datastroom niet kunnen zoeken naar "het moment dat item X exact Y seconden in status Z staat". Immers, pas wanneer ergens iets wijzigt, kunnen we een nieuwe tijd bepalen en duur van statussen meten.

Queries binnen YAVC doorlopen daarom alle voor de query relevante berichten, en bepalen bij elke wijziging opnieuw de status van elementen, en het waar/onwaar zijn van de voorwaarden. Belangrijk is:

- Een resultaat kan altijd maar op één moment worden weggeschreven
- Bij opstellen van een set voorwaarden moeten we er dus altijd voor zorgen dat op een bepaald moment die set voorwaarden eenmalig waar (begint te) zijn

## Opzet: boomstructuur

Het opbouwen van de voorwaarden van een VLOG-query in YAVC gebeurt middels toevoegen en ordenen van items in een boomstructuur. Tijdens de analyse doorloopt YAVC die structuur en zoekt naar een pad door de boomstructuur dat van begin tot eind waar oplevert.

In de boomstrcutuur zijn er twee type voorwaarden:

- Collectie: dit is een verzameling voorwaarden, die op een bepaalde manier met elkaar samenhangen.
    - Een collectie geeft "waar" af wanneer de collectie als geheel waar is.
    - Er zijn diverse typen collecties beschikbaar, die elk op een andere wijze omgaan met de onderliggende condities
- Conditie: dit is een enkele voorwaarde die waar of niet waar oplevert als resultaat.
    - Een conditie heeft nooit onderliggende items.
    - Een conditie heeft een type (signaalgroep, detector, input of output)
    - Een conditie is gerelateerd aan een item van het ingestelde type. Het is ook mogelijk de analyse uit te voeren voor alle items van het betreffende type. Dit wordt verderop nader toegelicht.
    - Voor het betreffende type wordt gezocht naar waar zijn van bepaalde ingesteld voorwaarden, bijvoorbeeld het startmoment dat ingang X waar wordt. De werking en instellingen van condities worden verderop nader toegelicht.

### Collecties

De volgende typen collecties zijn beschikbaar:

- En - alle onderliggende voorwaarden moeten waar worden
- Of - één van de onderliggende voorwaarden moet waar worden
- (Abolute) minimale tijd - de (absolute) tijd tussen de twee onderliggende voorwaarden moet minimaal X zijn
- (Absolute) maximale tijd - de (absolute) tijd tussen de twee onderliggende voorwaarden mag maximaal X zijn
- Tijd meting - meting uitvoeren van de tijdsduur tussen het waar zijn van twee onderliggende voorwaarden
- Zoeken in bereik - _nog niet operationeel_; hiermee wordt het later mogelijk tussen twee events te zoeken naar het waar worden van een onderliggende set voorwaarden

Voor collecties waarbij wordt gekeken naar een tijd moet een drempelwaarde worden ingesteld (met uitzondering van de meting).

### Condities

De volgende typen collecties zijn beschikbaar:

- Signaalgroepen
- Detectoren
- Ingangen
- Uitgangen
- DSI (gerelateerd aan signaalgroepen)

Na keuze voor een bepaalde type conditie kan een item van het betreffende type worden geselecteerd waarnaar voor deze conditie gekeken zal worden. Het is ook mogelijk een conditie uit te voeren voor alle items van het betreffende type. Zie verderop _**\[TODO\]**_.

Afhankelijk van het type conditie is het zoek type instelbaar, ofwel waarnaar tijdens de analyse zal worden gezocht:

- Signaalgroepen: groen, geel of rood
- Detectoren: bezet, onbezet of een eigen waarde (tbv. zoeken naar storingen)
- Ingangen en uitgangen: hoog, laag of multivalent
- DSI: onbekend, inmelding, uitmelding of voorinmelding

Voor een aantal zoek typen is een referentie waarde nodig waarmee de actuele status van het item tijdens de analyse vergeleken zal worden. Tevens moet de wijze waarop de vergelijking plaats zal vinden worden ingesteld:

- Dit geldt voor multivalente IO en voor 'detectie met een eigen waarde'
- Er moet een waarde worden opgegeven zodat daarmee vergeleken kan worden
- Het type vergelijking moet worden ingesteld: gelijk aan, groter dan, kleiner dan, etc.

Tenslotte moet het type conditie worden ingesteld. Dit bepaalt wanneer de conditie als geheel "waar" oplevert, en dus voor een resultaat kan zorgen (al dan niet in samenhang met gerelateerde condities in een collectie). De volgende typen condities zijn beschikbaar:

- Waar - levert "waar" op wanneer aan de gestelde voorwaarden wordt voldaan
- Onwaar - levert "waar" op wanneer niet aan de gestelde voorwaarden wordt voldaan
- Start - levert éénmalig "waar" op de eerste keer dat aan de gestelde voorwaarden wordt voldaan, en dan pas weer nadat de conditie eerst onwaar is geweest
- Eind - levert éénmalig "waar" op de eerste keer dat niet aan de gestelde voorwaarden wordt voldaan, en dan pas weer nadat de conditie eerst waar is geweest
- Waar/onwaar minimale/maximale tijd - levert "waar" op indien de voorwaarden minimaal/maximaal X tijd waar/onwaar zijn
- Start/einde waar/onwaar minimale/maximale tijd - levert éénmalig "waar" de eerste keer dat de voorwaarden minimaal/maximaal X tijd (niet) waar/onwaar zijn, en dan pas weer nadat de conditie eerst onwaar is geweest

Voor typen condities waar een tijd van toepassing is moet hiervoor de drempelwaarde worden ingesteld.

_Merk op:_ de combinatie van type conditie met type vergelijking behoeft extra aandacht. Zo kan het type conditie op "Waar" ingesteld staan, maar indien voor bv. een multivalente ingang het type vergelijking op "Niet gelijk aan" is ingesteld, wordt de conditie als geheel dan dus "waar" wanneer de ingang _niet_ de ingestelde waarde heeft.

## Bepalen resultaten

Wanneer een set voorwaarden "waar" oplevert en dus een resultaat zal worden weggeschreven, moet worden bepaald welk index, tijd en waarde voor het resultaat zullen worden gebruikt. Daarom is het per conditie/collectie mogelijk aan te geven dat de index/tijd/waarde van het item voor het resultaat gebruikt moet worden.

Hierbij geldt:

- Het is dus mogelijk op meerdere plaatsen in de boomstructuur "gebruik waarde" aan te geven, zodat verschillende vertakkingen elk een eigen waarde terug kunnen geven.
- Het item het dichts bij de "stam" waarvoor dit is ingesteld, overschrijft evt. eerder bepaalde resultaat data, dieper in de boomstructuur.
- In het geval twee vertakkingen van de boomstructuur exact tegelijk "waar" teruggeven, zal het resultaat van de onderste vertakking dat van die daarboven overschrijven; het beste is natuurlijk deze situatie te voorkomen
- Voor "waarde" geldt dat deze alleen bepaald kan worden voor multivalente IO en voor items waar iets met tijd wordt gedaan.
- Voor "En" en "Of" collecties wordt indien is ingsteld dat hiervan de waarde moet worden genomen tbv. het resultaat, de waarde van het eerste geneste item dat "waar" teruggeeft genomen

## Weergave van resultaten

De visualisatie van uitkomsten van een query werkt in principe precies zoals de visualisatie van analysis binnen YAVC. Van belang hierbij is met name de wijze waarop de uitkomsten tbv. tabellen en grafieken worden geagregeerd ("resampling"). Dit is instelbaar, naast een aantal andere aspecten van de visualisatie:

- Analyse beschrijving - verschijnt boven grafieken, en in de export
- Y-as beschrijving - verschijnt in grafieken bij de Y-as
- Resample type - de wijze waarop analyse uitkomsten worden geagregeerd:
    - Tellen - tellen van resultaten per tijdseenheid; de waarde van resultaten wordt buiten beschouwing gelaten. Bv. bij roodrijders is dit de juiste wijze.
    - Gemiddelde - per tijdseenheid wordt het gemiddelde van de gevonden metingen genomen voor de weergave. Bv. voor wachttijden is dit de juiste keuze.
    - Som - per tijdseenheid wordt het totaal van alle metingen genomen voor de weergave. Hiermee kan bv de totale groenduur per uur worden bepaald.
    - Herberekend gemiddelde - dit is voor queries niet relevant, maar wordt binnen YAVC gebruikt om voor analysis die zelf een gemiddelde zijn (groenbenutting, capaciteit) gebruikt om voor een groter tijdvak de uitkomst opnieuw te bepalen op basis van achterliggende waarden.
- Nul is valide uitkomst - dit geeft aan op "0" als waarde in de grafieken terug moet komen of niet
- Boxplot mogelijk - een boxplot is enkel relevant wanneer de uitkomsten een spreiding hebben
