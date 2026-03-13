---
title: "Werkbladen en UI van YAVV"
date: 2020-04-03
---

YAVV is ontworpen om eenvoudig en intuïtief te zijn in het gebruik. Het ontwerp van de applicatie volgt veel gebruikte patronen in software, en is gericht op dagelijks gebruik door verkeerskundigen. Hieronder volgt een globale omschrijving van de opbouw en werking van de UI (user interface ofwel gebruikersinterface).

Tip: lees voor een goed begrip van de opbouw van YAVV ook over [het verschil tussen werkbladen en documenten](https://www.codingconnected.eu/yavvwiki/algemeen/documentenbeheer-in-yavv/) zoals binnen YAVV wordt gehanteerd.

## Opbouw gebruikersinterface

De opbouw van de gebruikersinterface van YAVV is als volgt:

- Bovenin het venster is een menu, met toegang tot applicatie-brede commando's
- Onder het menu is een toolbar: ook hier enige applicatie-brede commando's, en al naar gelang het geselecteerde werkblad toegang tot andere commando's en instellingen.
    - Let op: wanneer bijvoorbeeld een analyse tabblad open staat, maar óók een fasenlog, zullen de toolbar items behorende bij de fasenlog ook zichtbaar blijven. Dit is, omdat de fasenlog ook náást het analyse tabblad geplaatst kan worden, dan geen focus heeft, maar wel zichtbaar is.
- Onder de toolbar bevindt zich het hoofd-venster: hier verschijnen bij geopende data behorende werkbladen
- Het hoofd-venster biedt ook plek aan tool-vensters: dit betreft bijvoorbeeld de ingebouwde File browser en het Documentenoverzicht. Tool vensters kunnen - net als werkbladen - naar wens in het hoofd-venster worden geplaceerd
- Onderaan het vester bevindt zich een status bar met informatie over de geopende data

## Multi-venster omgeving

YAVV heeft een multi-venster omgeving die veel lijkt op die van bijvoorbeeld Microsoft Visual Studio. Bij [openen van VLOG data](https://www.codingconnected.eu/yavv/data-openen-met-yavv/) in YAVV, wordt default de fasenlog geopend; deze verschijnt als tabblad in het hoofd-venster. Bij openen van andere data, of van bijvoorbeeld het analyse werkblad voor de reeds geopende data, wordt een volgende tabblad toegevoegd. De gebruiker kan tabbladen naar wens (her)schikken:

- Middels klik + slepen op de naam van het tabblad kan dit uit het hoofd venster worden gesleept
- Tijdens slepen van een tabblad of zwevend venster is een element zichtbaar in het hoofdvenster: door met de muis op dit element te bewegen kan het betreffende venster naar wens op/naast/boven/onder andere venster(s) worden geplaceerd
- Op deze wijze kan bijvoorbeeld de fasenlog worden weergegeven naast of boven/onder analyse uitkomsten van de betreffende VLOG data
- Ook tool vensters kunnen naar wens worden geplaceerd
- Wanneer tool vensters aan zijkant van het venster staan, is er de mogelijkheid middels de knop met de punaise, te kiezen voor het automatisch inklappen van het venster
- Wanneer de muis op het gebied tussen twee aangrenzende werkbladen staat (die dus naast/boven elkaar zijn geplaatst) veranderd de muiswijzer in een pijl die twee kanten op wijst; klikken + slepen zorgt nu voor veranderen van de grootte van de betreffende vensters

## Werkbladen in YAVV

Bij openen van nieuwe data wordt default een fasenlog weergegeven. Middels de knoppen bij "Tabs" op de toolbar kunnen aanvullende werkbladen worden geopend. Hieronder volgt een beknopte omschrijving van de beschikbare werkbladen:

- Fasenlog: weergave van het verloop van het regelproces - zowel intern (regelapplicatie) als exterrn (zichtbaar op straat) - in de tijd
- Analyse: weergave van de uitkomsten van analyses op de betreffende data; dit kan enkel goed functioneren bij een juiste configuratie
- Configuratie: hier kunnen naam en overige instellingen van in de regeling aanwezige elementen worden ingesteld; tevens zijn instellingen voor filters en analyses beschikbaar
- DSI: weergave in een lijst en op kaart van in de VLOG data aanwezige DSI berichten

YAVV heeft tevens werkbladen los van VLOG data:

- Instellingen YAVV: beschikbaar via het menu Help > Instellingen YAVV; hierin kunnen instellingen die voor de gehele applicatie gelden worden weergegven en ingesteld
