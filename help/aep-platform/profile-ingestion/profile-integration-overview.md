---
title: "[!DNL Platform] Overzicht van de handleiding voor profielontsluiting en toegang tot integratie"
description: Meer informatie over de integratie voor [!DNL Experience Platform] profielopname en toegang.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Integratiehandleiding: [!DNL Experience Platform] profielopname en toegang

De partners zouden deze integratiegids moeten gebruiken om hen bij het opbouwen van toegang en uitgang functionaliteit met de Adobe te helpen [!DNL Experience Platform] (AEP). Er zijn API&#39;s voor batch-opname, streaming-opname en Unified Profile-toegang (egress).

Ter ondersteuning van de ontwikkeling [Postman-collectie](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) is gecreeerd door het team van de Uitwisseling van de Adobe. Naar deze Postman-verzameling wordt in de integratiegids verwezen.

Meer informatie over het installeren en gebruiken van de Postman-collectie is beschikbaar op de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Er zijn ook voorbeelddatasets van [loyaliteit](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) en [profiel](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) gegevens.

## Het gebruik-geval van de integratie voorbeeld: Interactief systeem van de stemreactie

Voor integrators geldt dat de [!DNL Experience Platform] API&#39;s bieden alle mogelijkheden van het platform die in de hele gebruikersinterface worden aangeboden, maar nu ook de mogelijkheid om workflows voor klanten en geautomatiseerde gegevensstromen te maken. Als integrator, controleert u periodiek de status van datasets, opstellings nieuwe procedures van de gegevensopname, en integreert uw eigen oplossing van de publieksactivering met het Verenigde Profiel.

Overweeg de wereld van de systemen van de Reactie van de Interactieve Stem (IVR) en het beheerssoftware van het Centrum van de Vraag. De leverancier kan de [!DNL Experience Platform] APIs om historische informatie van de activiteit van het vraagcentrum van de klant in het meer van de Gegevens van de Ervaring in te nemen. Als de gegevens in de XDM worden opgenomen `ExperienceEvent` Het schema (een schema dat klanteninteractie uitdrukt), kunnen deze interacties zonder wrijving direct in de Verenigde Dienst van het Profiel worden opgenomen. In dit geval worden de `callerId` wordt gebruikt als de id van de klant. De dienst van de Identiteit zal voor identiteitsresolutie zorgen en zal de Verenigde Dienst van het Profiel bijstaan om het even welke gegevenspunten van recente interactie met het Centrum van de Vraag aan het profiel van de klant toe te voegen.

De volgende tijd een klant roept in het Centrum van de Vraag, zullen zij eerst door IVR worden beantwoord. Om het bericht te personaliseren en een aanbieding te leveren die aan de bezoeker wordt aangepast, moet het systeem IVR meer over de bezoeker begrijpen. Hier komt de API-integratie met het Unified Profile. De achtergrond IVR kan de Verenigde Dienst van het Profiel voor een puntraadpleging contacteren. Dan, raadpleeg of de profielattributen die op enkel vraag-centrum interactie of het volledige klantenprofiel van toepassing zijn, dat ook eigenschappen voor interactie op andere touchpoints heeft. Door gegevens van veelvoudige gegevensbronnen te combineren, gebruikend identiteitsresolutie, en het Verenigde Profiel, kunnen het vraagcentrum en de leverancier IVR een op maat gemaakte klantenervaring leveren, die door Adobe wordt gesteund [!DNL Experience Platform].&quot;

## Algemene middelen

* AEP [Productdocumentatie](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html).
* AEP [Uitbreidbaarheid](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Vragen of feedback?

Stuur alle vragen en feedback via de [ondersteuningskanaal](https://adobeexchangeec.zendesk.com/hc/nl-nl/requests/new)
