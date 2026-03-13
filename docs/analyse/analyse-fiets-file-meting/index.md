---
title: "Analyse: fiets file meting"
date: 2023-02-17
---

Bij drukke kruispunten kan het voorkomen dat de afwikkeling van fietsers niet optimaal verloopt en sprake is van filevorming. Om een beeeld te kunnen krijgen van de frequentie waarmee hiervan eventueel sprake is, kan dit algoritme worden gebruikt.

De analyse bepaalt op basis van een aantal verschillende indicatoren of er sprake is van filevorming; per voorwaarde wordt een score toegekend; is er in totaal sprake van een score hoger dan een ingesteld minimum (default = 6), dan is de inschatting dat er sprake is van filevorming, en wordt er een analyse resultaat gelogd.

De voorwaarden waarnaar wordt gekeken zijn:

- Aantal getelde fietsers tijdens rood
    - bij minimaal 8: score = 1
- Totale bezettijd koplus gedurende groen/geel
    - bij 10 sec.: score = 1
    - bij 15 sec.: score = 2
- Totale bezettijd verweglus
    
    - bij 13 sec.: score = 1
    
    - bij 25 sec.: score = 2
- Bezetting van de verweglus langer dan x (default = 4.0 sec.)
    - indien dit optreedt: 5 punten
- Tijdsduur tot minimaal hiaat op koplus na startgroen
    
    - bij 7 sec.: score = 1
    
    - bij 10 sec.: score = 2

Bij de default minimale score van 6 punten geldt dus, dat altijd aan minimaal 2 voorwaarden moet worden voldaan - en meestal aan 4 omdat een lange bezetting van de verweglus zelden voorkomt - voordat een analyse resultaat wordt gelogd. Dit kan natuurlijk anders worden ingesteld, daarbij is voorzichtigheid geboden, omdat moet worden voorkomen dat reguliere drukte als zijnde 'file' uit de analyse naar voren komt.

De volgende instellingen zijn beschikbaar (defaults in blokhaken):

- Minimale score om een resultaat weg te schrijven \[6\]: indien deze score wordt gehaald wordt een analyse resultaat aangemaakt; anders niet
- Minimale hiaattijd koplus \[1.0 sec.\]: de minimale tijd dat de koplus tijdens groen af moet vallen om de wachtende fietsers als "in beweging" te markeren ("optrektijd")
- Minimale bezettijd verweglus \[4.0 sec.\]: de minimale tijd dat de verweglus bezet moet raken om te zorgen dat dit event een score geeft
- Minimaal aantal fietsers tijdens rood \[8\]: minimaal aantal op de verweglus gemeten fietsers om te zorgen dat dit een score geeft
- Grenswaarde totale bezettijd koplus tijdens groen/geel grenswaarde laag \[10.0 sec.\]: zie boven voor uitleg
- Grenswaarde totale bezettijd koplus tijdens groen/geel grenswaarde hoog \[15.0 sec.\]: zie boven voor uitleg
- Grenswaarde totale bezettijd verweglus grenswaarde laag \[13.0 sec.\]: zie boven voor uitleg
- Grenswaarde totale bezettijd verweglus grenswaarde hoog \[25.0 sec.\]: zie boven voor uitleg
- Grenswaarde minimaal hiaat op koplus na startgroen laag \[7.0 sec.\]: zie boven voor uitleg
- Grenswaarde minimaal hiaat op koplus na startgroen hoog \[10.0 sec.\]: zie boven voor uitleg
