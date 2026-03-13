---
title: "Analyse: schatting wachtrijlengte"
date: 2024-02-13
---

Het is mogelijk in YAVV/YAVC een schatting te laten maken van de lengte van ontstane wachtrijen.

**_! LET OP !_** Het betreft hier uitdrukkelijk een **grove schatting**. De aard van de brondata (dus de VLOG data) zorgt dat een exacte bepaling van de wachtrijlengte niet mogelijk is. Immers, enkel de bezetting van detectoren is bekend; er is dus geen informatie omtrent positie, snelheid en/of lengte van voertuigen.

De meting verloopt in hoofdlijnen als volgt:

- Op start groen wordt gekeken of er sprake is van bezetting van één of meer koplussen; zo ja, dan wordt de meting gestart, zo nee, dan wordt niet gemeten.

- Bij start detectie wordt het einde van de wachtrij bepaald door te kijken naar het gevallen hiaat: indien een groot genoeg hiaat valt wordt de meting afgesloten

- Bij einde detectie op de koplus wordt tijdens groen geteld, indien een minimaal hiaat is gevallen.

- Bij einde detectie op de koplus tijdens groen wordt tevens op basis van de opgetreden bezettijd (voor eerste voertuig: tijd vanaf start groen) en de positie in de rij, geschat welke lengte het voertuig heeft, waarbij wordt gekozen tussen regulier en lang. Voor elk volgende voertuig wordt verondersteld dat dit sneller rijdt dan het voorgaande; daarbij gelden de volgende grenswaarden om te bepalen in welke categorie een voertuig terecht komt:
    - 1e voertuig: 4 seconden (lager of gelijk: regulier voertuig, hoger: lang voertuig)
        - Bij het eerste voertuig wordt rekening gehouden met een reactietijd van 1 seconde (dit zit inbegrepen in de grenswaarde van 4 seconden)
    
    - 2e: 2,3 seconden
    
    - 3e: 1,5 seconden
    
    - 4e: 1,0 seconden
    
    - 5e en verder: 0,75 seconden

- Op start groen wordt van de vorige cyclus het resultaat gelogd, indien er gemeten is (zie eerste bullet). Hierbij wordt per koplus gekeken naar de totale geschatte lengte, en geldt de langste waarde als resultaat.

- Is sprake van overstaan, dan worden resultaten eerst in een buffer gelogd. Pas als overstaan voorbij, worden alle resultaten vervolgens weggeschreven. Daarbij wordt vanaf de laatste cyclus steeds een (instelbaar, default 25%) aandeel van de wachtrij bij de voorgaande cyclus opgeteld. Bijvoorbeeld:
    - 1e realisatie, meting van 50 meter, overstaan gezien, resultaat in buffer
    
    - 2e realisatie, meting van 45 meter, weer overstaan, tweede resultaat in buffer
    
    - 3e realisatie, meting van 20 meter, géén overstaan, wegschrijven resultaten:
        - 3e realisatie = 20 meter
        
        - 2e realisatie = 45 + 0,25 \* 20 = 50 meter
        
        - 3e realisatie = 50 + 0,25 \* 50 = 62,5 meter
    
    - Het moge duidelijk zijn dat dit een suboptimale oplossing is, en er slechts sprake is van _invloed_ van overstaan op de resultaten, niet van een werkelijk correctie; middels de omschreven werkwijze is geprobeerd het optreden van wachtrijen langer dan die in één keer kunnen afrijden, te verdisconteren in de meetresultaten

De hierboven genoemde grenswaarden zijn bepaald door voor een theoretisch voertuig van 6 meter lang met een versnelling van 2 m/s2, te bepalen hoeveel tijd nodig is om af te rijden, uitgaande van diverse initiële snelheden. Dit is voor een theoretisch lang voertuig van 16 meter met een versnelling van 2 m/s2 ook gedaan. Voor beide typen is vervolgens een aanname gedaan omtrent de initiële snelheid van openeenvolgende voertuigen, wat per zoveelste voertuig een tijd oplevert die het kost de lus te passeren. De hierboven genoemde grenswaarden zijn gekozen tussen de gevonden tijden van beide theoretische voertuigtypen.

Voor deze analyse zijn de volgende instellingen beschikbaar \[defaults in blokhaken\]:

- Lengte regulier voertuig \[5.0\]: lengte in meters dat als regulier aangemerkte voertuigen toevoegen aan de wachtrijlengte

- Lengte lang voertuig \[12.0\]: lengte in meters dat als lang aangemerkte voertuigen toevoegen aan de wachtrijlengte

- Lengte hiaat tussen voertuigen \[1.0\]: veronderstelde lengte in meter van het hiaat dat tussen voertuigen valt; dit wordt vanaf het 2e voertuig opgeteld bij de wachtrijlengte per voertuig

- Minimaal hiaat \[1.2\]: minimaal hiaat dat moet vallen in seconden om koplus meldingen als afzonderlijke voertuigen te meten

- Minimaal hiaat voor einde wachtrij \[3.0\]: minimaal hiaat in seconden dat moet vallen om de wachtij te zien als afgereden, en de meting te beëindigen

- Controleren op overstaan \[waar\]: indien dit aan staat wordt rekening gehouden met overstaan; anders worden resultaten altijd direct gelogd en wordt niet gekeken naar overstaan

- Assumptie factor overgebeleven wachtrij bij overstaan \[0.25\]: aandeel van de wachtrij van navolgende cyclus dat in geval van overstaan wordt opgeteld bij de voorgaande cyclus; bij meerdere opeenvolgende cycli met overstaan wordt steeds bij de voorgaande cyclus dit aandeel van de berekend 'totale lengte + oversta lengte' genomen als basis; het stapelt zich dus terugwerkend op
