---
title: "YAVC: bewaking dataverzameling"
date: 2020-09-09
---

## Achtergrond en uitgangspunten

Binnen YAVC wordt VLOG data verzameld en opgeslagen: dit is (vooralsnog) de voornaamste databron, en dit is om die reden een cruciaal systeemonderdeel. Zonder data kan er geen fasenlog worden getoond, en niets worden geanalyseerd. Een goede omgang met en rapportage omtrent fouten in de dataverzameling is daarom van cruciaal belang.

Bij dataverzameling geldt als uitgangspunt voor omgang met fouten:

> Zodra het stilvallen van de dataverzameling de integriteit van de analyse in gevaar brengt, moet YAVC hierover een melding (kunnen) afgeven.

In de praktijk betekent dit dus dat zodra er sprake is van het gevaar op permanent dataverlies, de centrale in staat moet zijn hier melding van de maken.

### Aanpak bepalen gevaar op dataverlies

YAVC kan data verzameling op een aantal manieren:

- Streaming VLOG:
    - direct vanaf de automaat, of
    - indirect vanaf een service die de VLOG stream beluisterd en verder distribueert
- File based VLOG:
    - ftp
    - sftp
    - lokaal benaderbare map die wordtr doorzocht op nieuwe aanwezig bestanden

Afhankelijk van het type dataverzameling is er meer of minder snel sprake van een urgente situatie wanneer er geen data binnen komt:

- Streaming VLOG:
    - Gezien de aard van streaming VLOG ontstaat er een gat in de data zodra de verbinding wordt onderbroken. Ook een kortstondige onderbreking veroorzaakt direct dataverlies.
    - Een sporadisch gat in de data van 5 minuten hoeft niet altijd direct een 'gevaar' op te leveren, en is vaak onvermijdelijk omdat bijvoorbeeld draadloze verrbindingen vroeg of laat een keer uitvallen
- Filebased VLOG:
    - Bij filebased verzamelen wordt er op de automaat een buffer bijgehouden van VLOG data. De lengte van deze buffer verschilt qua tijdsduur, omdat deze doorgaans een bepaalde grootte heeft qua bytes. Hoe omvangrijker de data (meer items, meer berichten) hoe sneller de buffer vol is, en oude de data dus verwijderd moet worden.
    - Normaal gesproken zijn altijd enkele uren aan data op de VRI aanwezig
    - Een complicerende factor bij filebased VLOG is dat de binnenkomende data altijd achter loopt op de actuele tijd. De mate waarin dit zo is verrschilt sterk per VRI: van 5 minuten tot meer dan een uur.

## Bepalen urgentieniveau van fouten in de dataverzameling

Om op de juiste/gewenste momenten en in de juiste situatie melding te kunnen maken moet het juist urgentieniveau kunnen worden bepaald. De volgende niveau's worden onderscheiden:

- Laag - geen direct gevaar op dataverlies; er is een fout opgetreden, maar directe actie is niet vereisd
- Middel - geen direct gevaar op dataverlies; er zijn een of meer fout opgetreden, actie wordt aangeraden
- Hoog - grote waarschijnlijkheid op permanent dataverlies; actie nodig
- Acuut - acuut dataverlies

Per type dataverzameling wordt anders invulling gegeven aan het bepalen van het niveau. Uitgangspunt is dat een sporadisch verlies van weinig data lage urgentie krijgt, en vaak terugkerend dataverlies, of dataverlies over langere tijd, een hoge urgentie krijgt. Hierbij gelden de volgende uitgangspunten:

- Afhankelijk van het type dataverzameling en de situatie, wordt het urgentieniveau periodiek of acuut bepaald
    - Periodiek bepalen van foutmeldingen wordt herhaald met een instelbare frequentie; default elke 15 minuten.
- Streaming VLOG:
    - Dataverzameling staat stil: afhankelijk van de duur van de stilstand wordt de urgentie bepaald:
        - <= 5 minuten: laag
        - <= 10 minuten: middel
        - <= 15 minuten: hoog
        - \> 15 minuten: acuut
        - De urgentie voor deze situatie wordt bepaald vooraf aan het leggen van een verbinding met een automaat; indien de verbinding wegvalt wordt dit zo steeds opnieuw gedaan bij het herstarten van de verbinding.
    - Dataverzameling bevat gaten: afhankelijk van de dekking over de afgelopen 24 uur wordt de urgentie bepaald:
        - \>= 99%: geen melding
        - \>= 95%: laag
        - 95 - 85%: middel
        - 85 - 75%: hoog
        - < 75%: accuut
        - De urgentie voor deze situatie wordt periodiek bepaald
- Filebased VLOG:
    - Maatgevend voor het bepalen van de urgentie van eventuele fouten zijn 2 factoren:
    - 1) De laatste succesvolle poging data op te halen:
        - <= 30 min. geleden: geen melding
        - 30 - 45 min. geleden: laag
        - 45 - 60 min. geleden: middel
        - 60 - 120 min. geleden: hoog
        - \> 120 min. geleden: accuut
    - 2) De dekking over de afgelopen 24 uur; gerekend vanaf de laatst beschikbare data
    - De hoogste van deze 2 geldt als maatgevend voor het urgentieniveau

## Versturen en verwerken van meldingen

Wanneer is bepaald dat sprake is van een fout, zal dit al naar gelang het urgentieniveau aanleiding zijn voor het versturen van een melding, of weergeven van de fout in de client.

- Administator gebruikers kunnen instellen wie precies welke meldingen moet ontvangen.
- Aangemaakte (al dan niet verstuurde) meldingen worden opgeslagen in de database van YAVC
- Naast afgeven van meldingen kunnen geconstateerde fouten en hun urgentie ook worden weergegeven in de client. Zo is bv. mogelijk alleen bij het niveau "acuut" een email te laten versturen, maar reeds bij niveau "middel" in de client een kruispunt als problematisch aan te merken.
- In de client is het mogelijk een melding als "afgedaan" aan te merken.
- Bepalen van welke meldingen aan een gebruiker verstuurd moeten worden gebeurt door te kijken of een gebruiker bepaalde meldingen moet ontvangen, en zo ja, vanaf welke niveau

### Beperken aantal meldingen

Met name bij meldingen via de mail moet worden voorkomen dat deze in aantal te omvangrijk worden. Hiertoe zijn een aantal voorwaarden en uitgangspunten gespecificeerd:

- Status van meldingen:
    - Meldingen kunnen "actueel" zijn of "niet actueel". Actueel houdt in dat de situatie momenteel nog van toepassing is. Niet actueel houdt in dat de betreffende situatie zich in het verleden voor deed en niet langer actief is.
    - Meldingen kunnen al dan zijn afgehandeld. Dit is tbv. weergave of verbergen in de client: afgehandelde meldingen worden default verborgen.
- Aanmaken/verzenden van meldingen:
    - Per kruispunt wordt éénmalig een melding aangemaakt en - indien van toepassing - verzonden naar gebruikers waarvoor dit is ingesteld.
    - Wanneer bij een check ergens een fout wordt geconstateerd, wordt gekeken of er reeds een melding van hetzelfde type in de database aanwezig is, die niet als "actueel" is aangemerkt.
        - Zo nee: aanmaken nieuwe melding, indien van toepassing versturen
        - Zo ja: melding informatie updaten.
    - Volgende meldingen voor dezelfde kruising veroorzaken geen nieuwe email of andere alert.
        - Tenzij: het niveau is gewijzigd, is nu hoger, eerder is geen melding verzonden, maar dat nu wel moet gebeuren. YAVC houdt hiertoe bij welke gebruikers een melding wel/niet hebben ontvangen.
- Verwerken van meldingen:
    - Tijdens de periodieke check wordt gekeken of evt. meldingen al dan niet actueel zijn. Indien meldingen niet langer actueel zijn kunnen ze worden afgehandeld.
    - Meldingen van niveau 'middel' of lager kunnen automatisch worden afgehandeld. Dit gebeurt indien tijdens de periodieke check geen fout meer wordt geconstateerd.
    - Meldingen van niveau 'hoog' of 'acuut' kunnen enkel handmatig als afgehandeld worden bestempeld. Hiermee wordt voorkomen dat een groot gat in de dataverzameling van enkele dagen geleden over het hoofd kan worden gezien.
        - Wel geldt: nadat een melding niet langer actueel is, kan een nieuwe melding zorgen voor een nieuwe alert.
- Bufferen van meldingen:
    - Om een stormvloed aan meldingen te voorkomen, worden deze gebufferd. Nieuw te versturen meldingen worden in een buffer gezet.
        - Acute meldingen blijven maximaal 5 minuten in de buffer staan
        - Overigen meldingen blijven maximaal 15 minuten in de buffer staat
        - Zodra voor de eerste melding de gestelde termijn afloopt worden alle meldingen in de buffer verzonden, in één bericht
