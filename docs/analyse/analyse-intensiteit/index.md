---
title: "Analyse: intensiteit"
date: 2020-04-24
---

De intensiteit wordt in YAVV bepaald door te kijken naar einde detectie meldingen voor koplussen. Wanneer filtering wordt toegepast worden meldingen die als invalide zijn gemerkt niet meegenomen in de tellingen (dit geldt voor alle analyses).

Instellingen voor de intensiteits analyse (defaults tussen blokhaken):

- Richtinggevoelig meten \[onwaar\]: indien waar, wordt bij opeenvolgende koplussen op dezelfde rijstrook richtinggevoelig gemeten. Dit vergt dan geen verdere instellingen, enkel twee koplussen op dezelfde rijstrook waarvoor qua afstanden is ingesteld dat die achter elkaar liggen. Er wordt gemeten of ED van de verste lus maximaal een instelbare tijd voor SD van de voorste lus ligt; wordt de max overschreden, dan wordt geen telling geregistreerd.
- Richtinggevoelig meten max. detector afstand \[5.0 m.\]: maximale afstand tussen koplussen op dezelfde strook om richtinggevoelig te meten. Indien twee opeenvolgende koplussen dus meer dan deze afstand uit elkaar liggen (gemeten als het verschil tussen de ingesteld waarde afstand-tot-stopstreep), wordt niet richtinggevoelig gementen. Dit is enkel beschikbaar en relevant indien richtinggevoelig meten is ingeschakeld.
- Richtinggevoelig meten max. volgtijd \[2.0\]: maximale tijd tussen ED van de verste lus en SD van de voorste lus in geval van richtinggevoelig meten. Dit is enkel beschikbaar en relevant indien richtinggevoelig meten is ingeschakeld.

De data wordt intern **per rijstrook** bepaald, in de tabellen en grafieken is dit ook beschikbaar. Onder "ruwe data" staat de data per rijstrook in de kolom "Extra 1", waarbij de aantallen per rijbaan gescheiden zijn met ;.
