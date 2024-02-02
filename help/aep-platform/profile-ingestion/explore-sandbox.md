---
title: De AEP-sandbox openen en verkennen
description: Leer hoe u de sandbox met Experience Platforms kunt openen en verkennen.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# De AEP-sandbox openen en verkennen

Dit artikel heeft betrekking op:

* De verschillen tussen een bestaande de zandbakorganisatie van de Partner van de Uitwisseling van de Adobe en de gedeelde zandbak van AEP.
* Toegang tot de gedeelde AEP-sandbox aanvragen.
* Een e-mailuitnodiging ontvangen voor de gedeelde AEP-sandbox.
* Nieuwe gebruikers uitnodigen in het dialoogvenster [!DNL Admin Console].
* Navigeren door de interface van AEP.

Voor een algemeen overzicht van de Sandbox technologie in AEP, zie dit [artikel](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html).

## De gedeelde AEP-sandbox

De partners van de uitwisseling krijgen toegang tot diverse Adobe [!DNL Experience Cloud] producten (niet-AEP-producten zoals [!DNL Analytics], [!DNL Target], Platform-tags enzovoort) via hun eigen Adobe [!DNL Experience Cloud] Org (niet-gedeeld). De partners worden gegeven de toegangsrechten van de systeembeheerder aan hun eigen Org om gebruikers en andere toestemmingen te beheren. Adobe [!DNL Experience Platform] (AEP) wordt anders behandeld dan andere Adobe sandboxen. Hier zijn de belangrijkste verschillen:

* De toegang tot AEP zal NIET via de belangrijkste Adobe van de partners plaatsvinden [!DNL Experience Cloud] sandbox Org.
* De toegang tot AEP is via een gedeelde Adobe Exchange Org.
* Veel andere partnerbedrijven van de Uitwisseling van de Adobe hebben toegang tot AEP gebruikend zelfde Org
   * Via de functie AEP-sandbox kunnen gegevens en activiteiten binnen deze gedeelde organisatie niet door de andere partners worden gezien of gewijzigd; elke partner heeft toegang tot een andere sandbox binnen de gedeelde organisatie.
* De beheersrechten binnen dit gedeelde Org zijn zeer beperkt.
* Nadat toegang tot een zandbak op AEP wordt verleend, zullen de partners twee Orgs op de Org schakelaar in het hoogste recht van UI zien terwijl in de Admin Console of belangrijkste Experience Cloud homepage. Wanneer u zich echter aanmeldt bij AEP, moet alleen de gedeelde organisatie zichtbaar zijn.

## Toegang aanvragen tot de gedeelde AEP-sandbox

Een [supportverzoek](https://adobeexchangeec.zendesk.com/hc/nl-nl/requests/new) met de volgende informatie:

* E-mailadres
* Betreft: AEP Sandbox-verzoek
* Product: Algemene provisioning / Sandbox
* Tickettype: Programmaondersteuning - Exchange-programma / Vragen over leveringsverzoek
* Omschrijving: geef een korte beschrijving van het (de) integratiegebruik-geval(en) waarvoor een AEP-sandbox moet worden gebruikt
* Zorg ervoor dat u ook alle gebruikersnamen en e-mails opgeeft die aan de AEP-sandbox moeten worden toegevoegd. Het is mogelijk om extra gebruikers toe te voegen nadat het verzoek wordt ingediend maar de gebruikers zullen door Adobe via een extra kaartje moeten worden toegevoegd (zie hieronder).

## De e-mailuitnodiging ontvangen

De primaire contactpersoon die de AEP-sandbox heeft aangevraagd, ontvangt een automatische e-mail met de uitnodiging om aan de slag te gaan met de Adobe [!DNL Experience Platform]. De primaire contactpersoon heeft ook enkele beheerrechten die in de volgende sectie worden behandeld.

Navigeer in plaats van de knop &quot;Aan de slag&quot; in de e-mail rechtstreeks naar `https://platform.adobe.com.` Meld u aan bij de Adobe ID die is gekoppeld aan het e-mailadres in de uitnodiging of maak een account als het niet is gekoppeld aan een Adobe ID.

## Extra gebruikers uitnodigen

Een [supportverzoek](https://adobeexchangeec.zendesk.com/hc/nl-nl/requests/new) met de volgende informatie:

* E-mailadres aanvrager
* Betreft: AEP-sandbox - Admin/User toevoegen
* Product: Algemene provisioning / Sandbox
* Tickettype: Programmaondersteuning - Exchange-programma / Vragen over leveringsverzoek
* Omschrijving: Lijst met gebruikers die moeten worden toegevoegd (namen en e-mails)

## Navigeren door de interface van AEP

De interface van AEP bekijken [inleidende video](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Er zijn 12 primaire gebieden binnen AEP UI die via het linkerpaneel kunnen worden genavigeerd. Nochtans, zijn de belangrijkste secties voor dit type van integratie Schema&#39;s, Datasets, en Profielen.

* Home - Het landingsscherm

   * Suggesties voor een aantal begonnen activiteiten
   * Verzekert sommige verbindingen met het leren inhoud
   * Geeft een dashboardweergave voor enkele belangrijke AEP-objecten, zoals schema&#39;s, gegevenssets en profielen

* Workflows - introductie in algemene workflows voor het plaatsen van gegevens in AEP
* Verbindingen/Bronnen - bronnen beheren die in AEP komen
* Verbindingen/Doelen - beheer de verbindingen om gegevens naar externe systemen te verzenden
* Profielen - afzonderlijke klantprofielen bekijken en beheren
* Segmenten - doorblader, creeer en wijzig klantensegmenten
* Identiteiten - doorblader, creeer en wijzig identiteitsnamespaces; dit zijn de types primaire IDs die worden gebruikt om een klant uniek te identificeren
* Modellen (Data Science) - nemen deel aan activiteiten op het gebied van gegevenswetenschap, waaronder het gebruik van een ingesloten Jupyter-laptopomgeving
* Services (Data Science) - publiceer recepten voor gegevenswetenschappen als diensten
* Schema&#39;s - doorblader, creeer en wijzig schema&#39;s; dit zijn de gedetailleerde gegevensdefinities die worden gebruikt om gegevens te houden georganiseerd
* DataSets - doorblader, creeer en beheer DataSets; een Dataset wordt bepaald door een Schema en is waar de gegevens binnen AEP verblijven
* Vraagstukken - doorblader, creeer, wijzig en gebruik een bewaarplaats van vragen om inzichten van de gegevens binnen Datasets te verkrijgen
* Bewaking - bekijk de status van alle gegevens die in- en uitstappen van AEP voor zowel batch als streaming
