---
title: "Ik zie geen GUS/WUS/multivalente IO"
date: 2021-03-15
---

Soms ziet data er niet uit zo uit als verwacht. Bijvoorbeeld:

- GUS en WUS van uitgangen loopt niet gelijk
- De data bevat enkel GUS of enkel WUS van uitgangen
- De data bevat in tegenstelling tot de verwachting geen multivalente data
- Timings ontbreken
- Etc.

De meest waarschijnlijke oorzaak van dit type problemen is: foutieve configuratie van VLOG in het regelprogramma. Dit is dus ook de eerste plek om te zoeken naar de oorzaak. Bijvoorbeeld als volgt:

- Ga eerst na: betreft de data filebased data, die dus op de (i)VRI is aangemaakt, en via (s)ftp is gedownload? Of gaat het om streaming VLOG data die is omgezet naar een bestand (of direct vanuit een centrale wordt bekeken)?
- Ga vervolgens na: betreft dit een CCOL regeling of een netwerk regelaar (zoals imflow, flowtack, etc.)
- In geval van een netwerk regelaar:
    - Leg het probleem voor aan de makers van de betreffende regeling, automaat en/of ITS-box
- In geval van een CCOL regelaar:
    - Let op! Er zijn twee typen configuratie binnen CCOL: LOG (=filebased) en MON (=streaming). Om deze reden is van belang te weten om welk type data het gaat.
    - Controleer de BITs waarmee wordt ingesteld wat voor welk type item wel/niet wordt weggeschreven. Let hierbij op: kijk naar MON of LOG al naar gelang het type data.
    - Voor multivalente IO moet het juiste US\_type worden ingesteld voor de uitgang(en) die multivalent is/zijn. Dit moet per uitgang worden opgegeven.
    - Normaal gesproken wordt dit tijdens het programmeren van de regeling ingesteld (meestal in "tab.c"). Het is ook mogelijk een en ander via de parser in te stellen, zie de CCOL documentatie.
    - Zie voor meer details de documentatie van CCOL
