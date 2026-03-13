---
title: "Evaluatie: indicatoren"
date: 2023-03-29
---

Dit artikel omschrijft de beschikbare verkeerskundige indicatoren binnen de evalautie tooling van YAVV/YAVC. Voor meer informatie over deze module, zie [hier](../yavv-yavc-evaluatie-introductie/index.md).

Bij het uitvoeren van een evaluatie wordt verkeerskundige data omgerekend naar rapportcijfers. De verkeerskunige data betreft hier niet altijd 1 op 1 de data die binnen YAVV/YAVC zichtbaar is bij de analyse. Welke indicatoren beschikbaar zijn, en wat deze precies inhouden, wordt hieronder toegelicht.

## Aandachtspunten

_Let op!_ Bij zeer weinig metingen en/of zeer weinig voertuigen hebben de afzonderlijke metingen al snel veel invloed. Bij opvallend hoge of lage cijfers, of een zeer wisselend beeld, kan dit een oorzaak zijn. Dit punt geldt voor alle indicatoren. Bijvoorbeeld bij gemiddeld wachttijd eerstwachtende kan een enkele relatief lange wachttijd veel invloed hebben op het gemiddelde, als er slecht een paar metingen zijn. Of bij percentage roodrijders kan, bij zeer lage intensiteiten, een enkele roodrijder al zorgen voor een zeer hoog percentage roodrijders.

## Gemiddelde wachttijd eerstwachtende

Gegeven een bepaalde evaluatie periode, wordt hier de totale gemeten wachttijd eerstwachtende - dus over de complete tijdsperiode - voor een signaalgroep gedeeld op het aantal metingen. Bijvoorbeeld: stel signaalgroep 1 wacht tussen 8 en 9 uur 3 keer, namelijk resp. 10, 20 en 30 seconden, dan zal de waarde hier dus zijn (10+20+30)/3=20.

## Stopkans

Hier wordt de stopkans berekend op basis van data voor de complete periode. Merk op: dit is niet dezelfde waarde als wanneer je analyse resultaten op zou tellen en delen door het aantal resultaten. Gezien de aard van deze analyse (resultaten zijn al een soort rekenkundig gemiddelde) moet de waarde veeleer voor de complete periode worden herberekend.

Deze indicator is niet beschikbaar voor voetgangers.

## Percentage roodrijders / diepgeelrijders

Bij deze twee indicatoren wordt het gemeten aantal roodrijders/diepgeelrijders voor de complete tijdsperiode gedeeld op de totale gemeten intensiteit voor die periode. Zo wordt het percentage verkregen.

Deze indicator is niet beschikbaar voor voetgangers.

## Overstaan

Bij overstaan wordt het aantal realisaties met overstaan gedurende de complete tijdsperiode afgezet tegen het totaal aantal realisaties. Dit resulteert in een percentage dat de basis vormt voor de vertaling naar een rapportcijfer.

Deze indicator is niet beschikbaar voor voetgangers.

## Wachten zonder reden

Bij wachten zonder reden wordt de totale gemeten wachten-zonder-reden tijd bepaald voor de complete tijdsperiode. Deze wordt gedeeld op het aantal realisaties, resulterend in een gemiddelde waarde voor de tijd wachten-zonder-reden per realisatie.

## Gemiddelde wachttijd / gemiddelde wachttijd fiets

Voor deze indicator wordt voor gemotoriseerd verkeer de totale waarde van voertuigverliesuren voor de tijdsperiode gedeeld op het gemeten aantal voertuigen, waarmee een gemiddelde wachttijd per voertuig wordt bepaald. Voor fietsers geldt indirect hetzelfde, echter geeft hier de analyse reeds direct gemiddelde verliestijd als resultaat (wel moet de waarde gezien de aard van de analyse worden herberekend voor de complete tijdsperiode). De resulterende waarde (in seconden) vormt de basis voor de bepaling van het rapportcijfer voor een signaalgroep voor de betreffende periode.

Deze indicator is niet beschikbaar voor voetgangers.

## Tijd inmelding tot startgroen

Bij deze indicator wordt - net als bij gemiddelde wachttijd eerstwachtende - de gemiddelde waarde bepaald voor de tijdsperiode voor de analyse DSI-inmelding tot startgroen. Dit functioneert dus uitsluitend indien er DSI data is voor een bepaalde signaalgroep; anders zal er altijd een 10 worgen berekend.

Deze indicator is niet beschikbaar voor voetgangers en fietsers.
