---
title: AEP-schema's en gegevenssets maken
description: Creeer schema's en datasets in Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# Schema&#39;s en gegevenssets maken

De [Postman-collectie](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wordt van verwijzingen voorzien door het artikel gebruikend de bijbehorende vraag door aantal. Meer informatie over het installeren en gebruiken van de Postman-collectie is beschikbaar op de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Er zijn ook voorbeelddatasets van [loyaliteit](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) en [profiel](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) gegevens.

## Schema&#39;s

Een schema is een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. Op een hoog niveau, verstrekken de schema&#39;s een abstracte definitie van een real-world voorwerp (zoals een persoon) en schetsen welke gegevens in elke instantie van dat voorwerp (zoals voornaam, achternaam, verjaardag, etc.) zouden moeten worden omvat. De schema&#39;s kunnen in UI of het gebruiken van worden gecreeerd [!DNL Experience Platform] API&#39;s.

Zie [deze documentatie](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) voor meer informatie .

### Een schema maken

De partners kunnen een schema bouwen gebruikend UI door dit te volgen [zelfstudie](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html). In dit voorbeeld wordt het profielschema van het loyaliteitsprogramma gebruikt. Terwijl het voorbeeld een profielschema is, kunnen op gebeurtenis-gebaseerde schema&#39;s worden gebruikt gebruikend een gelijkaardig proces.

Om APIs te gebruiken, moeten de partners een bestaande Adobe I/O integratie met hebben [!DNL Experience Platform] rechten ingeschakeld. Zie deze handleiding voor [I/O-integratie maken](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

Ga vervolgens naar [deze koppeling](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-api.html) om te leren hoe u schema&#39;s bouwt met behulp van de API.

Als u een schema wilt maken via Postman, gebruikt u de aanroepen in de mappen 1: Schema maken, 1a: Schema maken voor PROFIELgegevens OF 1b: Schema maken voor GEBEURTENISgegevens.

## Gegevenssets

Alle gegevens die in de Adobe worden gebracht [!DNL Experience Platform] is opgenomen in gegevenssets. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Catalogusservice is het registratiesysteem voor gegevenslocatie en -lijn binnen [!DNL Experience Platform]en wordt gebruikt om gegevenssets te maken en te beheren. De catalogus volgt de meta-gegevens voor elke dataset, die een verwijzing naar het schema van de Gegevens van de Ervaring (XDM) omvat de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Ga [hier](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/overview.html) voor een gedetailleerd overzicht van de gegevensset.

### Een gegevensset maken

![Bewegende GIF voor gegevensset maken](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Een gegevensset maken via de gebruikersinterface:

1. Klik op **[!UICONTROL Create Dataset]**.

1. Klik op **[!UICONTROL Create from schema]**.

1. Klik op **[!UICONTROL Finish]**.

Ga [hier](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html) voor een dataset gebruikershandleiding.

[Een gegevensset maken met de API&#39;s](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/create.html).

Als u een gegevensset wilt maken via Postman, gebruikt u mappen 2: Gegevensset maken, 2a: Gegevensset maken voor PROFILE-gegevens OF 2b: Gegevensset maken voor GEBEURTENISgegevens.

## De beste praktijken van het schema en van de dataset voor partners

* De gegevens van de partner zouden een afzonderlijk profielschema tegenover het creëren van een mengeling-binnen voor het bestaande het profielschema en ervaringsschema van een klant moeten gebruiken.
* De partners zouden klassen en mengen-ins van de Adobe waar mogelijk moeten gebruiken.
* De partners zouden hun gegevens moeten uploaden gebruikend een afzonderlijke dataset in plaats van het proberen om hun gegevens in een bestaande dataset te combineren.
* De partners kunnen hun schema&#39;s aan het globale register momenteel niet uploaden.
