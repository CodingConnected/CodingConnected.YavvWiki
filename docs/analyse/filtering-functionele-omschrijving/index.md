---
title: "Filtering: functionele omschrijving"
date: 2019-10-14
---

YAVV en YAVC bieden de mogelijkheid detectie data te valideren. In YAVV is dit een functionaliteit die moet worden ingeschakeld voor ingeladen data, waarna dit kan worden gevisualiseerd in de fasenlog, en naar wensen analyses op basis van gevalideerde data kunnen worden uitgevoerd. In YAVC worden analyses standaard uitgevoerd op basis van gevalideerde data. Ook in YAVC kan de validatie worden gevisualiseerd in de fasenlog.

Vailidatie gebeurt in principe als één geheel: validatie filters worden achtereenvolgens uitgevoerd op een data set, met als uitkomst één set aan gevalideerde berichten. Per bericht dat is aangemerkt als invalide is bekend welke filter het betreffende bericht heeft gemarkeerd. Een bericht dat door een bepaalde filter als invalide wordt aangemerkt, speelt in navolgende filtering geen rol meer: bijvoorbeeld, wanneer een hardware storing geldt, wordt voor de betreffende berichten niet meer gekeken naar kleine gaten, korte meldingen en/of volgorde.

De volgende validatie filters worden in YAVV/YAVC achtereenvolgens doorlopen en vormen tezamen het complete proces van detector data validatie:

1. Hardware fout filter - filtert obv fout meldingen uit de automaat

3. Flutter filter - filtert door te kijken naar een teveel aan opeenvolgende meldingen in een bepaalde periode (experimenteel: dit filter is default uitgeschakeld)

5. Kleine gaten filter - filtert zeer kleine hiaaten weg, plakt dus opeenvolgende meldingen aan elkaar

7. Korte melding filter - filtert te korte meldingen weg

9. Volgorde filter - filtert op basis van volgorde van achtereenvolgende detectoren

11. Omgekeerde volgorde filter - filtert op basis van volgorde van achtereenvolgende detectoren in omgekeerde richting

De filters worden in de genoemde volgorde doorlopen. In elke volgende stap worden reeds als invalide aangemerkte meldingen niet meer verder behandeld. Twee zeer korte, snel op elkaar volgende meldingen kunnen dus zijn samengevoegd, en zullen daardoor op basis van de 'Korte melding' filter niet meer worden weg gefilterd.

De filters worden hieronder nader functioneel toegelicht.

## Hardware fout filter

Alle detectie meldingen die in de VLOG data zelf als foutief zijn gemarkeerd (hardware error, boven-, onder- of fluttergedrag) worden in YAVV/YAVC 1 op 1 ook als invalide gemarkeerd. Daarbij geldt, dat een melding bezet die start gedurende een hardware storing, maar eindigt zonder storing, in zijn geheel als invalide wordt gezien.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

## Kleine gaten filter

De 'kleine gaten' filter merkt zeer kleine hiaaten aan als invalide. Dit filter geldt niet voor lange lussen en knoppen. Hoe klein een gat moet zijn om gedicht te worden is instelbaar. Default geldt dat er minimaal 0,3 seconde tussen twee meldingen moet zitten, en dus bezet meldingen die binnen 0,2 na de vorige volgen aan elkaar zullen worden geplakt.

Technisch gezien worden in dit geval dus de melding 'detector onbezet' van de eerste detector puls, en de melding 'detector bezet' van de te snel gevolgde volgdende puls als invalide aangemerkt, waardoor 'detector bezet' van de eerste en 'detector onbezet' van de tweede overblijven.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

- Minimale tijd tussen metingen \[0.3 sec.\]: komen opeenvolgende detector meldingen op kop- of verweg lusser korter na elkaar dan deze tijd , dan worden ze aan elkaar geplakt

## Korte meldingen filter

De 'korte meldingen' filter zoekt naar meldingen die korter duren dan een instelbare tijdsduur. Default is dit op 0,2 seconden ingesteld, en het is raadzaam deze default aan te houden om onterecht wegfilteren van data te voorkomen. Waarde hoger dan 0,2 seconden is de kans groot dat valide detector meldingen onterecht worden weg gefilterd.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

- Minimale bezettijd \[0.2 sec.\]: metingen die korter duren dan deze instelling worden weg gefilterd

## Volgorde filter

De volgorde filter zoekt voor opeenvolgende detectoren of een melding start detectie vooraf is gegaan door een melding start detectie op een voorliggende lus. Wordt die niet gevonden, dan wordt nog gekeken naar de lus daar weer voor, indien aanwezig. Indien óók daar niets wordt gevonden, wordt de melding (start en einde) als invalide aangemerkt.

Voor kop en lange lussen wordt gedurende groen, geel en een instelbare tijd na start rood (default 3,0 seconden), niet gefilterd, om te voorkomen dat er teveel berichten foutief als invalide worden aangemerkt. Opeenvolgende meldingen mogen maximaal een instelbare tijd (default 10,0 seconden) uit elkaar liggen, anders worden ze als onafhankelijk gezien.

Indien een meting langer duurt dan een grenswaarde (default 5,0 seconden) er niet wordt gefilterd. De gedachte hier, is dat dit bijvoorbeeld een voertuig betreft dat laat van rijstrook is gewisseld. Een langere bezet tijd duidt doorgaans op de aanwezigheid van daadwerkelijk wachtende voertuigen, ook wanneer voorgaande lussen niet bezet zijn geweest.

Voor koplussen geldt aanvullend: indien een voorgaandemelding op dezelfde lus niet is gefilterd op basis van volgorde en minder dan een instelbare tijd(default 3,0 seconden) voor de huidige melding ligt, wordt deze niet gefilterd. Hiermee wordt voorkomen dat in geval van een korte wachtrij, waarbij alleen de koplus en dus niet lange lus bezet is, meldingen na afrijden van het eerste voertuig worden weg gefilterd, omdat deze meer dan de ingestelde grenswaarden na de voorgaande lus liggen.

De volgorde filter werkt niet als een kettingreactie/heeft geen domino effect. Dat wil zeggen: stel de melding op de lange lus wordt aangemerkt als invalide omdat er op de verweg lus geen melding is gezien. De navolgende melding op de koplus wordt nu _niet_ als invalide aangemerkt, omdat er wél een voorgaande melding is gezien op de lange lus. De reden hiervoor is voorkomen van teveel - ongewenst - als invalide aangemerkte meldingen.

_Merk op:_ een aantal analyses heeft ook binnen de analyse de optie voor richting gevoelig meten (bijvoorbeeld: intensiteit, roodrijders). Indien dat is ingeschakeld wordt filtering op basis van volgorde in die analyses genegeerd.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

- Maximale tijd tussen metingen \[10,0 sec.\]: liggen metingen deze tijd of meer uit elkaar, dan worden ze als onafhankelijk gezien. Een koplus melding die dus minimaal 10 seconden later volgt dan einde detectie op de lange lus, zal worden gefilterd (in de afwezigheid van andere meldingen).

- Maximale bezettijd \[5,0 sec\]: alleen meldingen korter dan deze instelling mogen worden gefilterd op basis van volgorde.

- Minimale tijd na voorgaande melding \[3,0 sec.\]: is er tussen opeenvolgende koplus meldingen een hiaat korter dan deze instelling, en is de voorgaande melding niet gefilterd, dan wordt de huidige ook niet gefilterd

## Omgekeerde volgorde filter

Dit filter werkt als het volgorde filter, echter wordt hier teruggekeken. Bijvoorbeeld: wordt een melding op een koplus vooraf gegaan door een melding op een lange lus? Deze filter heeft doorgaans geen effect op koplus data en is daarom minder invloedrijk dan de andere filters. Immers: de meeste typen analyse maken vooral gebruik van koplus data.

Vooral bij overspraak, wanneer bv. wel de lange, maar niet de korte lus bezet raakt, of bij flutter-achtige storingen op verweg lussen, is dit filter effectief. Ook wanneer op een rijstrook (bijvoorbeeld de fietsers) meerdere koplussen aanwezig zijn die achter elkaar liggen kan dit filter actief worden.

_Merk op:_ een aantal analyses heeft ook binnen de analyse de optie voor richting gevoelig meten (bijvoorbeeld: intensiteit, roodrijders). Indien dat is ingeschakeld wordt filtering op basis van volgorde in die analyses genegeerd.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

- Maximale tijd tussen metingen \[10,0 sec.\]: liggen metingen deze tijd of meer uit elkaar, dan worden ze als onafhankelijk gezien. Een koplus melding die dus minimaal 10 seconden eerder volgt dan einde detectie op de lange lus, zal worden gefilterd (in de afwezigheid van andere meldingen).

## Flutter filter (experimenteel)

Het flutter filter kijkt naar een teveel aan metingen in te korte tijd. Wordt geconstateerd dat hiervan sprake is, dan worden de betreffende meldingen als groep weg gefilterd. In moderne automaten zit een dergelijk filter ook in de regeling, en biedt dit filter waarschijnlijk weinig meerwaarde.

_Opmerking vooraf_: bij significant veel fluttergedrag in data geldt als eerste advies: zoek vervangende data van betere kwaliteit, waarmee de gewenste analyse alsnog kan worden uitgevoerd. Dit zal altijd een beter resultaat leveren dan slechte data die wordt gefilterd. Is dergelijke data niet aanwezig, dan kan het flutter filter helpen de voor te bereiden om toch zinvolle analyses uit te kunnen voeren. _Controleer altijd de uitkomsten, en kijk bijvoorbeeld steekproefsgewijs in de fasenlog met visualisatie van de filtering_.

Fluttergedrag is zeer lastig om goed te filteren, zonder daarmee ook veel goede meldingen onterecht als foutief aan te merken. Een blik op de fasenlog is voor een verkeersregelkundige vaak voldoende om fluttergedrag te herkennen, maar technisch gezien is dit beduidend complexer. Er geldt:

- Het filter heeft een beperkt toepassingsbereik; verwacht dus niet dat alle visueel herkenbare vormen van fluttergedrag worden weg gefilterd bij inschakelen van dit filter!

- Het filter werkt het beste bij extreem geflutter, met zeer veel korte meldingen. In die gevallen geeft dit filter een beter beeld dan de andere filters

- Bij minder extreem flutteren, bv. een lus die elke 2-10 seconden zomaar op komt, is dit veel lastiger. Want: markeren van dergelijke meldingen heeft als 'bijwerking' dat je al snel ook correcte meldingen markeert, vooral tijdens drukke perioden. Het volgorde filter zal dan beter werken, maar ook dan geldt dat dit type foutieve meldingen weerbarstig blijft.

Het flutter filter houdt van afzonderlijke detectoren bij hoe vaak deze bezet zijn geweest. Zijn er over een aaneengesloten periode (default: 15,0 seconden) meer dan een ingesteld aantal meldingen gezien (voor een koplus bv. default 12 of meer), dan worden die meldingen met terugwerkende kracht als invalide gemarkeerd. De periode is doorlopend, er wordt dus bij elke volgende melding het aantal ingestelde seconden terug gekeken om te bepalen of er fluttergedrag is gezien.

Dit filter heeft de volgende instellingen \[defaults in blokhaken\]:

- Toepassen filter \[aan\]: in- of uitschakelen van dit filter

- Periode meting \[15,0 sec.\]: periode waarbinnen wordt gekeken of de ingestelde grenswaarde voor aantal meldingen wordt overschreden

- Koplus/verweg lus grenswaarde aantal \[12\]: grenswaarde aantal meldingen binnen de tijdsperiode voor kop- en verweg lussen

- Lange lus grenswaarde aantal \[10\]: grenswaarde aantal meldingen binnen de tijdsperiode voor lange lussen

- Knop grenswaarde aantal \[15\]: grenswaarde aantal meldingen binnen de tijdsperiode voor knoppen

## Praktisch nut en effect

De huidige implementatie van filtering in YAVV/YAVC is het resultaat van een uitgebreide zoektocht en afweging omtrent wat wel/niet te filteren. Filtering van VLOG data is **altijd** een balanceer-act:

- enerzijds voorkomen van teveel false-positives (wegfilteren van valide meldingen)

- anderzijds: teveel false negatives (niet wegfilteren van invalide data) is ook niet goed

Met name bij koplussen moet een onderschatting worden voorkomen; die is in de resultaten niet goed terug te zien en levert dan ongemerkt verkeerde data. **Daarom: als de keuze is tussen teveel of te weinig filteren is te weinig preferabel.** Immers: uitschieters met extreme getallen vallen sneller op (bv. 1000 roodrijders vanwege raar flutter-achtig gedrag) dan te lage waarden.

Bij de filtering zijn de koplussen het belangrijkst, want die zijn bepalend voor de meeste analyses. De impact van filtering is in de praktijk vooral groot als:

- koplussen met op/af meldingen in hardware/BG/OG/flutter storing staan in de VLOG data; dit wordt dan direct weggefilterd

- er veel is sprake van overspraak; dit zal YAVV er voor een groot deel uitfilteren, omdat dit doorgaans zorgt voor volgorde fouten

- er lussen zijn die zonder duidelijk aanleiding regelmatig zeer kort op en afvallen; dit wordt dan weggefilterd

- er koplussen zijn die niet goed reageren en daarom vaak op en afvallen met zeer korte hiaaten; meeldingen worden dan aaneen geplakt; waarbij opgemerkt dat het plakken vaak geen perfecte complete melding oplevert

- een koplus fluttert, maar niet zo dat er in de logging "echt" fluttergedrag komt; YAVV zal veel filteren, met name op basis van volgorde, maar niet alles.
    - merk op: dit is direct de lastigste vorm van detectie om te filteren, want zodra je "strenger" wordt, levert dat teveel false positives op.
    
    - het experimentele flutter filter biedt hier mogelijk uitkomst
