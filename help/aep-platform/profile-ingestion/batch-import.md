---
title: Batchgegevens importeren naar AEP
description: Leer hoe u batchbestanden in Experience Platform importeert
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Batchgegevens importeren naar AEP

AEP kan batchbestanden opnemen die profielgegevens bevatten van een plat bestand (zoals een parket) of gegevens die overeenkomen met een bekend schema in het [!UICONTROL Experience Data Model] (XDM) register.

AEP kan gegevens invoeren met batchbestanden. De volgende indelingen worden geaccepteerd: JSON, Parquet en CSV.

Dit artikel heeft betrekking op:

* Voorwaarden voor inname in batch
* Aanbevolen werkwijzen en limieten bij inname in batch
* Hoe maakt u een batch
* Hoe een batch voltooien
* Hoe de status van een batch te controleren

De [Postman-collectie](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wordt van verwijzingen voorzien door het artikel gebruikend de bijbehorende vraag door aantal. Meer informatie over het installeren en gebruiken van de Postman-collectie is beschikbaar op de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Er zijn ook voorbeelddatasets van [loyaliteit](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) en [profiel](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) gegevens.

Gebruik voor alle aanroepen in deze zelfstudie Postman-callmappen: 4: Batch importeren, 4a: Batch importeren voor PROFILE-gegevens OF 4b: Batch importeren voor GEBEURTENISgegevens.

## Voorwaarden voor inname in batch

* Definieer een schema en maak een dataset.
* De gegevens moeten worden opgemaakt in JSON, Parquet of CSV.
* [Verifiëren voor het platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Verzamel de waarden voor vereiste kopballen van de hierboven verbonden authentificatiezelfstudie.

## Aanbevolen werkwijzen en limieten bij inname in batch

* Maximale batchgrootte: 100 GB
* Maximumaantal bestanden per batch: 1500
* Als een bestand groter is dan 512 MB, moet het in kleinere delen worden verdeeld. Meer informatie vindt u in het gedeelte [ontwikkelaarsgids](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Maximumaantal eigenschappen of velden per rij: 10.000
* Maximumaantal batches per minuut per gebruiker: 138

## Een batch maken

In deze zelfstudie gebruiken we JSON als de indeling. Meer indelingsvoorbeelden vindt u in het dialoogvenster [ontwikkelaarsgids](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Creeer een partij gebruikend JSON als inputformaat (ben zeker om een dataset identiteitskaart te omvatten en dat uw gegevens met het schema XDM verbonden aan de dataset in overeenstemming zijn):

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Reactie:

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Bestanden uploaden

Bestanden kunnen nu worden geüpload naar de nieuwe batch (met behulp van batch_id uit de bovenstaande reactie).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>De API ondersteunt alleen uploaden in één deel, wat betekent dat elk bestand/elke microbatch moet worden geüpload met individuele aanroepen. Zorg ervoor dat het inhoudstype application/octet-stream is.

Reactie:

```
200 OK
```

## Een batch voltooien

Zodra alle dossiers zijn geupload, zal deze vraag erop wijzen dat de partij voor bevordering klaar is:

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Reactie:

```
200 OK
```

## De status van een batch controleren

De batchstatus kan worden gecontroleerd in de gebruikersinterface of via de API (zie onderstaande aanroep). Om in UI te controleren, navigeer aan DataSet om de status te zien.

De verschillende statussen van inname in batch zijn te vinden [hier](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Reactie:

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Referentieartikelen

* [Data Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Overzicht van batchverwerking](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Handleiding voor ontwikkelaars van batchverwerking](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Handleiding voor het oplossen van problemen met inslikken](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Postman-verzameling gegevensinname](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Zelfstudie verificatie](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
