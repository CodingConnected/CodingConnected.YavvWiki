---
title: "Verpakken YAVV/YAVC-client voor Citrix"
date: 2022-03-24
---

Zowel voor YAVV als voor YAVC-client zijn .msi files beschikbaar (Microsoft Installer). Deze vormen normaliter de basis voor de packaging voor Citrix. De .msi files zijn altijd digitaal ondertekend door CodingConnected. Hieronder worden enige details genoemd voor beide applicaties die relevant zijn bij de packaging voor Citrix.

## Packaging YAVV voor Citrix

Voor YAVV geldt het volgende:

- YAVV is een 64 bits applicatie.
- De applicatie wordt default geïnstalleerd in C:\\Program Files\\YAVV, dit is tijdens de installatie procedure instelbaar. Een 'silent install' is ook mogelijk.
- Tijdens installatie is geen licentie nodig.
- De applicatie slaat enige data op in de Roaming map, daarin maakt de applicatie een map aan met de naam YAVV (doorgaans is dat dan dus C:\\Users\\<username>\\AppData\\Roaming\\YAVV, waarbij de naam van de map in de Nederlandse versie van Windows 'Gebruikers' is). _Deze data moet worden behouden_ tussen afzonderlijke Citrix sessies, anders verliest de gebruiker eigen instellingen.
- Voor gebruik van de volledige versie van YAVV is een licentie nodig. Deze ontvangt u van CodingConnected. De eindgebruiker kan deze handmatig installeren, maar het is beter wanneer tijdens deployment de licentie mee komt:
    - Hernoem de ontvangen licentie naar "defaultsecret.lic"
    - Plaats dit bestand in de map "Data" in de applicatie map
    - Dus bv.: C:\\Program Files\\YAVV\\Data\\defaultsecret.lic
    - Het evt. bestaande bestand moet worden overschreven
- Dezelfde opzet is mogelijk voor default instellingen: indien uw organisatie eigen default instellingen heeft voor YAVV, kan tijdens deployment het bestand "defaultsettings.json" in de map Data worden overschreven door de eigen versie. Dit is uiteindelijk enkel relevant voor nieuwe gebruikers, want voor bestaande gebruikers worden de settings uit de map Roaming genomen. Om dit toe te passen:
    
    - Plaats het eigen "defaultsettings.json" bestand in de map "Data" in de applicatie map
    - Dus bv.: C:\\Program Files\\YAVV\\Data\\defaultsettings.json
    
    - Het evt. bestaande bestand moet worden overschreven
    - Dit is bv. handig om te voorkomen dat gebruikers binnen Citrix een melding krijgen over een nieuwe versie, die ze sowieso niet kunnen installeren. In de eigen defaults kan deze check worden uitgeschakeld.

## Packaging YAVC-client voor Citrix

Voor YAVC-client geldt het volgende:

- YAVC-client is momenteel een 32 bits applicatie
- De applicatie wordt default geïnstalleerd in C:\\Program Files (x86)\\YAVC client; dit is tijdens de installatie procedure instelbaar. Een 'silent install' is ook mogelijk.
- Tijdens installatie is geen licentie nodig.
- De applicatie slaat enige data op in de Roaming map, daarin maakt de applicatie een map aan met de naam YAVC (doorgaans is dat dan dus C:\\Users\\<username>\\AppData\\Roaming\\YAVC, waarbij de naam van de map in de Nederlandse versie van Windows 'Gebruikers' is). _Deze data moet worden behouden_ tussen afzonderlijke Citrix sessies, anders verliest de gebruiker lokale instellingen.
- YAVC-client heeft voor correct functioneren een verbinding nodig met:
    - Een identity provider (Idp) waarin YAVC is geconfigureerd (bijv. AzureAD, ADFS, Auth0, etc.)
    - De client-API van YAVC, die de client voorziet van de benodigde data
    - Een evt. firewall moet dus correct zijn ingesteld zodat deze beide services bereikbaar zijn
- De client moet zowel van de IdP als de client-API weten waar die bereikbaar zijn; hiervoor is een configuratie bestand nodig dat CodingConnected aanlevert. De eindgebruiker kan dit bestand zelf laden, fraaier is echter wanneer dit voor Citrix mee wordt verpakt:
    
    - Hernoem de ontvangen configuratie naar "defaultconnection.json"
    
    - Plaats dit bestand in de map "Data" in de applicatie map
    - Dus bv.: C:\\Program Files\\YAVC client\\Data\\defaultconnection.json
    - Het evt. bestaande bestand moet worden overschreven
