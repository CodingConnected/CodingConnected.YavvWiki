---
title: "Ontbrekende data in VLOG"
date: 2025-05-14
---

Een terugkerende vraag waar het gaat om de inhoud van VLOG data, is waarom bepaalde data niet tevoorschijn komt. In veruit de meeste gevallen komt dit, doordat data van het betreffende type niet in de brondata (= de VLOG data) zit.

## Voorbeelden van ontbrekende data

Hieronder enkele terugkerende voorbeelden van data die wordt verwacht, maar niet verschijnt in de fasenlog:

- DSI data (VLOG update type 28 ofwel 0x1C)

- Van signaalgroepen/uitgangen de updates, waardoor er enkel op de hele 5 minuten grens wijzigingen te zien zijn (VLOG status type 9 of 13 ofwel 0x09 of 0x0D)

- Detectoringang lengte informatie (VLOG update type 62 ofwel 0x3E)

- Etc.

## Controleren of bepaalde data in de VLOG zit

Gaat het om ASCII gecodeerde data, dan is het vrij eenvoudig om na te gaan of bepaalde data wel/niet in de VLOG data aanwezig is. Hieronder een beknopt stappenplan:

- Eerste stap: open de data in YAVV en pas de instellingen zodanig aan (via de toolbars "GUS/WUS" en "Speciaal") dat de betreffende data in principe in de fasenlog getoond zou moeten worden
    - Ja: eureka!
    
    - Nee: ga verder...

- Ga na of sprake is van ASCII gecodeerde VLOG:
    - Open een VLOG bestand in notepad of een vergelijkbare tekst editor.
    
    - Zijn er leesbare regels te zien, zoals bijvoorbeeld "012025022600000000", en zijn er enkel cijfers (0-9) en letters (A-F) zichtbaar? Dan is het ASCII gecodeerde VLOG data.
    
    - Zijn er vreemde en onleesbare tekens te zien? Dan is het binaire VLOG data. Deze kan worden omgezet naar ASCII via de tooling voor opknippen van VLOG data (zowel in YAVV als YAVC-client via menu Tools > Splitsen VLOG data). Bij het wegschrijven van de gesplitste data kan worden gekozen voor binair of ASCII; het splitsen heeft verder enkel effect op de data wanneer deze een langere periode beslaat dan het gekozen splits-interval.

- Tweede stap: ga na wat het VLOG-interne type nummer is van de data die wordt verwacht.
    - Raadpleeg hiervoor de V-Log specificatie, bijvoorbeeld te vinden door op g00gle te zoeken naar "v-log 3.0 protocol". Op bladzijde 17-18 staat een tabel met status berichten, op bladzijde 20-22 een tabel met status berichten.
    
    - Zoek het juiste type nummer op: voor DSI berichten, bijvoorbeeld 

- Open nu een relevant VLOG bestand in bijvoorbeeld Notepad++ of een andere tekst editor met de mogelijkheid te zoeken met gebruik van "regular expression".
    - Voorbeeld: we willen weten of er DSI berichten in de data zitten
    
    - Ctrl+F in Notepad++
    
    - Voer in: ^1C
        - Dat betekent: we zoeken naar 1C (hexidecimaal, dus waarde 28, het VLOG type voor KAR/DSI)
        
        - Het dakje ^ aan het begin betekent: we zoeken enkel naar regels die _starten_ met de navolgende tekst
    
    - Kies bij "Search mode" (in Notepad++) voor "Regular expression"
    
    - Klik "Find next"
    
    - Op dezelfde wijze kunnen bv ook timestamps worden opgezocht (type 1 ofwel 0x01)
    
    - Let op: VLOG is in hexidecimaal formaat in ASCII gecodeerd, dus voor type 28 moeten we zoeken naa 1C. Gebruik de Windows Rekenmachine in programmeur modus tbv omrekenen tussen decimaal en hexidecimaal

Op deze manier kan worden vastgesteld: er zit in de betreffende VLOG data wel/geen bericht van type X.

Wordt in de data wél een bericht gevonden, maar wordt dat in YAVV niet getoond? Dan is er mogelijk sprake van een bug; [geef dit vooral door](https://www.codingconnected.eu/contact/bugreport/) aan CodingConnected, dan kunnen we kijken wat de oorzaak is.

## Oorzaken van ontbrekende data

Is eenmaal vastgesteld dat bepaalde data niet in de VLOG aanwezig is, waar dat wel gewenst is, dan is de vraag hoe dat komt. Hieronder volgen een aantal veel voorkomende oorzaken van het ontbreken van data:

- Voor KAR/DSI: er komt geen data binnen in de automaat, en dus niet de VLOG

- Voor lengtedetectie/snelheidsdetectie: de hardware is niet operationeel. _Let op_: voor lengte en snelheid moet worden gekeken naar _ingangen_ in de VLOG data. In tegenstelling tot wat de naam doet vermoeden, is deze informatie namelijk gekoppeld aan een ingang, en niet aan een detector.

- Configuratie data (VLOG type 127 ofwel 0x7D): het betreft VLOG versie 2, waar dit nooit in zit. Of: de informatie is door de regelapplicatie of andere VLOG-producerende applicatie (bv. een TLC-FI consumer app) niet in de data opgenomen.

- Updates (van bijvoorbeeld signaalgroepen, uitgangen, of andere data): bij niet-CCOL ontbreekt vaak interne signaalgroep status, omdat dit niet bestaat in bv. Flowtack. Bij CCOL regelingen betreft het hier vaak een misconfiguratie van de VLOG instellingen.

Voor niet-CCOL regelingen waar verwachte data ontbreekt, zal dit moeten worden onderzocht door de leverancier van de regelapplicatie en/of automaat.

## Instellingen voor VLOG binnen CCOL

CCOL heeft een groot arsenaal aan mogelijke instellingen voor wat er wel/niet gelogd moet worden en waar. Veel van deze instellingen zijn aan te passen op straat, diverse instellingen moeten echter ook reeds bij het laden van de applicatie correct zijn ingesteld. Hieronder volgt een zo beknopt en toch zo compleet mogelijk overzicht van de relevante instellingen. Voor details wordt verwezen naar de documentatie van CCOL, waarin deze informatie is verspreid over een aantal hoofdstukken.

### Filebased en streaming: LOG en MON

Veel instellingen zijn afzonderlijk beschikbaar voor filebased VLOG en streaming VLOG. Binnen CCOL wordt hieraan gerefereerd als LOG (filebased) en MON (streaming). Het is aan te raden de instellingen voor beide typen gelijk in te stellen om verwarring omtrent de inhoud van de data zoveel mogelijk te voorkomen.

### Etc.
