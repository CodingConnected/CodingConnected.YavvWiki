---
title: "Rollen en rechten in YAVC"
date: 2021-04-13
---

In YAVC wordt gewerkt met gebruikers. Elke gebruiker heeft een bepaalde rol, en die rol bepaalt de rechten van de gebruiker. Bij rechten gaat het om toegang (of juist niet) tot bepaalde data en het al dan niet hebben van de mogelijkheid data te bewerken en/of te verwijderen. In de praktijk gaat dit dus met name om het al dan niet hebben van de mogelijkheid het systeem te configureren.

De rol heeft invloed op twee niveau's:

- De user interface van de client: al naar gelang de rol van de aangemelde gebruiker worden bepaalde elementen in de applicatie wel/niet getoond of zijn die wel/niet beschikbaar.
- Op het niveau van de toegang tot de data (API): hier is middels moderne standaarden geregeld dat enkel geauthenticeerde gebruikers met de juiste rol toegang hebben tot inzien of bewerken van de juiste data. Zelfs wanneer een gebruiker de UI weet te omzeilen is de zekerheid dus gewaarborgd.

## Rollen

De volgende rollen zijn beschikbaar:

- user - reguliere gebruiker met alleen-lezen toegang tot alle data, met uitzondering van:
    - connectie instellingen (geen rechten)
    - archivering instellingen (geen rechten)
    - yavc systeem instellingen (geen rechten)
    - gebruikersdata (uitsluitend lezen en schrijven voor eigen account)
- admin - Gebruiker met rechten zoals nodig voor het dagelijks beheer van YAVC:
    - rechten zoals bij 'user', met aanvullend:
    - connectie instellingen (alleen lezen)
    - archivering instellingen (alleen lezen)
    - analyse configuratie & analyse data (lezen en schrijven)
        - deze gebruiker kan dus analyse configuraties wijzigen, dit opslaan, en zo zorgen dat de analyse data wordt herberekend
- systemadmin - gebruiker met toegang tot alle data
    - toevoegen/verwijderen kruispunten incl. alle bijbehorende data
    - wijzigen instellingen en meta data kruispunten
    - toevoegen/verwijderen/wijzigen connectie configuraties
    - wijzigen systeem instellingen
    - verwijderen van VLOG data uit de database van YAVC

YAVC biedt zelf geen mogelijkheden voor het aanmaken en/of beheren van gebruikers en toedelen van rollen aan gebruikers. Dit wordt gedaan door een zogenaamde "identity provider" (IdP). De IdP kan bij de klant staan ("on premise") of elders. Bij de installatie van YAVC wordt bekeken wat hier het beste past en wordt dit ingeregeld.

## Toegang

Hieronder wordt voor de volledigheid nog per bron in YAVC weergegeven welke rol wel/geen toegang heeft

- analyse configuraties
    - user = lezen
    - admin = lezen+wijzigen
    - systemadmin = lezen+wijzigen+aanmaken+verwijderen
- beschikbaarheid vlog data, beschibaarheid filtering data, beschikbaarheid analyse data
    
    - user, admin = lezen
    
    - systemadmin = lezen+wijzigen+aanmaken+verwijdern
- archivering configuraties, connectie configuraties, errors, issues
    
    - user = geen toegang
    
    - admin = lezen
    - systemadmin = lezen+wijzigen+aanmaken+verwijderen
- gebruikersdata
- geïmporteerde bestanden, overige instellingen
    - user, admin = geen toegang
    - systemadmin = lezen+wijzigen+aanmaken+verwijderen
- vlog data, filtering data, analyse data
    - user, admin = lezen
        - merk op: admin heeft indirect de mogelijkheid filtering en analyse data te laten herberekenen wanneer een analyse configuratie wordt gewijzigd
    - systemadmin = lezen+wijzigen+aanmaken+verwijderen
