---
title: "Ik zie geen analyse data"
date: 2020-08-06
---

Soms lijkt het alsof YAVC geen analyses uitvoert, en komt er uitsluitend 0 terug als analyse resultaat. In de meeste gevallen is er sprake van een onvolledige of incorrecte configuratie, waardoor de analyse niet goed uitgevoerd kan worden.

Hier volgt een checklist:

- Is er een configuratie ingeladen? Indien bv alle fasen FC001, FC002 etc. heten, is dat hoogstwaarschijnlijk niet het geval. Zoek dan .cfg, .vlt of .vlc file op, en laad die in. Controleer vervolgens de configuratie van de kruising.
- Zijn de detectoren juist toegewezen? Controleer in het tabblad "Detectoren" of alle detectoren aan de juiste fase zijn toegewezen. Zonder kennis van welke detector bij welke fase hoort kunnen de meeste analyses niet worden uitgevoerd.
- Is van de detectoren het type juist ingesteld? Soms staan bv. alle detectoren op "Overige detector", omdat het type detector niet of onjuist in de configuratie zat.
- Bevat de data interne statussen voor signaalgroepen en uitgangen? Zo niet, dan moet dit (momenteel) voor sommige analyses worden ingesteld. Dit geldt momenteel voor de analyse "wachttijd eerstwachtende".
- Bevat de data (correcte) informatie omtrent de "status regelen"? Zo niet, dan moet dit voor sommige analyses worden ingesteld. Dit geldt momenteel voor "Wachten voor niets" en "Cyclustijd".

Levert de checklist geen soelaas? Gebruikers van YAVC en van YAVV pro kunnen [contact opnemen](https://www.codingconnected.eu/contact/), dan kijken we samen waar het probleem zit.
