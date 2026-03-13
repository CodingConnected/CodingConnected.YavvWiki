---
title: "Analyse: roodrijders"
date: 2020-04-22
---

Roodrijders worden in YAVV gevonden door te kijken naar de melding start detector laag voor koplussen. Instelbaar is hoeveel seconden na start rood wordt gemeten (default 1 seconde). Deze marge geldt in YAVV ook aan het begin van de ingeladen data.

Een aantal punten hier van belang:

- Let op! De marge geldt enkel voor voertuigen waarvan start detectie vóór start rood heeft plaatsgevonden. Detectie meldingen die compleet na start rood liggen worden altijd als roodrijder gezien.

- In YAVV worden roodrijders gerapporteerd inclusief eventuele vroegstarters.

- Indien [filtering](https://www.codingconnected.eu/yavv/filtering-functionele-omschrijving/) wordt toegepast worden koplus meldingen die als foutief zijn gemarkeerd niet meegenomen in de analyse.

De volgende instellingen zijn voor de roodrijders analyse beschikbaar (defaults in blokhaken):

- Marge na start rood \[1.0 s.\]: voertuigen waarvan **start detectie voor start rood** ligt, en **einde detectie binnen de marge** valt, worden **niet als roodrijder aangemerkt**. Deze instelling maakt het mogelijk rekening te houden met lange voertuigen die feitelijk afrijden (de stopstreep passeren) tijdens geel.

- Minimale roodtijd \[0.0 s.\]: de minimale tijd dat het rood moet zijn geweest voor roodrijders terugkomen in de analyse resultaten. Deze instelling is dus wezenlijk anders dan de hiervoor genoemde "marge". Het is hiermee mogelijk een beeld te krijgen van de "aard" of "ernst" van het roodrijden: vooral snel na startrood, of ook vaak zomaar ergens?

- Maximale afstand koplus tot stopstreep \[5.0 m.\]: indien een lus met type koplus verder dan deze instelling van de stopstreep ligt, wordt die bij de roodrijders analyse niet meegenomen

- Controlleer status regelen \[waar\]: indien waar, worden enkel roodrijders geregistreerd indien de status alles-rood of regelen (werkelijke status ofwel WUS) is gezien in de VLOG data.

- Richtinggevoelig meten \[onwaar\]: indien waar, wordt bij opeenvolgende koplussen op dezelfde rijstrook richtinggevoelig gemeten. Dit vergt dan geen verdere instellingen, enkel twee koplussen op dezelfde rijstrook waarvoor qua afstanden is ingesteld dat die achter elkaar liggen. Er wordt gemeten of ED van de verste lus maximaal een instelbare tijd voor SD van de voorste lus ligt; wordt de max overschreden, dan wordt geen roodrijder geregistreerd.

- Richtinggevoelig meten max. detector afstand \[5.0 m.\]: maximale afstand tussen koplussen op dezelfde strook om richtinggevoelig te meten. Indien twee opeenvolgende koplussen dus meer dan deze afstand uit elkaar liggen (gemeten als het verschil tussen de ingesteld waarde afstand-tot-stopstreep), wordt niet richtinggevoelig gementen. Dit is enkel beschikbaar en relevant indien richtinggevoelig meten is ingeschakeld.

- Richtinggevoelig meten max. volgtijd \[2.0\]: maximale tijd tussen ED van de verste lus en SD van de voorste lus in geval van richtinggevoelig meten. Dit is enkel beschikbaar en relevant indien richtinggevoelig meten is ingeschakeld.

Indien geen roodrijders in bepaalde data worden gevonden, waar dit wel de verwachting is, zijn er waarschijnlijk geen of de verkeerde lustypen ingesteld. Controleer dit in het tabblad met de VLOG configuratie.

## Opties voor andere omgang met OV

Voor openbaar vervoer zijn een aantal aanvullende opties beschikbaar (sinds YAVV 1.20 en YAVC-client 3.7). Dit betreft een vrij specifieke use case en moet met enige terughoudendheid worden toegepast.

Het betreft de volgende opties, die indien gebruikt dus uitsluitend van toepassing zijn op richtingen die zijn geconfigureerd als signaalgroep type "OV":

- OV afzonderlijk meten \[ONWAAR\]: indien ingeschakeld, worden signaalgroepen met type "OV" apart geanalyseerd, met onderstaande opties

- Alleen meten bij SD na start rood \[ONWAAR\]: indien ingeschakeld, worden enkel detector meldingen waarvan het begin (start detectie) ná start rood heeft plaatsgevonden meegenomen als roodrijder; deze optie, evenals de volgende, is bedoeld om bij zeer lange voertuigen die starten met afrijden tijdens groen (en geel) niet als roodrijder te meten

- Alleen meten bij SD na start geel \[ONWAAR\]: indien ingeschakeld, worden enkel detector meldingen waarvan het begin (start detectie) ná start geel heeft plaatsgevonden meegenomen als roodrijder

- Marge na start rood OV \[1\]: dit is een alternatieve waarde voor de marge na start rood, die wordt toegepast op OV signaalgroepen. Zie voor de werking de beschrijving bovenaan, betreffende de reguliere roodrijder meting. Merk op: indien "alleen meten bij SD na start rood" is ingeschakeld, heeft deze marge geen effect

- Minimale detector bezettijd \[0\]: hiermee kan worden geregeld dat een detector minimaal een bepaalde duur bezet moet zijn geweest voordat een detectormelding als potentiele roodrijder wordt meegenomen in de analyse

- DSI voertuignummer loggen \[ONWAAR\]: indien waar, wordt bij een analyse resultaat (dwz een vermeende roodrijder) in de "extra data" bij het resultaat, het laatst bekende voertuignummer opgeslagen zoals uit de DSI buffer gelezen. Daarbij geldt:
    - Dit wordt enkel dan gelogd, indien het laatste DSI bericht tussen SD en ED van de detectormelding ligt
    
    - De DSI melding moet zijn verbonden met de betreffende signaalgroep
    
    - **LET OP!** Indien dit wordt gelogd, is hiermee geenszins gezegd, dat het betreffende voertuig daadwerkelijk door rood is gereden; de aard van de data (VLOG) is zodanig, dat dit niet kan worden vastgesteld. Raadpleeg altijd de fasenlog, en houdt zelfs dan rekening met mogelijke meetfouten en grote marges!

De opties zoals hier omschreven zijn vooral bedoeld om een betere meting van door rood rijdende trams mogelijk te maken. Gebruik deze opties enkel dan, wanneer die voor een specifieke use case nodig zijn om zo bruibaar mogelijke analyse resultaten te krijgen. In de allermeeste gevallen zal de reguliere analyse roodrijders volstaan.

Indien wél gebruik gemaakt wordt van deze opties, is het aan te raden dit goed te testen en de uitkomsten (aanvankelijk) steeksproefsgewijs na te lopen met de fasenlog, om te voorkomen dat bijvoorbeeld te weinig meldingen in de resultaten zichtbaar worden, en zeker te stellen dat de instellingen passen bij de concrete situatie.
