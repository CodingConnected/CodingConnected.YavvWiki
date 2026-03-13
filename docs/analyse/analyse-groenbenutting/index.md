---
title: "Analyse: groenbenutting"
date: 2019-11-28
---

De analyse groenbenutting doet op basis van de VLOG data een inschatting per richting van het aandeel van de groentijd die is benut door verkeer. Het betreft een inschatting omdat detectie data slechts ten dele een accurate weergave van het gedrag van voertuigen in werkelijkheid op de kruising.

Voor de capaciteitsbepaling zijn de volgende instellingen beschikbaar, steeds met defaults in \[blokhaken\]:

- Eerste voertuig zonder optrekverlies \[6\] - Vanaf dit voertuig dat vanaf startgroen afrijdt geldt het maximale hiaat in plaats van een opgehoogd hiaat t.b.v. bepaling van benut groen tussen voertuigen.

- Minimale hiaat \[0.5\] - Minimaal hiaat tussen ED en SD om een volgend voertuig te tellen. Hiermee wordt voorkomen dat bv trailers als aparte voertuigen worden geteld. De telling is bij groenbenutting uitsluitend van belang om te bepalen of voor een voertuig nog rekening gehouden moet worden met optrekverlies - en dus een langer maximaal hiaat.

- Maximaal hiaat \[2.5\] - Maximaal hiaat tussen ED en SD: indien het langer duurt dan deze waarde voor de volgende SD optreedt, wordt een default van 1,0 sec. genomen als benut aandeel van het opgetreden hiaat. Is het hiaat kleiner dan of gelijk aan de instelling, dan wordt het hiaat zelf genomen

De opzet van het algoritme is als volgt:

- De analyse start op startgroen.

- Indien een koplus op dat moment bezet is worden voor die lus geteld passerende voertuigen geteld; zo niet, dan wordt de telling gestart op de instelling van het eerste voertuig zonder optrekverlies, waardoor die geen invloed heeft.

- Een melding van SD tot ED wordt enkel als voertuig geteld indien het voorliggend hiaat groter of gelijk is aan de instelling van het minimale hiaat

- Op einde detectie wordt de complete duur van de melding detectie bezet als 'benut groen' geregistreerd

- Op start detectie wordt bepaald welk aandeel van het voorliggend hiaat benut was:
    - Gegeven voertuig nummer N, wordt de waarde bepaald van ((\[maxHiaat\] + 0,5 \[1eVtgZonderOptrVerl\]) - N \* 0,5); dit is waarde maxH1
    
    - De instelling voor het maximale hiaat noemen we maxH2
    
    - Nu wordt de maximale waarde genomen tussen maxH1 en maxH2; dit is waarde maxH
    
    - Indien op start detectie tijdens groen het hiaat groter is dan maxH, wordt een default van 1,0 sec. als benut groen genoemen, anders het eigenlijke hiaat

- De analyse eindigt op start geel. De groenbenutting wordt bepaald door de berekende benutte groentijd te delen door de tijd SG tot EG, en dit te vermenigvuldigen met 100. Bij meerdere koplussen wordt deze waarde gedeeld door het aantal koplussen. De waarde wordt altijd weggeschreven, ook als deze 0 is: dit betekent dan een groenfase zonder bezetting van de koplus.
