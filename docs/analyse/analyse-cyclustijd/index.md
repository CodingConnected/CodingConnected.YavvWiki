---
title: "Analyse: cyclustijd"
date: 2020-08-27
---

## Achtergrond

De cyclustijd wordt binnen YAVV/YAVC bepaald op basis van detectie data en externe signaalgroep status. Er wordt bewust niet gewerkt met interne signaalgroep status en/of module informatie. Die keuze is met name ingegeven door het feit met de komst van netwerk regelingen, er steeds meer VLOG data komt zonder interne statussen en informatie omtrent modules (die vaak zelfs niet bestaan).

De cyclustijd wordt bepaald voor de regeling als geheel. Momenteel is er geen cyclustijd beschikbaar voor afzonderlijke richtingen.

De keuze voor analyse op basis van uitsluitend "externe" data heeft natuurlijk consequenties. Eén consequentie is dat geen rekening gehouden kan worden met bijvoorbeeld alternatieve realisaties, of de indicatie omtrent de stand van de cyclus volgens de regeling zelf - die echter sowieso van beperkte waarde is, gezien de "wachtmodule" die in rustigere perioden actief blijft. Een voordeel is dat de cyclustijden tussen regelingen onderling vergeleken kunnen worden ongeacht het type regeling.

### Definitie

Voor YAVV/YAVC is voor cyclustijd de volgende definitie gehanteerd:

> De tijd vanaf het moment waarop er activiteit op de kruising wordt gemeten, tot de tijd dat ofwel er geen activiteit op de kruising wordt gemeten, ofwel alle richtingen waar activiteit is gezien aan de beurt zijn geweest.

YAVV zoekt dus in de data naar 'rustmomenten' en/of momenten waarop alle richtingen die moesten komen aan beurt zijn geweest, waarna de meting herstart.

## Instellingen

Voor de cyclustijd gelden de volgende instellingen (defaults in blokhaken):

- Controleer status regelen - al dan niet controleren of de regelaar in de stand 'regelen' staat (WPS) \[uit\]
- Meten drukknop activiteit - al dan niet kijken naar meldingen op drukknoppen om te bepalen of er activiteit is op een richting \[aan\]
- Minimale tijd zonder activiteit - indien op een richting gedurende deze periode geen activiteit wordt gemeten wordt een evt. lopende cyclustijd meting afgerond \[3.0 sec.\]
- Minimale cyclustijd - metingen lager dan deze waarde worden genegeerd. Hiermee kunnen metingen waarbij slechts één richting kort groen is geweest worden genegeerd \[5.0 sec.\]
- Multi module molens - hiermee wordt aangegeven dat de regeling beschikt over meerdere, parallelle module molens. Default worden richtingen opgedeeld naar 100-tallen: 1xx in molen 1, 2xx in molen 2 en 3xx in molen 3. De toedeling is ook instelbaar, zie navolgende punten \[uit\]
- Fasen molen 1 - handmatig opgeven van de fasentoedeling aan module molen 1. Geef hier namen in van fasen, gescheiden met ;. Bijvoorbeeld: "101;102;105"
- Fasen molen 2/3 - idem, voor module molen 2 en 3. Is er geen twee of derde molen, laat het veld dan leeg

## Werking

Bij 'Achtergrond' is op hoofdlijnen de werking van de analyse omschreven. Hieronder volgt een meer gedetailleerde en technische omschrijving van de wijze waarop de cyclustijd wordt bepaald.

### Configuratie

De analyse kijkt uitsluitend naar:

- Status regelingen (indien ingeschakeld
- Externe (werkelijke) signaalgroepstatus
- Detectie metingen
    - Indien er wordt gefilterd, worden enkel detectie meldingen die niet als invalide zijn aangemerkt meegenomen in de analyse. De analyse zelf kijkt naar bezet en onbezet zijn van detectie zonder te kijken naar evt. storingsdata in de VLOG berichtgeving

Er wordt uitsluitend gekeken naar detectoren die zijn toegewezen aan een richting, en uitsluitend de volgende types doen mee:

- Koplussen
- Lange lussen
- Verweg lussen
- Knoppen (schakelbaar)

_Tip:_ wanneer er vreemd of zeer hoge waarden optreden, is een eerste check of de toedeling van detectoren klopt, met name voor drukknoppen.

Activiteit op detectoren wordt bijgehouden, en indien een detector afvalt "vervalt" ook de activiteit. Hierdoor wordt het mogelijk ook inactiviteit te meten, en zodanig een "rustmoment" te bepalen. Tevens

Voor knoppen geldt: tijdens geel en rood wordt gemeten; indien er wordt gedrukt wordt een vlag waar, die weer afvalt zodra de richting groen wordt. Tijdens het waar zijn van de vlag geldt dat er "activiteit" is op de betreffende richting, ongeacht afvallen van de knop melding of verdere drukknop meldingen.

Zijn er situaties zijn waarin een aanvraag middels een drukknop weer ingetrokken kan worden, kunnen drukknoppen in de analyse worden genegeerd. De meting zal alsnog goed uitgevoerd worden, omdat de omlooptijd van de overige richtingen wel beïvloed wordt door richtingen met enkel drukknoppen.

#### Meerdere module molens

Indien de regeling beschikt over meerdere module molens, kan dit in de instellingen worden aangegeven middels een vinkje. Default deelt YAVV de fasen als volgt op in module molens:

- 0-200: molen 1
- 200-299: molen 2
- 300-399: molen 3
    - meer dan 3 molens worden momenteel niet ondersteund

Hierbij is dus het uitgangspunt dat fasen cijfermatige namen hebben. Is sprake van een andere structuur, dan kan in de instellingen de verdeling van de fasen over de molens handmatig worden opgegeven.

### Verloop meting

De meting start wanneer:

- De meting loopt niet
- Er wordt detectie activiteit gezien op een richting met status rood

De meting eindigt wanneer voor alle richtingen geldt:

- Er is geen activiteit (meer) of de richting is reeds gerealiseerd, óf
- De activiteit is niet van een drukknop (indien actief), het is groen op de richting, en de laatst gemeten activiteit op de richting is minimaal de ingestelde minimum tijd geleden

Na afronden van een meting wordt de status meten uitgezet. Vervolgens wordt direct gekeken of wordt voldaan aan de voorwaarden om een meting te starten, en start deze dus weer direct indien van toepassing.

Metingen lager dan de ingestelde minimum waarde worden niet in de resultaten opgenomen; de meting herstart wel na een dergelijke meting.
