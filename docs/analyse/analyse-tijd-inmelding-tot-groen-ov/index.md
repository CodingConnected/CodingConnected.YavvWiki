---
title: "Analyse: tijd inmelding tot groen OV"
date: 2021-06-30
---

In regelingen waar in DSI data aanwezig is, bijvoorbeeld van KAR meldingen en/of selectieve detectie lussen (zoals VECOM) is het mogelijk de tijdsduur te bepalen tussen de inmelding en het startgroen moment. Dit kan behulpzaam zijn bij het analyseren van de afwikkeling van het OV.

De inmelding wordt als volgt bepaald:

- Bij een DSI melding zonder lus nummer (selectieve detectie index 0) wordt gekeken naar het type bericht: in of uit
- Bij een DSI melding met een lus nummer (selectieve detectie index 1 of groter) wordt gekeken naar het type lus: in of uit
    - Het type lus wordt hierbij bepaald op basis van data uit de geladen configuratie.
    - Merk op: in de huidige versie van YAVV is het bewerken van deze configuratie data nog niet mogelijk
- De meting wordt uitsluitend gestart indien de DSI melding een correct signaalgroep nummer heeft, en uitsluitend tijdens status rood van de gerelateerde signaalgroep

Bij een uitmelding tijdens rood wordt de meting afgebroken.

_Merk op_: voor het juist functioneren van deze analyse is een correcte configuratie van de selectieve detectie nodig. Deze wordt, indien aanwezig, uitgelezen uit de VLOG config (.cfg, .vlc, etc.). Indien afwezig, zal ten minste het type lus juist ingesteld moet worden (in of uit).
