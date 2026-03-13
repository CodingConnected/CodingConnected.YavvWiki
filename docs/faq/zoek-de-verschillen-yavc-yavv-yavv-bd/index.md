---
title: "Zoek de verschillen: YAVC, YAVV, YAVV/bd"
date: 2021-01-18
---

De namen YAVV en YAVC wekken soms verwarring: wat is nu precies wat, en wat kan waarmee precies doen? Daarom hier een beknopte toelichting:

- [YAVC](https://www.codingconnected.eu/software/ivri-centrale/) is de **VLOG centrale van CodingConnected**. De centrale is een server applicatie met bijbehorende (afzonderlijke) client applicatie. De server verzamelt en analyseert data, die met de client kan worden bekeken.YAVC is gericht op continue dataverzameling.
    - YAVC voert ook continu analyses uit, die vervolgens op afroep beschikbaar zijn.
    - De data zit bij YAVC in een database, óók de analyse data, en is zonder meer te bekijken met de client.
    - YAVC beschikt over een API voor koppeling met externe applicaties, zoals PowerBI, etc.
    - Met YAVC is het mogelijk op grote schaal met data te werken: gemiddelden over langere perioden, trend analyses, etc.
    - De client van YAVC is net als YAVV een Windows desktop applicatie, maar werkt niet met data van schijf. In plaats maakt de client verbinding met de database om data op te halen.
- [YAVV](https://www.codingconnected.eu/software/yavv/) is een **standalone desktop applicatie** voor Windows waarmee **VLOG data van schijf** kan worden ingelezen:
    
    - YAVV werkt dus met data van de harde schijf (of van een netwerk schijf). Deze moet dus ergens vandaan komen.
    - YAVV is gericht op werken met data van een aantal uren, een dag, of - zo lang er voldoende geheugen is - ook een langere periode.
    
    - De data wordt weergegeven in de vorm van een fasenlog.
    - De data kan worden gefilterd en geanalyseerd.
    - De analyse kan ook worden gevisualiseerd en geëxporteerd.
    - YAVV is vooral geschikt voor wie op zoek is naar (verkeersregelkundige) details in de VLOG data, of wie op kleine schaal wil analyseren.
- [YAVV/bd](../../yavv/yavv-big-data-introductie/index.md) (YAVV "big data") is een addon voor YAVV. De addon voegt aanvullende functionaliteit toe aan YAVV, waardoor het mogelijk wordt te **werken met mappen met VLOG data**.
    - Net als YAVV werkt YAVV/bd met data van schijf.
    - Met YAVV/bd kan een map worden geöpend, die dan wordt geïndexeerd. YAVV zoekt dan uit welke data er in de map zit.
    - Na indexatie is zichtbaar welke data beschikbaar is. Er is snel toegang naar de fasenlog en analyse per dag.
    - Tevens is het mogelijk trend analyses uit te voeren over een selectie van dagen: gemiddelden en het verloop van bepaalde analyse grootheden over een langere periode.
    - Deze addon vergt een aanvullende licentie, bovenop de reguliere licentie voor YAVV pro.
