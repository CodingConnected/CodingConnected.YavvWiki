---
title: "Data openen met YAVV"
date: 2020-04-03
---

YAVV is een VLOG-viewer, en dus bedoeld voor het openen, weergeven en analyseren van VLOG data. VLOG is een protocol voor het loggen van data uit verkeersregelautomaten (VRI's): zie [hier](http://www.v-log.nl/) voor meer informatie en [hier](https://www.ivera.nl/downloads) om het protocol te downloaden.

## Waar haal ik VLOG data vandaan?

VLOG data wordt aangemaakt door daarvoor geconfigureerde VRI's. Een VRI kan de VLOG data lokaal wegschrijven op schijf en tijdelijk opslaan, en/of via TCP ontsluiten als "streaming" data. In het eerste geval kan de data middels ftp of sftp worden opgehaald; doorgaans is data van de afgelopen 8-12 uur beschikbaar in de VRI. In het tweede geval moet een TCP verbinding worden opgezet en continu op staan om de data te ontvangen; vervolgens moet deze worden opgeslagen in VLOG bestanden.

## VLOG data openen met YAVV

Er zijn diverse manieren om VLOG data in YAVV te openen:

- Via het menu Bestand > Open kunnen 1 of meer bestanden worden geselecteerd

- Idem middels sneltoets Control + O

- Idem middels de knop "Openen VLOG bestanden" op de toolbar

- Door bestanden op het venster van YAVV te slepen, bijvoorbeeld vanuit Windows Verkenner

- Indien de exectuable YAVV.exe verbonden is met de .vlg en/of .vlog extensie: door dubbel klikken of enter toets op een VLOG bestand in bijvoorbeeld Windows Verkenner. _Let op: dit werkt slechts voor één bestand tegelijk, bij meerdere bestanden worden meerdere YAVV vensters geopend._

## Geopende bestanden afsluiten

- Middels een klik op de 'X' naast de naam van het werkblad kan het werkblad worden afgesloten; voor 'zwevende' werkbladen bevindt de 'X' zich zoals gebruikelijk in Windows in de rechter bovenhoek

- Idem middels sneltoets Control + W of Control + F4 (dit werkt niet voor werkbladen die los zijn gehaald van de hoofd applicatie)

- Een document (één of meer als geheel geopende bestanden) wordt afgesloten (en verdwijnt uit het Documenten Overzicht) wanneer alle daarmee verbonden werkbladen zijn gesloten: de fasenlog, en evt. het analyse, configuratie en/of DSI werkblad
