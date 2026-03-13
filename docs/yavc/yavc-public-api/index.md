---
title: "YAVC: public API"
date: 2021-03-15
---

YAVC komt met de mogelijkheid analyse data te ontsluiten via een publieke API. Publiek wil hier zeggen: beschikbaar indien de server waarop de API draait beschikbaar is. Vaak is dit dus enkel binnen een (al dan niet virtueel) privaat netwerk, waardoor de API dus alsnog is afgeschermd van de buitenwereld. Sowieso geldt dat een gebruiker (= een extern systeem) van de API zich moet authentiseren.

De "publieke" API draait afzonderlijk van de "client API" van YAVC. Vaak is deze laatste ook extern bereikbaar, echter kent deze API geen Swagger documentatie, en is enkel bedoeld voor data uitwisseling met de client applicatie van YAVC. De publieke API daarentegen is expliciet bedoeld om externe systemen toegang te verschaffen tot data van YAVC.

## Kenmerken API

De API van YAVC is opgebouwd volgende principes van REST. De belangrijkste consequenties hiervan zijn: er is geen 'status', elke aanroep van de API gebeurt afzonderlijk zonder relatie met andere aanroepen. Daarnaast is de data op te roepen via eenduidige endpoints en kan sprake zijn van caching van data.

De publieke API is bedoeld voor system-to-system data uitwisseling. Wordt hieronder gesproken over "gebruikers", dan wordt bedoeld: externe systemen die toegang nodig hebben tot data uit YAVC.

De API is uitsluitend benaderbaar na authenticatie van de client middels OAuth 2.0. Hiervoor is een identity provider (IdP) nodig waarmee, bijvoorbeeld middels client credentials, een access token kan worden opgehaald.

Technische kenmerken: de API is gemaakt met ASP.NET 8 en draait normaal gesproken achter een reverse proxy webserver. Het versiebeheer van de API verloopt via de http-headers.

Het is raadzaam enige voorzichtigheid te betrachten bij gebruik van de publieke API: zeer intensief gebruik (wanneer bv. meerdere gebruikers continu veel data op gaan vragen) zal de server belasten, alsook de database; dit kan de werking van YAVC negatief beïnvloeden. De API buffert geen data/gebruikt geen cache en zal dus bij elke call de database raadplegen. Bij regulier gebruik van de API, bv. voor periodiek ophalen van nieuwe analyse data, is van overbelasting evenwel geen sprake, ook niet wanneer het meerdere externe apps betreft. Wordt zeer intensief gebruik voorzien, dan is een proxy service die zorgt voor buffering/caching aan te bevelen.

## Authenticatie

De API kan pas worden bevraagd nadat is geauthentiseerd: voor het bevragen van de API is namelijk een Json Web Token (JWT) ofwel bearer token nodig die met elke API call moet worden meegestuurd. Het gehanteerde protocol heet OAuth 2.0, met gebruik van de client credentials flow. Zie [dit artikel](../yavc-public-api-authentication/index.md) voor details.

## Gebruik van de API

De API is voorzien van ingebakken documentatie middel "swagger", wat voldoet aan de OpenAPI standaard. De documentatie is na installatie benaderbaar via https://<server>:<poort>/swagger. De API is momenteel opgedeeld in drie delen, met elk een aantal endpoints (=mogelijkheden data op te vragen). Hieronder een zeer beknopt overzicht, zie voor details de swagger documentatie:

- Configurations: ophalen van analyse en evaluatie configuraties. Tevens ophalen van kruispunt groepen (indien geconfigureerd).

- Intersections: ophalen kruispunt data, opvragen beschikbare data ranges, ophalen analyse data en ophalen evaluatie data

- YAVC: ophalen lijst met id's van analyse typen, ophalen lijst met geconfigureerde meta data velden

De documentatie omvat informatie over de beschikbare API calls, alsook de data objecten die terug komen als resultaten van dergelijke calls. De informatie komt default in json formaat terug. Is er noodzaak om te werken met XML dan kan CodingConnected dit in overleg mogelijk maken.

## Praktisch gebruik: een typische use case

Een gebruikelijke use case voor de api is bijvoorbeeld: ontsluiten van intensiteitsdata naar een externe applicatie. Hieronder een beknopt stappenplan waarmee dit mogelijk wordt gemaakt.

### Opvragen analyse data

1. Ten eerste moet de authenticatie via OAuth2 worden geregeld. Zie hier boven bij authenticatie: client id en secret moeten bekend zijn, alsook het juist IP adres of domein waar de identity server draait. Het is raadzaam het ophalen van een token te testen, bijvoorbeeld met gebruik van de tool [insomnia](https://insomnia.rest/).

3. Om analyse data op te halen hebben we een aantal gegevens nodig:
    1. Type analyse: voor de aanvraag hebben we het id nodig. Voor intensiteiten is dit 1. Alle id's zijn op te vragen via het endpoint https://<server>:<poort>/api/yavc/analysisdetails
    
    3. Interval: in blokken van welke grootte moet de data terugkomen? Het minimum is 5 minuten, en het is raadzaam een interval te kiezen waarvan een veelvoud precies in een uur past. Bv.: 15 min.
    
    5. Start en einde van de periode waarover we data willen hebben

5. Als we dit hebben kunnen we een endpoint opbouwen om de data op te vragen, bijvoorbeeld:
    1. Stel we gaan uit van kruispunt 1, analyse intensiteiten ofwel id 1, interval 15 min, start datum/tijd is 16-03-2021 08:00, eind is 16-03-2021 10:00
    
    3. Dan wordt het endpoint: https://<server>:<poort>/api/intersections/1/analysis/1?intervalInMinutes=15&from=20210316080000&to=20210316100000
    
    5. Let vooral op de omzetting van de datum/tijd waarden naar tekst: dit volgt het formaat yyyyMMddHHmmss

7. Sturen we dit verzoek naar de api, en zijn we geauthenticeerd, dan komt de data, indien aanwezig terug

### Api respons

Uitgaande van het stappenplan hierboven zal het volgende terugkomen:

```json
{
  "intersectionId": 1,
  "analysisId": 1,
  "intersectionName": "K208",
  "analysisName": "Intensity",
  "start": "2021-03-16T08:00:00",
  "end": "2021-03-16T10:00:00",
  "intervalInMinutes": 15,
  "data": [
    {
      "itemId": 0,
      "itemName": "01",
      "time": "2021-03-16T08:00:00",
      "value": 40.0
    },
    {
      "itemId": 0,
      "itemName": "01",
      "time": "2021-03-16T08:15:00",
      "value": 54.0
    },
    {
      "itemId": 0,
      "itemName": "01",
      "time": "2021-03-16T08:30:00",
      "value": 49.0
    },
    ...
  ],
  "dataIncomplete": false,
  "missingRanges": []
}
```

We zien hier dat we de kruispunt en analyse id terugkrijgen, alsook de bijbehorende namen. Tevens komen start en einde voor de volledigheid terug in het resultaat. Vervolgens komt de eigenlijke data, met per resultaat per item een item in de lijst "data". Per item is er een index nummer, een naam, een tijd (de start tijd van de data voor dit blok) en een waarde. Merk hierbij op:

- De tijd is de eind tijd. De data is opgedeeld in blokken conform het opgegeven interval. Waar staat "time": "2021-03-16T08:00:00" geldt dus dat de navolgende waarde, de waarde is voor het tijdvak vanaf 'interval' minuten vóór die tijd tot aan die tijd zelf. In dit voorbeeld dus 15 minuten, dus 40 voertuigen tussen 7:45 en 8:00

- De "waarde" heeft uitsluitend betekenis gerelateerd aan enerzijds het interval, en anderzijds het type analyse. Zonder die informatie is de waarde zomaar een getal

Ten slotte volgen nog twee velden: 'dataIncomplete' en 'missingRanges'. De eerste is een boolean (waar of onwaar) en geeft aan of er sprake is van gaten in de data. De tweede is een lijst van evt. perioden waarvoor de data ontbreekt in het opgevraagde tijdvak. Hieronder een voorbeeld, wanneer we data opvragen uit de toekomst:

```json
  "dataIncomplete": true,
  "missingRanges": [
    {
      "type": 0,
      "startTime": "2022-03-16T08:00:00",
      "endTime": "2022-03-16T10:00:00"
    }
  ]
```

Het veld 'type' is hier een placeholder en wordt momenteel niet gebruikt.

#### Geen data beschikbaar?

Behoudens gaten in de data kan het ook zijn dat er überhaupt niet beschikbaar is. Dit is zo wanneer er voor (een deel van) de opgevraagde periode geen analyse configuratie beschikbaar is. Niet-beschikbaar-zijn geldt natuurlijk ook voor de toekomst, maar gezien de interne werking van YAVC is er wel een geldende analyse configuratie voor de toekomst, namelijk de laatst geldende configuratie die geldig is tot in de eeuwigheid.

Wordt data opgevraagd voor een periode waarvoor geen geldige analyse configuratie beschikbaar is, dan geeft de api een 500 melding terug, met de volgende inhoud:

```json
{
  "type": "https://tools.ietf.org/html/rfc7231#section-6.6.1",
  "title": "An error occurred while processing your request.",
  "status": 500,
  "detail": "Intersection with id 1 has no analysis configuration for the period between 3/16/1874 8:00:00 AM and 3/16/1874 10:00:00 AM",
  "traceId": "|503635f1-4f4e1ef976386b46."
}
```

Dit geldt tevens wanneer voor de opgevraagde periode er meer dan één configuratie geldig is; dit wordt niet ondersteund want er kunnen geen eenduidige resultaten worden teruggegeven.
