---
title: "Omgang met configuraties in YAVC"
date: 2020-05-28
---

Bij VLOG data hoort een configuratie. Zonder configuratie is bijvoorbeeld onbekend welk voertuigtype een bepaalde signaalgroep heeft, welke lus welk type heeft, bij welke signaalgroep die hoort, en waar die precies ligt, etc. Die type informatie is echter noodzakelijk om de data correct te kunnen visualiseren in de fasenlog, en correct filtering en analyses uit te kunnen voeren.

Dit artikel omschrijft de manier waarop binnen YAVC (grotendeels automatisch) wordt omgegaan met configuraties. Zie voor concrete analyse instellingen per kruising [dit artikel](../kruispunten-configureren-in-yavc/index.md).

## Samenvatting:

- YAVC maakt automatisch configuraties aan voor verzamelde VLOG data: zo ontstaat een lijst met opeenvolgende configuraties, die elk geldig zijn voor een bepaald tijdvak
- Automatisch gegenereerde configuraties zijn _niet gevalideerd_; pas na validatie door de gebruiker start filtering en analyse van de data
- Het is mogelijk configuraties te bewerken, ook na validatie; wel moet dan (desgewenst) filtering en analyse data opnieuw worden doorgerekend

## Algemene omgang met configuraties

YAVC verzorgt het aanmaken en configureren van kruispunten zoveel mogelijk geautomatiseerd. Na configuratie van een kruispunt in YAVC wordt automatisch gestart met verzameling van VLOG data (indien ingeschakeld). Bij indexatie van de eerste VLOG data maakt YAVC een eerste configuratie aan.

Betreft het VLOG versie 3, dan wordt de VLOG configuratie (beter bekend als CFG of VLT bestand) elke uur op het hele uur met de VLOG data mee gestuurd. YAVC gebruikt dit om automatisch de namen van elementen in te laden, en met gebruik van default waarden een voorzet te doen voor welke detector bij welke signaalgroep hoort, waar welke detector ligt en hoe lang die is.

### Validatie van configuraties

Een automatisch aangemaakte configuratie is aanvankelijk _niet gevalideerd_. YAVC zal daarom nog geen filtering en analyse uit kunnen voeren. Pas na validatie van de configuratie door de gebruiker zal YAVC (met terugwerkende kracht vanaf de start van de periode waarvoor de configuratie geldig is) starten met validatie en analyse van data. Het kan vervolgens afhankelijk van de hoeveelheid te verwerken data enige tijd duren voor alle analyse resultaten beschikbaar zijn.

### Herberekenen: ja of nee?

Omdat YAVC analyse data continu doorrekend, is het bij het wijzigen van een configuratie nodig de filtering/analyse data te herberekenen om te zorgen dat de in de database aanwezig data weer overeenstemt met de configuratie. Daarbij is soms de vraag: _is dit eigenlijk wel nodig?_

Zeker bij veel data kan het herberekenen geruim tijd in beslag nemen. Het rekenen zelf kost relatief weinig tijd, het ophalen van de VLOG data om mee te rekenen kost echter ook enige tijd. En vooral geldt: er veel database operaties mee gemoeid om de nieuwe data op te slaan en bij te houden wat reeds wel/niet is bijgewerkt. Vooral dit type operaties kost relatief veel tijd.

Daarom enige tips omtrent het al dan niet herberekenen van data:

- Bij zeer veel data kan herbereken lang duren: bv. bij een jaar of meer aan data kan dit 12 uur of meer duren, al naar gelang de grootte van de kruising, de omvang van de brondata en het type systeem waar YAVC draait; in zo'n geval is de afweging: hoe belangrijk is het dat de wijziging wordt verwerkt in historische data?
- Koplussen zijn voor veel analyses allesbepalend: intensiteiten, roodrijders, vroegstarters, wachttijd eerstwachtend, etc. Wijzigt er dus wat op dit vlak, dan is herberekenen eigenlijk onontbeerlijk, want de eventueel reeds berekende data is waarschijnlijk foutief.
- Idem. voor wijziging van de ligging van detectie (rijstrook, afstand tot ss) waardoor de volgorde per rijstrook wijzigt: de eventueel reeds berekende data is waarschijnlijk incorrect, met mogelijk onbedoeld effect (met name qua filtering) op de data en daarmee op de uitkomst van analyses
- Niet alle wijzigingen aan een configuratie hebben effect op de filtering/analyse. Hieronder een overzicht van wijzigingen die _wel_ belangrijk zijn:
    - Signaalgroepen:
        - wijzigen aantal rijstroken
        - type
        - geeltijd (enkel voor [wachten zonder reden](../../analyse/analyse-wachten-zonder-reden/index.md))
    - Detectoren:
        - wijzigen signaalgroep
        - rijstrook
        - type
        - ligging: dit is enkel relevant wanneer daardoor de volgorde wijzigt, behalve voor de analyse "[gemiddelde wachttijd fiets](../../analyse/analyse-gemiddelde-wachttijd-fietsers/index.md)", waarbij de ligging van verweg detectie invloed heeft op de resultaten
    - Handmatige toedeling DSI: van belang voor de analyses OV inm. tot uitm. en OV inm. tot SG
    - Wijzigingen aan instellingen van een of meer filters: dit heeft invloed op álle data, want wijzigt mogelijk de feitelijke brondata zoals de analyses die te zien krijgen
    - Wijzigingen aan instellingen van een analyse: enkel van belang voor de betreffende analyse

_Toekomst:_ voor YAVC staat op de ontwikkellijst om intelligentie in te bouwen waarmee de (client) applicatie op basis van de wijzigingen zelf kan bepalen welke data wel/niet verwijderd hoeft te worden om de data gelijk te trekken met de configuratie.

## Geldigheid van configuraties & omgang met wijzigingen

Een regeling kan wijzigen, waarbij bijvoorbeeld een signaalgroep of detector wordt verwijderd of toegevoegd. Dit betekent dat er vanaf het moment van de wijziging een nieuwe configuratie moet gelden. VLOG configuraties hebben daarom altijd een bepaalde periode waarvoor ze geldig zijn. In YAVC geldt dat de laatste configuratie geen einddatum heeft: deze is dus geldig tot nader order.

In YAVC geldt dus:

- Een configuratie is altijd geldig _vanaf_ een bepaald moment
- Een configuratie is altijd geldig _tot_ een bepaald moment
- Er is dus een lijst met configuraties, die achtereenvolgens gelden voor een bepaald tijdvak
- De laatste configuratie heeft geen eind datum, en is daarmee altijd de 'huidige' configuratie: bij binnenkomst van nieuwe data wordt gekeken of die past bij de actieve configuratie

Tijdens de indexatie van nieuwe data voert YAVC een check uit om te kijken of de nieuwe data past bij de actieve configuratie. Hiertoe:

- Worden de aantallen signaalgroepen/detectoren/ingangen en uitgangen in de nieuwe data vergeleken met diezelfde aantallen in de actieve configuratie
- Bij VLOG3 wordt bij binnenkomst van de configuratie (normaliter komt op het hele uur de VLOG config ("CFG") mee met de data) gekeken of de naamgeving en rangering van elementen nog identiek is
    - Deze optie is uitschakelbaar bij de geävanceerde instellingen per kruispunt; dit is bijvoorbeeld relevant wanneer er handmatig elementen (bv. een signaalgroep) zijn toegevoegd aan een configuratie
- Is er een match, dan blijft de actieve configuratie gelden.
- Is er geen match, dan maakt YAVC een nieuwe configuratie aan. Hierbij worden zoveel mogelijk instellingen uit de geldende configuratie overgenomen in de nieuwe configuratie. Hier geldt wederom: deze is aanvankelijk _niet gevalideerd_.

Wordt een nieuwe configuratie aangemaakt, dan maakt YAVC een issue aan en verrstuurt aan gebruikers voor wie dit is ingesteld een alert. Het betreffende issue wordt automatisch gesloten zodra de configuratie is gevalideerd door een gebruiker.

## Handmatig configuraties toevoegen of verwijderen

Het is ook mogelijk handmatig configuraties toe te voegen. Hiermee kan bijvoorbeeld vóór een wijziging aan een regeling reeds de nieuwe configuratie worden ingericht en gevalideerd, zodat de filtering en analyse na de wijziging direct door kan lopen.

Let wel op:

- Het tijdstip vanaf wanneer de nieuwe configuratie van toepassing is moet in de toekomst worden gelegd; anders zal YAVC automatisch een nieuwe configuratie aanmaken voor data zoals die momenteel binnen komt
- Het tijdstip van de wijziging moet bekend zijn
    - Ligt dit uiteindelijk eerder dan ingesteld, dan zal YAVC momenteel een fout constateren: het "invoegen" van een nieuwe configuratie ergens midden in de lijst met opeenvolgende configuraties wordt nog niet ondersteund.
    - Ligt het moment uiteindelijk later, dan zal YAVC reeds zelf een (niet gevalideerde) configuratie aanmaken bij binnenkomst van de eerste data waarop de huidige configuratie niet meer van toepassing is
- Op de wensenlijst staat de mogelijkheid van het aanmaken van een reeds vooraf gevalideerde "kandidaat" configuratie: bij een geconstateerde wijziging kan YAVC dan nagaan of de kandidaat past bij de nieuwe data, en deze direct toepassen. Dan is het exacte moment van de wijziging niet meer van belang

Toevoegen van een configuratie kan _uitsluitend aan het einde_ van de lijst met configuraties. Dit geldt eveneens voor het verwijderen van configuraties en wijzigen van de datum vanaf wanneer een configuratie geldt: uitsluitend de laatste configuratie - die dus geen einddatum heeft en 'nu' geldt - kan worden verwijderd of geldigheidsduur worden gewijzigd. Wordt van de laatste configuratie de start datum gewijzigd, dan wijzigt de eind datum van voorlaatste configuratie automatisch mee.

Indien een configuratie wordt verwijderd, dan wordt de bijbehorende filtering en analyse data ook verwijderd. Wordt de start datum van de laatste configuratie gewijzigd, dan wordt alle data in de periode tussen de oude en de nieuwe start datum verwijderd.

## Instellingen bewerken en opslaan

Dit wordt uitgebreid omschreven in [dit artikel](../kruispunten-configureren-in-yavc/index.md).
