---
title: Ansluta till informationslagret med Power BI
titleSuffix: Microsoft Intune
description: Du kan ladda ned en fil och använda den med Microsoft Power BI för att läsa in interaktiva och dynamiskt skapade rapporter för Microsoft Intune-klientorganisationen.
keywords: Intune-informationslager
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5E5A35D3-88F8-441B-8A0B-C5D7A1E5137B
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6dfba55c8e516e2e689513f063d56f5a43d52d9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359891"
---
# <a name="connect-to-the-data-warehouse-with-power-bi"></a>Ansluta till informationslagret med Power BI

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Du kan använda Compliance-appen i Power BI för att läsa in interaktiva, dynamiskt skapade rapporter för din Intune-klientorganisation. Du kan också läsa in klientorganisationens data i Power BI med hjälp av OData-länken. Intune tillhandahåller anslutningsinställningar för din klientorganisation så att du kan visa följande exempelrapporter och diagram relaterade till:  

- Egenskaper
- Registrering
- Appskyddsprincip
- Policy för efterlevnad
- Enhetens konfigurationsprofiler
- Programuppdateringar
- Inventeringsloggar för enheten

Här markeras också trenderna för registrering, regelefterlevnad, enhetens konfigurationsprofil och programuppdateringar. För exempeldiagram och rapporter tillämpas användarvänliga filter på arbetsytan. Om du vill använda avancerade filter kan du gå till rutan **Filter** i Power BI Desktop.

I följande anvisningar visas hur du laddar ned Power BI-filen och använder OData-länken med Power BI.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## <a name="install-power-bi"></a>Installera Power BI

Installera den senaste versionen av [Power BI Desktop](https://aka.ms/intune/datawarehouseapi/installpowerbi). Mer information finns i [Power BI Desktop](https://powerbi.microsoft.com/desktop)

## <a name="load-the-data-and-reports-using-the-power-bi-intune-compliance-data-warehouse-app"></a>Läsa in data och rapporter med Intune Compliance Data Warehouse-appen i Power BI

[Intune Compliance-appen (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) i Power BI innehåller information för din klientorganisation och en uppsättning fördefinierade rapporter baserade på Data Warehouse-datamodellen.

1. Navigera till **AppSource-sidan** i [Intune Compliance-appen (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) för att påbörja installationen.
2. Klicka på knappen **Hämta nu** och klicka sedan på **Fortsätt**.
3. När du uppmanas att installera Power BI-appen klickar du på **Installera**.
4. När installationen är klar klickar du på app-rutan **Intune Compliance Data Warehouse-appen**.
5. Klicka på knappen **Anslut**. Dialogrutan **Anslut till Intune Compliance Data Warehouse App** visas.
6. Klicka på knappen **Logga in**.
7. Logga in med ett användarkonto som har åtkomst till Intune-informationslagret för den klient som har rapporter som du vill visa.
8. Om du vill visa instrumentpanelen som ingår klickar du på fliken **Instrumentpaneler** och klickar sedan på instrumentpanelen för **efterlevnadsöversikt**.
9. Om du vill se alla tillgängliga rapporter klickar du på fliken **Rapporter** och klickar sedan på rapporten **Compliance V1.0**. Bläddra igenom rapportsidorna genom att klicka på flikarna längst ned.
10. Om du vill göra det enklare att gå tillbaka till de här rapporterna senare klickar du på stjärnan bredvid rapporten **Compliance V1.0**. När du gör det läggs rapporten till i dina Power BI-favoriter.

Du kan också installera appen från Intune-portalen:

1. Logga in på Azure Portal och välj **Övervakning + hantering** > **Intune**. Du kan också söka efter resurser för Intune.
2. Öppna bladet **Konfigurera Intune Data Warehouse**.
3. Välj **Hämta Power BI-appen** så att du kan komma åt och dela Power BI-rapporter som skapats i förväg för din klientorganisation i webbläsaren.
4. Följ steg 2–10 ovan.

## <a name="load-the-data-in-power-bi-using-the-odata-link"></a>Läsa in data i Power BI med OData-länken

När en klient har autentiserats med Azure AD ansluter OData-webbadressen till RESTful-slutpunkten i informationslager-API:t som gör datamodellen tillgänglig för rapporteringsklienten. Följ de här anvisningarna för att ansluta och skapa egna rapporter med hjälp av Power BI Desktop. Du är inte begränsad till enbart Power BI Desktop utan kan använda ett valfritt analysverktyg med OData-webbadressen så länge klienten har stöd för OAUTH2.0-autentisering och OData v4.0-standarden.

1. Logga in på [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Klicka på **Konfigurera Intune Data Warehouse** under avsnittet **Andra uppgifter** till höger på översiktsbladet. Bladet **Intune Data Warehouse** visas.
3. Hämta webbadressen till anpassad feed på rapportbladet, till exempel:<br>
    `https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Öppna **Power BI Desktop**.
5. Välj **Arkiv** > **Hämta data**. Välj**OData-feed**.
6. Välj **Basic**.
7. Skriv eller klistra in **OData-URL** i webbadressrutan.
8. Välj **OK**.
9. Om du inte har autentiserats med Azure AD för klientorganisationen från Power BI-skrivbordsklienten anger du dina autentiseringsuppgifter. För att få åtkomst till dina data måste du auktorisera Azure Active Directory (Azure AD) med hjälp av OAuth 2.0.  
    1. Välj **Organisationskonto**.  
    2. Ange användarnamn och lösenord.  
    3. Välj **Logga in.**  
    4. Välj **Anslut**.  
10. Välj **Läs in**.

## <a name="next-steps"></a>Nästa steg

Du hittar svar på frågor om miljön, till exempel hur många enheter som har registrerats per dag den senaste veckan. Du kan få bättre insyn i din Intune-klientorganisation och klientpopulation med hjälp av Power BI-rapporterna i Intune Data Warehouse som du hämtat från bladet i Azure. Intune tillhandahåller dock ett antal ytterligare sätt att utöka eller återanvända dessa data. Med Power BI och API:et för Intune Data Warehouse har du tillgång till fler funktioner, till exempel:

<!-- - You can use Power BI Desktop to create additional report types with your data. For example, you could create a custom chart representing the ratio of device manufactures in your enterprise. For more information about creating custom reports with Power BI and the Intune Data Warehouse, see `BLOG POST ON POWER BI`. -->
- Klientorganisationsdata sammanställs så att de lätt kan tolkas. Mer information om hur data sammanställs finns i [Datamodellen informationslager](reports-ref-data-model.md).
- Du kan också komma åt informationen från ett RESTful-gränssnitt och kan lägga till informationen i din egen app. Mer information finns i [Hämta data från API för informationslager med en REST-klient](reports-proc-data-rest.md).
