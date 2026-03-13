---
title: "Analyse: detectie fouten"
date: 2020-09-09
---

Middels deze analyse kan een snel overzicht worden verkregen van waar en hoe lang er detectie fout op zijn getreden in de betreffende data. De analyse bepaalt de duur dat detectie in storing heeft gestaan volgens de automaat. De analyse kijkt dus uitsluitend naar logging van boven- en onder- en fluttergedrag en hardwarestoring.

Detectie fouten zijn in dit kader momenteel als volgt gedefinieerd:

- Alle detectie meldingen die in de VLOG data stroom als foutief zijn aangemerkt: ondergedrag, bovengedrag, fluttergedrag of hardware fout; dit zijn dus door de automaat als zodanig herkende en gemarkeerde fouten
- De [filtering van YAVV/YAVC zelf](../filtering-functionele-omschrijving/index.md) (volgorde filters, korte bezetting, etc.) wordt hierin **nog niet** meegenomen.

De resultaten van de analyse worden opgesplitst in blokken van 5 minuten. Staat een detector bijvoorbeeld gedurende 12 minuten continu in storing, dan zal dit drie resultaten opleveren. Dit maakt het mogelijk de duur dat detectoren in storing hebben gestaan over langere tijd te aggregeren. In de weergave kan de resolutie worden verlaagd, bijvoorbeeld naar totale tijdsduur in storing per uur.
