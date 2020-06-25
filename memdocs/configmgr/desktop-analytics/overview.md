---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: En översikt över tjänsten Desktop Analytics som är integrerad med Configuration Manager.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 774e77f62ee31daa89eeb4273f3c1e7db68a374d
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353487"
---
# <a name="what-is-desktop-analytics"></a>Vad är Desktop Analytics?

Desktop Analytics är en molnbaserad tjänst som kan integreras med Configuration Manager. Tjänsten ger insikt och information för att fatta mer välgrundade beslut om uppdaterings beredskap för dina Windows-klienter. Den kombinerar data från din organisation med data som sammanställs från miljon tals enheter som är anslutna till Microsofts moln tjänster.

Använd Skriv bords analys med Configuration Manager för att:  

- Skapa en inventering av appar som körs i din organisation  

- Utvärdera appens kompatibilitet med de senaste funktions uppdateringarna för Windows 10  

- Identifiera kompatibilitetsproblem och ta emot minsknings förslag baserat på molnbaserade data insikter  

- Skapa pilot grupper som representerar hela program-och driv rutins egendomen i en minimal uppsättning enheter  

- Distribuera enheter som hanteras av Windows 10 till pilot och produktion  

![Skärm bild av start sidan för Skriv bords analys i Azure Portal](media/portal-home.png)

Följande video är en session från antändning 2019, som innehåller mer information om Desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Med hjälp av Skriv bords analys och Configuration Manager kan du minska Windows TCO genom data drivna insikter för hantering, underhåll och support](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Hoppa till 10:00 för en djupgående demonstration.

> [!Note]  
> Desktop Analytics är en efterföljande av Windows Analytics, som dras tillbaka den 31 januari 2020.
>
> Funktionerna i Windows Analytics kombineras i Skriv bords analys tjänsten. Desktop Analytics är också mer tätt integrerat med Configuration Manager. Mer information finns i [vanliga frågor och svar om Windows Analytics-kunder](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Fördelar

Många kunder har utmaningar med att hämta och hålla dig uppdaterad med Windows 10. Den primära utmaningen är att testa program. Den här processen är vanligt vis manuell. Det är tids krävande för IT-administratörer och program ägare att kontinuerligt analysera befintliga program. Åtgärda eventuella problem som uppstår.

Desktop Analytics ger följande fördelar:

- **Enhets-och program varu inventering**: inventering av viktiga faktorer, till exempel appar och versioner av Windows.  

- **Pilot identifiering**: identifiering av den minsta uppsättningen enheter som ger flest täckning av faktorer. Den fokuserar på de faktorer som är viktigast för en pilot med Windows-uppgraderingar och uppdateringar. Att se till att piloten är mer framgångs rik gör att du snabbt och säkert kan gå vidare till breda distributioner i produktionen.  

- **Problem identifiering**: med hjälp av sammanställd marknads information tillsammans med data från din miljö förutsäger tjänsten potentiella problem som kan uppstå och bli aktuella med Windows. Därefter föreslås eventuella begränsningar.  

- **Configuration Manager-integrering**: tjänst molnet – möjliggör din befintliga lokala infrastruktur. Använd dessa data och analyser för att distribuera och hantera Windows på dina enheter.  

## <a name="prerequisites"></a>Krav

Om du vill använda Desktop Analytics kontrollerar du att din miljö uppfyller följande krav.

### <a name="technical"></a>Teknik

- En aktiv Global Azure-prenumeration med [globala administratörs](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) behörigheter. [Microsoft-konton](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) stöds inte.  

    - **Ägarens behörigheter för arbets ytan** för att **Konfigurera din arbets yta**och följande roller:  

      - [**Administratörs roll för Skriv bords analys**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) .

      - [**Log Analytics deltagare**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) och [**användar åtkomst administratör**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) i resurs gruppen för att använda en befintlig arbets yta eller skapa en ny arbets yta i en befintlig resurs grupp.

      - [**Ägare**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)eller [**deltagare**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) och [**administratörs behörighet för användar åtkomst**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) på prenumerationen för att skapa en arbets yta i en ny resurs grupp.  

    - För att få åtkomst till portalen efter onboarding behöver du:

      - [**Administratörs rollen för Skriv bords Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) och [**ägare**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), eller [**deltagar**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) behörigheter på arbets ytan Log Analytics skapades.

- Configuration Manager version 1902 med Samlad uppdatering (4500571) eller senare. Mer information finns i [uppdatera Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - [**Fullständig administratörs**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) roll i Configuration Manager  

    > [!NOTE]
    > Desktop Analytics stöder flera Configuration Manager hierarkier som rapporterar till en enda Azure AD-klient.<!-- 4814075 --> Om du har flera hierarkier i din miljö har du följande alternativ:
    >
    > - Använd olika kommersiella ID: n och Azure AD-klienter.
    > - Konfigurera båda hierarkierna så att de använder samma kommersiella ID för att dela Azure AD-instansen och Desktop Analytics-instansen. Använd [olika appar](connect-configmgr.md#bkmk_connect) för att ansluta varje hierarki. Det kan ta upp till 30 dagar innan du kopplar från en hiearchy för portalen för att återspegla ändringarna. 

- Enheter som kör Windows 7, Windows 8,1 eller Windows 10  

    - Installera de senaste uppdateringarna. Mer information finns i [Uppdatera enheter](enroll-devices.md#update-devices).  

    - Enheter måste också ha Configuration Manager-klienten, version 1902 med Samlad uppdatering (4500571) eller senare. Mer information finns i [uppdatera Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics stöder inte uppgraderingar till Windows 10 långsiktig service Channel (LTSC). Mer information finns i [Översikt över Windows som en tjänst](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics är utformat för bästa möjliga uppgraderings scenario på plats. Om du behöver göra större ändringar, till exempel från 32-bitars till 64-bitars arkitektur, använder du ett avbildnings scenario. Desktop Analytics Insights är fortfarande värdefulla i de här klassiska scenarierna för operativ Systems distribution, men du kan ignorera den detaljerade vägledningen vid uppgradering på plats. Mer information finns i [scenarier för att distribuera operativ system i företag med Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Windows diagnostik-data. Mer information finns i följande artiklar:  

    - [Diagnostiska data nivåer](enable-data-sharing.md#diagnostic-data-levels)  

    - [Sekretess för Skriv bords analys](privacy.md)  

- Nätverks anslutning från enheter till det offentliga Microsoft-molnet. Mer information finns i [så här aktiverar du data delning](enable-data-sharing.md)  

> [!Important]
> Microsoft har ett kraftfullt engagemang för att tillhandahålla de verktyg och resurser som hjälper dig att kontrol lera din integritet. Därför samlar Microsoft inte in följande data från enheter som finns i Europeiska länder (EES och Schweiz):
>
> - Windows-diagnostikdata från Windows 8,1-enheter
> - Användnings data för appar för Windows 7

### <a name="licensing-and-costs"></a>Licensiering och kostnader

- En aktiv Global Azure-prenumeration.

    > [!NOTE]
    > De flesta av de motsvarande prenumerationerna för Configuration Manager inkluderar även Azure AD. Se till exempel [Microsoft 365 planer](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) och [Enterprise Mobility + Security licensiering](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Enheter som har registrerats i Skriv bords analys behöver en giltig Configuration Manager-licens. Mer information finns i [Configuration Manager licensiering](../core/understand/product-and-licensing-faq.md).

- Användare av enheten behöver någon av följande licenser:

  - Windows 10 Enterprise E3 eller E5 (ingår i Microsoft 365 F3, E3 eller E5)

  - Windows 10-utbildning a3 eller A5 (ingår i Microsoft 365 a3 eller A5)

  - Windows Virtual Desktop Access E3 eller E5  

> [!NOTE]
> Utöver kostnaden för dessa licens prenumerationer finns det ingen extra kostnad för att använda Desktop Analytics i Azure Log Analytics. De data typer som matas in av Skriv bords analys är kostnads fria från alla Log Analytics data inhämtning och avgifter för kvarhållning. Som data typer som inte är fakturerbara, omfattas dessa data inte heller av Log Analytics dagliga data inmatnings tak. Mer information finns i [Log Analytics användning och kostnader](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Nästa steg

Följande självstudie innehåller en steg-för-steg-guide för att komma igång med Desktop Analytics och Configuration Manager:
  
> [!div class="nextstepaction"]
> [Distribuera Windows 10 till en pilotgrupp](tutorial-windows10.md)
