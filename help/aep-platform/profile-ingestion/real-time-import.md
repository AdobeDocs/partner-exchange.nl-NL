---
title: Importeren in realtime
description: Leer hoe u gegevens in real-time naar AEP kunt importeren.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Gegevens streamen naar AEP

Adobe [!DNL Experience Platform] kan zowel profiel- als ervaringsgebeurtenissen worden gestreamd en in realtime beschikbaar zijn. Alle gegevens die via streaming naar AEP worden verstuurd, blijven in het datumpomeer aanwezig. Gegevens kunnen naar bestaande gegevenssets of naar geheel nieuwe gegevenssets worden gestreamd via API&#39;s of via het starten van Adoben.

Dit artikel heeft betrekking op:

* Streamen naar het afzonderlijke XDM-profiel
* Streamen naar de XDM ExperienceEvent
* De extensie Starten gebruiken om te streamen

De [Postman-collectie](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wordt van verwijzingen voorzien door het artikel gebruikend de bijbehorende vraag door aantal. Meer informatie over het installeren en gebruiken van de Postman-collectie is beschikbaar op de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Er zijn ook voorbeelddatasets van [loyaliteit](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) en [profiel](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) gegevens.

## Vereisten

* [Verifiëren voor het platform](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html).
* Verzamel de waarden voor vereiste kopballen van de hierboven verbonden authentificatiezelfstudie.

## Een streamingverbinding maken

Als u wilt streamen naar AEP, moet u eerst een streamingverbinding maken. Streaming verbindingen bevatten kenmerken zoals de bron van streaming gegevens en of u records verzendt die bij de [!DNL Experience Data Model] (XDM) schema&#39;s. Nadat u een streamingverbinding hebt gemaakt, krijgt u een unieke URL waarmee u gegevens kunt streamen naar AEP.

Ga [hier](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) voor instructies over het maken van een streamingverbinding via API of [hier](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) voor instructies over hoe te om een het stromen verbinding via UI tot stand te brengen.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Reactie:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Ben zeker om identiteitskaart te bewaren die in de reactie hierboven voor toekomstige het stromen ingaat vraag wordt verstrekt (de inzameling van Postman zal dit voor u in de milieu variabele CONNECTION_ID bewaren).

## Profielgegevens naar AEP streamen

Gebruik voor deze sectie Postman-callmappen: 3: Real-time importeren, 3a: Real-time importeren voor PROFILE-gegevens.

Gedetailleerde JSON-aanvragen met reacties voor streaming profielgegevens worden gedocumenteerd [hier](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Stappen:

1. Een individueel XDM-profielschema maken
1. De primaire identiteitsbeschrijving instellen voor het afzonderlijke XDM-profiel (primaire sleutel)
1. Een gegevensset maken voor afzonderlijke XDM-profielrecords
1. Roep de Streaming Ingestie-API&#39;s aan om een XDM Individual Profile Record te maken
1. Het nieuwe profiel ophalen

## Gebeurtenissen voor streamervaringen naar AEP

Gebruik voor deze sectie Postman-callmappen: 3: Real-time importeren, 3b: Real-time importeren voor PROFILE-gegevens.

Gedetailleerde JSON-aanvragen met reacties voor streamingervaringen worden gedocumenteerd [hier](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Stappen:

1. Een XDM ExperienceEvent-schema maken
1. De primaire identiteitsbeschrijving instellen voor XDM ExperienceEvent (primaire sleutel)
1. Een gegevensset maken voor XDM ExperienceEvents
1. Roep de API&#39;s voor streaming insluiting aan om een XDM ExperienceEvent te maken
1. De nieuwe gebeurtenis ophalen

## Experience Platform-tags gebruiken om te streamen naar AEP

De Adobe [!DNL Experience Platform] Met de extensie Starten kunt u via Launch naar AEP streamen. Zie voor meer informatie [deze handleiding](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Referentieartikelen

* [API&#39;s voor gegevensinname](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Overzicht van streaming inscriptie](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Handleiding voor ontwikkelaars van streaming-insluiting](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [De AEP-extensie starten gebruiken](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
