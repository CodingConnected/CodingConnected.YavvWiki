---
title: "Analyse: gemiddelde wachttijd fietsers"
date: 2021-07-07
---

Om het effect van bepaalde maatregelen te kunnen beoordelen kan het interessant zijn te kijken naar gemiddelde wachttijden. In tegenstelling tot de wachttijd eerstwachtende worden hierin alle passerende voertuigen meegenomen. Zo kan het bijvoorbeeld zijn dat na een maatregel de wachttijd eerstwachtende gelijk is gebleven (of zelfs is toegenomen), maar er meer fietsers afrijden tijdens groen, waardoor de gemiddelde wachttijd, en daarmee de totale verliestijd, af is genomen. Deze analyse geeft een inschatting van de gemiddelde wachttijd voor fietsers.

_Let op!_ De analyse gebeurt op basis van informatie omtrent massa detectie uit VLOG data. Daarom zijn de uitkomsten per definitie een inschatting: het is op basis van deze data niet mogelijk precies te weten waar er wanneer hoeveel fietsers waren. Daarom wordt gewerkt met een aantal aannames, en is de uitkomst van de analyse altijd een inschatting van de werkelijke waarde.

De huidige analyse werkt door fietsers te registreren op basis van verweg detectie. Dit werkt als volgt:

- Indien er één verweg lus is, wordt die gebruikt
- Indien er twee verweg lussen zijn, wordt richtinggevoel gemeten indien de lussen op maximaal 5 meter (instelbaar) van elkaar liggen en start detectie van de 2e lus volgt maximumaal 2 seconden (instelbaar) na start detectie van de eerste lus
- Is enkel een koplus (of twee koplussen) aanwezig, dan wordt momenteel niets berekend
- _Let op!_ De juiste instellingen voor de ligging van detectie zijn belangrijk bij deze analyse

Het bepalen van de gemiddelde wachttijd verloopt vervolgens als volgt:

- Per fietsers wordt op basis van een instelbare snelheid (default 15 km/u) bepaald wanneer deze bij de stopstreep zal arriveren (hier is dus een correct ingestelde afstand tot de stopstreep van belang)
- Wanneer de fietser volgens de berekening bij de stopstreep arriveert wordt gekeken naar de status van de signaalgroep:
    - Tijdens rood, ná de ingestelde minimale roodtijd wordt de fietser geteld en wordt de wachttijd voor de fietser gestart
    - Tijdens groen wordt de fietser geteld, er geldt dan een wachttijd van 0
    - Tijdens geel en tijdens rood vóór de minimale roodtijd is bereikt, geldt dat de fietser wordt geteld en apart geregistreerd; bij bereiken van de minimale roodtijd wordt hier apart naar gekenen (zie volgende bullet)
- Een instelbare tijd na start rood (default 2.0 seconden) wordt de berekening afgerond:
    - De totale wachttijd van fietsers die hebben gewacht wordt bepaald
    - Zijn er fietsers die volgens de berekening tijdens geel of vóór de minimale roodtijd zijn aangekomen bij de stopstreep, dan wordt gekeken of de koplus bezet is. Zo ja, dan geldt:
        - Is de laatste fietser tijdens geel afgereden, dan wordt deze verplaatst van de huidige naar de volgende ronde
        - Is de laatste fietser tijdens rood afgereden, dan worden alle fietsers die zijn afgereden tijdens rood verplaatst naar de volgende ronde
        - Met deze werkwijze wordt gepoogd een balans te vinden tussen het soms overschatten (onterecht verplaatsen van fietsers naar de volgende ronde) en onderschatten (onterecht meerekenen van fietsers met de huidige ronde) van de totale wachttijd
    - De totale wachttijd gedeeld op het aantal fietsers geeft de gemiddelde wachttijd voor deze realisatie (ronde)

Bij de implementatie zijn een aantal keuzen gemaakt v.w.b. omgang met bijzonderheden:

- Roodrijders worden niet apart behandeld. Immers, deze zouden hebben moeten wachten. Een roodrijder wordt dus als reguliere fietser met wachttijd vanaf berekende aankomst bij de stopstreep meegenomen
- Indien de aanvraag wordt ingetrokken wordt de berekening afgebroken. Dit is informatie die in de interne signaalgroepstatus zit, die niet altijd beschikbaar is
- Indien startgroen volgt binnen de ingestelde minimale roodtijd wordt direct de berekening afgerond en de volgende ronde gestart
- Bij meerdere rijstroken (bv. een fietser in twee richtingen met één signaalgroep) wordt het totaal van alle fietsers berekend; de omschreven omgang met fietsers tijdens geel/begin rood geldt per rijstrook
- Wordt gedurende een meting geen enkele activiteit gezien op de koplus, dan wordt de meting niet meegenomen in de resultaten. Dit kan worden uitgeschakeld, voor het geval bv. de koplus defect is. Bij signaalgroepen zonder koplussen geldt deze voorwaarde niet

De volgende instellingen zijn beschikbaar voor de analyse (defaults in blokhaken):

- Minimale roodtijd \[2.0\] – minimale tijd na start rood voordat de berekening wordt afgerond; dit is het punt waarop de bezetting van de koplus wordt bekeken; fietser die bij de stopstreep arriveren tussen startrood en dit moment worden niet meegenomen
- Snelheid fietsers \[15\] – snelheid in km/u waarmee wordt gerekend om te bepalen wanneer fietsers bij de stopstreep arriveren
- Maximale afstand richtinggevoelig meten \[5.0\] – maximale afstand tussen twee lussen om ze als richtinggevoelig paar te behandelen
- Maximale rijtijd richtinggevoelig meten \[2.0\] – maximale afstand tussen start detectie op richtinggevoelig lussenpaar
- Kijken naar activiteit op de koplus \[aan\] - al dan niet kijken naar activiteit op de koplus om een meting wel/niet mee te nemen in de resultaten
