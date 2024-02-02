---
title: Toegang tot het verenigde profiel
description: Gebruik APIs om tot het Verenigde Profiel toegang te hebben.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Toegang tot het verenigde profiel met de profiel-API

De Adobe [!DNL Experience Platform] heeft realtime toegang tot het profiel van de klant; de [[!DNL Experience Platform] Real-time API voor klantprofiel](https://adobe.ly/2TtDHWr) is ontworpen om daarmee te communiceren. Zie dit [zelfstudie](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html) voor toegang tot de realtime gegevens van het klantprofiel met de profiel-API.

In dit artikel wordt in grote lijnen verwezen naar de bovenstaande zelfstudie.

De [Postman-collectie](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wordt van verwijzingen voorzien door het artikel gebruikend de bijbehorende vraag door aantal. Meer informatie over het installeren en gebruiken van de Postman-collectie is beschikbaar op de Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Er zijn ook voorbeelddatasets van [loyaliteit](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) en [profiel](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) gegevens.

Voor deze sectie gebruikt u de Postman-map 5: Profiel opzoeken, 5a: Real-time opzoekPROFILE-gegevens OF 5b: Real-time opzoekgegevens van GEBEURTENISSEN.

## De API gebruiken

De volgende secties helpen u bij het voor authentiek verklaren aan Experience Platform. Meer informatie over het API-pad, koptekstgegevens en meer.

### Verifiëren voor [!DNL Platform]

Zie [dit](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html) de authentificatiezelfstudie alvorens om het even welke hieronder vraag te maken.

### API-pad

De platformgateway-URL die nodig is voor de real-time API voor het klantprofiel is: `https://platform.adobe.io/`

Het basispad voor de API is: `/data/core/ups/access/entities`

Een voorbeeld van een volledig pad is: `https://platform.adobe.io/data/core/ups/access/entities`

### Informatie over koptekst

De koptekst moet het volgende bevatten:

* Toestemming
* x-gw-ims-org-id - verkrijgbaar via console.adobe.io
* x-api-key - ophalen via console.adobe.io
* x-sandbox-name - opgehaald uit de Adobe Integration Manager
* Inhoudstype: application/json

Meer informatie over de koptekst vindt u in het gedeelte [zelfstudie](https://adobe.ly/2PTHuKv).

## Toegang tot realtime klantprofielen met identiteiten

Met de profiel-API hebt u via een GET-aanvraag toegang tot profielen met een id. Hieronder vindt u de volgende secties [hulplijn](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html).

### Profielgegevens benaderen met identiteit

De API geeft toegang tot profielinformatie gebruikend identiteit. Dit wordt gedaan door een verzoek van de GET aan /access/entities met entiteitsidentiteitskaart als één van de parameters en entiteitsidentiteitskaart te doen namespace. NOTA: Houd in mening dat om het even welk verzoek dat 50 verslagen terugkeert slechts een 422 status van HTTP en een bericht zal leveren dat &quot;teveel verwante identiteiten&quot;leest en het onderzoek met meer parameters zal moeten worden versmald.

Verzoek:

Met het volgende verzoek worden de e-mail en de naam van een klant opgehaald aan de hand van een identiteit:

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Reactie:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Toegangsprofielen op lijst met identiteiten

API verleent toegang tot profielen gebruikend een lijst van identiteiten door een verzoek van de POST aan het /access/entities eindpunt te gebruiken en de identiteiten in de nuttige lading te verstrekken. Deze identiteiten bestaan uit een ID-waarde (entityId) en een naamruimte identity (entityIdNS).

Verzoek: Het volgende verzoek haalt de namen en e-mailadressen van verscheidene klanten door een lijst van identiteiten terug:

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Respose: Een succesvolle reactie keert de gevraagde gebieden van entiteiten terug die in het verzoeklichaam worden gespecificeerd.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Gebeurtenissen van tijdreeksen

De partners kunnen tot de gebeurtenissen van de tijdreeks door de identiteit van de bijbehorende profielentiteit toegang hebben door een verzoek van de GET tot het /access/entities eindpunt te richten.

### De gebeurtenissen van de tijdreeks van de toegang voor een profiel door identiteit

De gebeurtenissen van de tijdreeksen worden betreden door de identiteit van hun bijbehorende profielentiteit door een verzoek van de GET tot het /access/entities eindpunt te richten. Deze identiteit bestaat uit een ID-waarde (entityId) en een naamruimte voor identiteit (entityIdNS).

Verzoek: Met de volgende aanvraag wordt een profielentiteit gevonden op ID en worden de waarden opgehaald voor de eigenschappen endUserIDs, web en channel **voor iedereen** aan de entiteit gekoppelde tijdreeksgebeurtenissen.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Reactie:

Een geslaagde reactie retourneert een gepagineerde lijst met gebeurtenissen uit de tijdreeks en de bijbehorende velden die in de aanvraagparameters zijn opgegeven.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Paginering voor tijdreeksgebeurtenissen voor een profiel

Resultaten worden gepagineerd bij het ophalen van tijdreeksgebeurtenissen. Als er volgende pagina&#39;s met resultaten zijn, bevat de parameter _page.next van het antwoord een id. Daarnaast biedt de parameter _links.next.href van de reactie een aanvraag-URI voor het ophalen van de volgende pagina.

Verzoek:

Met de volgende aanvraag wordt de volgende pagina met resultaten opgehaald met de URI _links.next.href als aanvraagpad.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Reactie:

Als de reactie is gelukt, wordt de volgende pagina met resultaten geretourneerd. In dit voorbeeld wordt een reactie getoond waarbij geen volgende pagina&#39;s met resultaten worden weergegeven, zoals wordt aangegeven door de lege tekenreekswaarden van _page.next en _links.next.href.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Referentieartikelen

* [Real-time API voor klantprofiel](https://adobe.ly/2TtDHWr)
* [Toegang tot realtime klantprofielgegevens met behulp van de profielAPI-zelfstudie](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Verificatiehandleiding](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)
