---
title: "YAVV portable wil niet starten"
date: 2021-01-08
---

## Het probleem

Met de portable versie van YAVV (de .zip file die kan worden uitgepakt in een map naar keuze) kan het voorkomen dat de applicatie na uitpakken niet wil starten.

De volgende fout treed dan vaak op:

```
Fout in YAVV (versie x.x.x.x).
Bron: Application.Current.DispatcherUnhandledException, in YAVV vx.x.x.x.
System.NotSupportedException: Er is een poging gedaan een assembly te laden vanuit een netwerklocatie.
```

De oorzaak van de fout is het feit dat de zip waaruit de applicatie komt van internet is gedownload. Op sommige systemen zorgt dit ervoor dat de uitgepakte applicatie als onbetrouwbaar wordt aangemerkt.

## De (waarschijnlijke) oplossing

Met een handmatige actie vóór het uitpakken kan dit worden verholpen:

1. Selecteer de zip in Windows verkenner
2. Open het context menu met een rechtermuisklik
3. Klik helemaal onderaan het context menu op "Eigenschappen"
4. In het tabblad "Algemeen" staat onderaan een kopje "Veiligheid" met een korte tekst die aangeeft dat de zip van elders komt. Daarnaast is een vinkje "Deblokkeren" of "Unblock". Vink dit aan, en klik dan op Toepassen of direct op OK.
5. Pak de zip nu opnieuw uit naar of in een eigen (lege) map en start YAVV.

Indien deze acties nodig zijn op een bepaald systeem, is dit iedere keer nodig nadat de applicatie opnieuw is gedownload. Door gebruik te maken van de setup kan dit worden voorkomen, die is namelijk digitaal ondertekend, wat bij een zip niet kan.
