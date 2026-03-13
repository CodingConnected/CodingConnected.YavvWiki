---
title: "Analyse: rijtijd OV"
date: 2025-04-29
---

De rijtijd van het openbaar vervoer wordt bij deze analyse bepaald door te kijken naar:

- De tijd inmelding tot uitmelding, _tenzij_

- Bij uitmelding tijdens rood, de tijd inmelding tot eerstvolgende moment startgroen na uitmelding

Op deze wijze wordt rekening gehouden met de mogelijkheid dat bij gebruik van KAR voor in- en uitmelden, de locatiebepaling soms onnauwkeurig is, wat kan leiden tot uitmelden vóór de stopstreep.

De opties voor de analyse zijn als volgt \[defaults staan in blokhaken\]:

- DSI uit berichten negeren \[uit\]: indien aan, wordt enkel gekeken naar DSI "in" berichten. Dit is soms relevant bij de tram.

- Filteren op voertuig categorie \[Alle categoriën\]: hiermee kunnen DSI berichten worden gefilterd, zodat enkel berichten met het opgegeven type worden meegenomen voor de analyse

- Check op lijnnummer \[uit\]: hiermee kan worden gefilterd op lijnnummer

- Lijnnummers: indien de check aan staat, kan hier een komma-gescheiden lijst met nummers worden opgegeven

- Maximale tijd meting \[180\]: na verloop van dit aantal seconden na een inmelding, vervalt de meting; hiermee worden extreem hoge metingen voorkomen, bijvoorbeeld in geval er geen uitmelding volgt

- Minimale tijd DSI uit na start rood \[2.0\]: volgt een uitmelding tijdens rood _binnen_ dit aantal seconden na start rood, dan wordt toch dit moment genomen als einde van de meting, en niet het navolgende moment start groen

- Controleer status regelen \[aan\]: indien aan, wordt gedurende niet-regelen, _altijd_ gekeken naar de tijd inmelding tot uitmelding, en wordt de bijzondere omgang met uitmelding-tijdens-rood dus uitgeschakeld

- Niet meten tijdens niet-regelen: niet meten als de status regelen niet is 'regelen' of 'alles rood'; gedurende niet-regelen wordt danb dus in het geheel niet gemeten
