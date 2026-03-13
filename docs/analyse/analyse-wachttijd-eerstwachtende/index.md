---
title: "Analyse: wachttijd eerstwachtende"
date: 2020-09-14
---

Bij de wachttijd eerstwachtende wordt gekeken hoe lang het voorste voertuig in de wachtrij moet wachten tot startgroen. In YAVV/YAVC zijn er twee varianten van deze analyse:

- analyse uitsluitend op basis van externe signaalgroep status (WUS, de default)
- analyse waarbij wordt gekeken naar de interne signaalgroep status (GUS)

## Analyse met WUS

De wachttijd meting wordt gestart indien op een koplus of knop activiteit wordt gezien tijdens geel of rood van een signaalgroep. Daarbij geldt: 

- Indien de koplus weer afvalt wordt dit ook geregistreerd, en indien er niet langer voertuigen aanwezig zijn vervalt de meting.
- Een drukknopmelding wordt nooit gereset. **Let op:** op dit mometn is dus impliciet het uitgangspunt dat drukknopmeldingen tijdens geel zorgen voor een aanvraag die nooit wordt teruggenomen. Neem contact op indien dit voor u een probleem vormt.

Op start groen wordt een eventueel lopende meting weggeschreven. De meting van activiteit wordt gereset, en pas na start detectie van een betrokken detector of knop kan de meting weer gaan lopen.

Deze opzet zorgt ervoor dat alleen bij werkelijke activiteit op een richting, er ook een wachttijd gemeten wordt. Meeaanvragen hebben zo bijvoorbeeld geen invloed.

## Analyse met GUS

De analyse op basis van interne signaalgroep status verloopt net als die op basis van de interne status door te kijken naar activiteit op een richting. Aanvullend wordt hier echter gekeken naar het opstaan van "A", ofwel de richting moet een aanvraag hebben, anders wordt niet gemeten.

Daarnaast worden bij deze analyse naast koplussen en knoppen, ook lange en verweg lussen bekeken om de activiteit te bepalen. Ter informatie: dit verschil is een min of meer arbitraire keuze geweest, ontstaat in de loop van de ontwikkeling.
