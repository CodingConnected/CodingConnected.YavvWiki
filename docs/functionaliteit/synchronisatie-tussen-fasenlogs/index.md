---
title: "Synchronisatie tussen fasenlogs"
date: 2021-01-08
---

Het is in YAVV mogelijk te "synchroniseren" tussen documenten, waarbij bepaalde aspecten van een document synchroon worden gehouden met het gekoppelde document. Vooralsnog geldt dit uitsluitend voor de fasenlog.

_Let op_: de huidige versie van YAV-client biedt nog geen mogelijkheden voor synchronisatie tussen fasenlogs; dit staat wel op de wensenlijst.

## Synchroniseren van fasenlogs

Lees voor een goed begrip van deze functionaliteit eerst het artikel over [documenten beheer binnen YAVV](https://www.codingconnected.eu/yavvwiki/algemeen/documentenbeheer-in-yavv/).

In YAVV is het mogelijk twee fasenlogs in de tijd en/of qua layout te synchroniseren. Synchroon in de tijd betekent dat bij schuiven in de tijd in de ene fasenlog, de andere mee schuif, al dan niet met een bepaalde offset. Synchroon qua layout betekent dat opties zoals wel/niet weergeven van GUS of WUS en zoom niveau tussen de fasenlogs worden gesynchroniseerd.

### Synchronisatie fasenlog: uitgangspunten

De volgende uitgangspunten zijn van belang bij het werken met synchronisatie tussen fasenlogs:

- De synchronisatie verloopt altijd van één fasenlog, naar één fasenlog.
- Wanneer bij document 1 wordt ingesteld dat met document 2 wordt gesynchroniseerd, betekent dat wanneer van document 2 naar document wordt gesynchroniseerd. Ofwel, bij scrollen in document 2, scrollt doucment 1 mee.
- Het is mogelijk de synchronisatie in twee richtingen in te stellen, door dit bij beide documenten in te stellen.

#### Synchroniseren tijd

Open twee of meer documenten. Selecteer de fasenlog die aan een andere fasenlog gekoppeld moet worden. Let op: scrollen bij _die andere fasenlog_ zal dus zorgen dat deze log ook verschuift. Klap in het Documenten Beheer toolvenster “Document instellingen” uit, en vink “Synchroniseer” aan. Selecteer nu bij “Synchroniseer met” het document waarmee gesynchroniseerd moet worden, en selecteer vervolgens “Fasenlog tijd synchroniseren” aan.

Middels “Fasenlog offset” kan de offset van deze fasenlog ten opzichte van die waarnaar wordt gekeken worden geregeld. Dit is een waarde in seconden, die ook negatief kan zijn, en een fractie kan hebben. Let op: wordt ook een synchronisatie de andere kant op ingesteld, dan geldt _het verschil_ tussen de twee offset waarden als uiteindelijke verschilwaarde.

#### Synchroniseren weergave

Volg de stappen zoals bij synchroniseren tijd. Vink aan het eind “Fasenlog weergave synchroniseren” aan.
