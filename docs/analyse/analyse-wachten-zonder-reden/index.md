---
title: "Analyse: wachten zonder reden"
date: 2020-09-14
---

Bij wachten zonder reden gaat het om situaties waarin een weggebruiker moet wachten voor een rood licht, terwijl daar gezien de verkeerssituatie geen goede reden voor is. Dit wordt door YAVC/YAVV als volgt bepaald:

- Tijdens rood wordt start wachten geregistreerd op basis van koplussen of knoppen
- Tijdens groen wordt activiteit op de koplus genomen om voor conflicten van de betreffende richting het wachten te markeren als "met reden"
    - Hierbij geldt vanaf start groen een instelbare minimale tijd sowieso als "goede reden"
    - Voor voetgangers is apart een minimale (en vaste) tijd in te stellen die geldt als "goede reden"
    - Voor voetgangers is mogelijk in te stellen dat de groen hier voor conflicten altijd geldt als "goede reden" om te wachten
- Voor wachtende richtingen wordt voortdurend bekeken: is er recent, rekening houdend met de geel- en ontruimingstijd/intergroentijd, nog activiteit gezien op een conflict?
    - Zo ja: dan wacht de richting met een "goede reden"; was eerder sprake van wachten zonder reden, dan wordt dat op dit moment beëindigd
        - Hierbij geldt: het moet minimaal een instelbare tijd rood zijn, voordat sprake kan zijn van wachten zonder reden
    - Zo nee: dan is er sprake van wachten zonder reden
- Op start groen worden resultaten verzameld:
    - Alleen wachten-zonder-reden blokken langer dan een ingesteld minimum worden meegenomen
    - Er wordt enkel een resultaat weggeschreven indien de totale tijd wachten-zonder-reden hoger is dan een instelbaar minimum

Gezien VLOG als databron en de omschreven aanpak gelden er enige beperkingen:

- Er wordt geen rekening gehouden met verkeersregelkundige situaties waardoor bepaalde richtingen "legitiem" niet realiseren, zoals gelijkstarten en andere synchronisaties
- Er wordt geen rekening gehouden met verkeersregelkundige situaties waardoor bepaalde richtingen extra groen krijgen anders dan door activiteit op de betreffende richting, zoals nalopen en andere interne koppelingen
- Voor voetgangers is de activiteit na start groen normaal gesproken (behoudens bv. bij aanwezigheid van radar) onbekend, en wordt daarom gebruik gemaakt van een instelbare vaste tijd vanaf startgroen die voor conflicten geldt als geldige reden om te wachten

De instellingen die beschikbaar zijn en hierboven zijn genoemd worden hieronder normaals opgesomd, met de default instelling tussen blokhaken:

- Minimale tijd wachten zonder reden \[2.0\]: blokjes wachten zonder reden korter dan deze tijd worden genegeerd
- Minimale totale tijd wachten zonder reden \[8.0\]: indien gedurende een roodfase in totaal minder dan deze tijd zonder reden is gewacht, wordt geen resultaat aangemaakt op start groen
- Minimale benutte groentijd \[4.0\]: gedurende deze tijd vanaf start groen geldt voor conflicten van een richting dat die ongeacht activiteit wachten mét reden
- Minimale benutte groentijd voertgangers \[4.0\]: idem apart voor voetgangers
- Controleer status regelen \[waar\]: indien niet waar, wordt tijdens status anders dan regelen niets gelogd
- Groen bij voetgangers geldt altijd als goede reden \[onwaar\]: indien waar, geldt de complete groentijd bij voetgangersrichtingen voor conflicten als goede reden om te wachten
