---
title: "Analyse: capaciteit"
date: 2019-11-26
---

De capaciteitsanalyse doet op basis van de VLOG data een inschatting van de capaciteit per richting. Het betreft een inschatting omdat de meting vaak gebaseerd is op slechts enkele voertuigen, en daardoor sterk wordt beinvloed door variatie in de data. Daarnaast geeft detectie data slechts ten dele een accurate weergave van het gedrag van voertuigen in werkelijkheid op de kruising.

Voor de capaciteitsbepaling zijn de volgende instellingen beschikbaar, steeds met defaults in \[blokhaken\]:

- Tellen vanaf voertuig \[4\] - Vanaf welk opeenvolgende voertuig vanaf start groen wordt gemeten

- Minimale hiaat \[0.5\] - Minimaal hiaat tussen ED en SD om een volgend voertuig te tellen. Hiermee wordt voorkomen dat bv trailers als aparte voertuigen worden geteld.

- Maximaal hiaat \[1.5\] - Maximaal hiaat tussen ED en SD waarna de meting wordt afgebroken. Merk op: deze waarde geldt pas vanaf het voertuig met nummer N waarvoor geldt: N \* 0,5 >= \[maxHiaat\]

De opzet van het algoritme is als volgt:

- De analyse start op startgroen, indien één of meer koplussen op dat moment bezet is

- De analyse eindigt sowieso op start rood, of eerder indien de maximale hiaattijd wordt overschreden

- Er geldt een maximale hiaattijd _tussen_ voertuigen (= ED en SD); wordt deze overschreden, dat stopt de analyse. Hierbij geldt:
    - Gegeven voertuig nummer N, wordt de waarde bepaald van (5,5 - N \* 0,5); dit is waarde maxH1
    
    - De instelling voor het maximale hiaat noemen we maxH2
    
    - Nu wordt de maximale waarde genomen tussen maxH1 en maxH2; dit is waarde maxH
    
    - Indien op start detectie tijdens groen of geel het hiaat groter is dan maxH, wordt de analyse beeindigd

- Start detectie van het voertuig vanaf waar wordt geteld geldt als start meetperiode

- Eind meetperiode wordt als volgt bepaald:
    - Op eind detectie wordt einde meetperiode altijd ingesteld op tijdstip ED + 1,0 seconde
    
    - Op start detectie wordt einde meetperiode overschreven door tijdstip SD indien het maximale hiaat niet wordtr overschreven, of door tijdstip laatste ED + 1,0 indien het hiaat wel wordt overschreden

- Het resultaat, indien aanwezig, wordt altijd weggeschreven op start rood. Alleen resultaten met een minimaal aantal getelde voertuigen (geteld vanaf het Nde voertuig zoals ingesteld) van 3 worden gebruikt. Het resultaat wordt bepaald als ((totaal-aantal-voertuigen) / (einde-meet-periode - start-meet-periode)) \* 3600
