---
title: Vad är apphantering i Microsoft Intune?
titleSuffix: ''
description: Läs mer om klientappens hanteringsfunktioner per plattform i Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/05/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98eba2cd2905a70157cfb50299bb9b11a6319fcc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342341"
---
# <a name="what-is-microsoft-intune-app-management"></a>Vad är apphantering i Microsoft Intune?


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Som IT-administratör kan du använda Microsoft Intune för att hantera klientappar som ditt företags personal använder. Den här funktionen är ett tillägg till hanteringen av enheter och att skydda data. En av en administratörs prioriteringar är att säkerställa att användarna har åtkomst till appar som de behöver för att utföra sitt arbete. Detta mål kan vara en utmaning eftersom:
- Det finns en mängd olika enhetsplattformar och apptyper.
- Du kan behöva hantera appar på både företagets enheter samt på användarnas personalenheter.
- Du måste se till att ditt nätverk och dina data förblir säkra.

Dessutom kanske du vill tilldela och hantera appar på enheter som inte har registrerats med Intune.

## <a name="mobile-application-management-mam-basics"></a>Grunderna inom hantering av mobilprogramsappar (MAM, Mobile Application Management)

Med [Intune mobile application management](app-lifecycle.md) avses den svit av Intune-hanteringsfunktioner som låter dig publicera, pusha, konfigurera, skydda, övervaka och uppdatera mobilappar för dina användare.

Med MAM kan du hantera och skydda din organisations data i ett program. Med **MAM utan registrering** (MAM-WE), kan en arbets- eller skolrelaterad app som innehåller känsliga data hanteras på nästan alla [enheter](app-management.md#app-management-capabilities-by-platform), inklusive personliga enheter i **BYOD-scenarier** (Bring Your Own Device). Många produktivitetsappar, till exempel Microsoft Office-apparna, kan hanteras av Intune MAM. Se listan över officiella [MicrosoftIntune-skyddade appar](apps-supported-intune-apps.md) tillgängliga för allmänt bruk.

Intune MAM stöder två konfigurationer:
- **Intune MDM + MAM**: IT-administratörer kan bara hantera appar med hjälp av MAM och appskyddsprinciper på enheter som registreras med Intune mobile device management (MDM). För att hantera appar med hjälp av MDM + MAM, ska kunder använda Intune-konsolen i Azure-portalen på https://portal.azure.com.
- **MAM utan enhetsregistrering**: Med MAM utan enhetsregistrering, eller MAM-WE, kan IT-administratörer hantera appar med hjälp av MAM och appskyddsprinciper på enheter som inte har registrerats med Intune MDM. Detta innebär att appar kan hanteras av Intune på enheter som registrerats med tredje parts EMM-leverantörer. För att hantera appar med hjälp av MAM-WE, ska kunder använda Intune-konsolen i Azure-portalen på https://portal.azure.com. Appar kan också hanteras av Intune på enheter som har registrerats med tredje parts-leverantörer av Enterprise Mobility Management (EMM) eller inte har registrerats alls med MDM. Mer information om BYOD och Microsofts EMS finns i [Teknikval för att kunna tillämpa BYOD med Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## <a name="app-management-capabilities-by-platform"></a>Apphanteringsfunktioner efter plattform

Intune erbjuder en mängd funktioner som hjälper dig att få de appar som du behöver, på de enheter som du önskar köra dem på. Följande tabell innehåller en sammanfattning av apphanteringsfunktionerna.

|  | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| Lägga till och tilldela appar till enheter och användare | Ja | Ja | Ja | Ja | Ja |
| Tilldela appar till enheter som inte registrerats i Intune | Ja | Ja | Nej | Nej | Nej |
| Använda principer för appkonfigurering som styr apparnas startfunktion | Ja | Ja | Nej | Nej | Nej |
| Använda principer för etablering av mobilappar för att förnya utgångna appar | Nej | Ja | Nej | Nej | Nej |
| Skydda företagets data i appar med appskyddsprinciper | Ja | Ja | Nej | Nej <sup>1</sup> | Nej |
| Ta bort endast företagsdata från installerade appar (selektiv rensning) | Ja | Ja | Nej | Ja | Ja |
| Övervaka apptilldelningar | Ja | Ja | Ja | Ja | Ja |
| Tilldela och spåra volyminköpta appar från en appbutik | Nej | Nej | Nej | Ja | Nej |
| Obligatorisk installation av appar på enheter (obligatoriskt) <sup>2</sup> | Ja | Ja | Ja | Ja | Ja |
| Valfri installation på enheter från Företagsportalen (tillgänglig installation) | Ja <sup>3</sup> | Ja | Ja | Ja | Ja |
| Installera genvägar till appar på webben (webblänk) | Ja <sup>4</sup> | Ja | Ja | Ja | Ja |
| Verksamhetsspecifika appar | Ja | Ja | Ja | Ja | Nej |
| Appar från en butik | Ja | Ja | Nej | Ja | Ja |
| Uppdatera appar | Ja | Ja | Nej | Ja | Ja |

<sup>1</sup> Överväg att använda [Windows informationsskydd](../protect/windows-information-protection-configure.md) för att skydda appar på enheter som kör Windows 10.<br>
<sup>2</sup> Gäller enheter som hanteras av Intune endast.<br>
<sup>3</sup> Intune har stöd för tillgängliga appar från Google Play Store för företag på Android Enterprise-enheter.<br>
<sup>4</sup> Intune tillhandahåller inte installation av en genväg till en app som en webblänk på vanliga Android-Enterprise-enheter. Stöd för webblänkar finns dock för [dedikerade Android Enterprise-enheter med flera appar](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings). 


## <a name="get-started"></a>Kom igång

Du hittar den mesta apprelaterade informationen i arbetsbelastningen **Appar** som du öppnar på följande sätt:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Appar**.

    ![Arbetsbelastningsfönstret Appar](./media/app-management/apps-workload.png)

Apparbetsbelastningen innehåller länkar till allmän information om appar och funktioner. 

Överst i navigeringsmenyn för apparbetsbelastningen finns ofta använd appinformation:
- **Översikt**: Välj det här alternativet om du vill visa klientorganisationens namn, MDM-utfärdare, klientplats, kontostatus, appinstallationsstatus och status för programskyddsprincip.
- **Alla appar**: Välj det här alternativet om du vill visa en lista över alla tillgängliga appar. Du kan lägga till ytterligare appar från den här sidan. Dessutom kan du se status för varje app och även se om en app är tilldelad. Mer information finns i [Lägg till appar](apps-add.md) och [Tilldela appar](apps-deploy.md).
- **Övervaka appar**
    - **Applicenser**: Visa, tilldela och övervaka volyminköpta appar från appbutiker. Mer information finns i [iOS-appar i volymköpprogrammet (VPP)](vpp-apps-ios.md) och [volymköpta appar från Windows Store för företag](windows-store-for-business.md).
    - **Identifierade appar**: Visa appar som har tilldelats av Intune eller installerats på en enhet. Mer information finns i [Appar som identifieras i Intune](app-discovered-apps.md).
    - **Status för appinstallation**: Visa status för en apptilldelning som du har skapat. Mer information finns i [Övervaka appinformation och tilldelningar med Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **Appskyddsstatus**: Visa status för en appskyddsprincip hos en användare som du väljer.
- **Per plattform**: Välj de här plattformarna om du vill visa tillgängliga appar efter plattform.
    - Windows
    - iOS
    - macOS
    - Android
- **Princip**:
    - **Appskyddsprinciper**: Välj det här alternativet för att koppla inställningar till en app och skydda de data som företaget använder. Du kan till exempel begränsa möjligheterna för en app att kommunicera med andra appar eller du kan kräva att användaren anger en PIN-kod för att få åtkomst till en företagsapp. Mer information finns i [Appskyddsprinciper](app-protection-policies.md).
    - **Appkonfigurationsprinciper**: Välj det här alternativet om du vill ange inställningar som kan krävas när en användare kör en app. Mer information finns i [Appkonfigurationsprinciper](app-configuration-policies-use-ios.md), [Konfigurationsprinciper för iOS-appar](app-configuration-policies-use-ios.md) och [Konfigurationsprinciper för Android-appar](app-configuration-policies-overview.md).
    - **Etableringsprofiler för iOS-app**: iOS-appar innehåller en etableringsprofil och en kod som har signerats av ett certifikat. När certifikatet upphör att gälla kan du inte längre köra appen. Intune tillhandahåller verktyg för att tilldela en ny etableringsprofilprincip till enheter som har appar som snart upphör att gälla. Mer information finns i [etableringsprofilerna för iOS-appar](app-provisioning-profile-ios.md).
    - **Tilläggsprinciper för S-läge**: Välj det här alternativet om du vill tillåta att fler program körs på dina hanterade S-lägesenheter. Mer information finns i [Tilläggsprinciper för S-läge](apps-win32-s-mode.md).
    - **Principuppsättningar**: Välj det här alternativet om du vill skapa en tilldelningsbar samling appar, principer och andra hanteringsobjekt som du har skapat. Mer information finns i [Principuppsättningar](../fundamentals/policy-sets.md).
- **Andra**:   
    - **Selektiv radering av app**: Välj det här alternativet för att ta bort enbart företagsdata från en vald användares enhet. Mer information finns i [Selektiv appradering](apps-selective-wipe.md).
    - **Appkategorier**: Lägg till, fäst och ta bort appkategorinamn.
    - **E-böcker**: En del appbutiker erbjuder möjligheten att köpa flera licenser till en app eller bok som du vill köra i företaget. Mer information finns i [Hantera volyminköpta appar och böcker med Microsoft Intune](vpp-apps.md).
- **Hjälp och support**: Felsök, begär support eller visa Intunes status. Mer information finns i [Felsöka problem](../fundamentals/help-desk-operators.md).

## <a name="additional-information"></a>Ytterligare information
Följande objekt i konsolen tillhandahåller apprelaterade funktioner:
- **Microsoft Store för företag**: Konfigurera integration till Microsoft Store för företag. När du gjort detta kan du synkronisera inköpta program till Intune, tilldela dem och spåra användningen av licenser. Mer information finns i [Volymköpta appar från Windows Store för företag](windows-store-for-business.md).
- **Windows företagscertifikat**: Tillämpa eller visa status för ett kodsigneringscertifikat som används för att distribuera verksamhetsspecifika appar till dina hanterade Windows-enheter.
- **Windows Symantec-certifikat**: Tillämpa eller visa status för ett Symantec-kodsigneringscertifikat som behövs för att distribuera XAP- och WP8.x appx-filer till Windows 10 Mobile-enheter.
- **Windows-nycklar för separat inläsning**: Lägg till en Windows-nyckel för separat inläsning som kan användas för att installera en app direkt till enheter, i stället för att appen publiceras och hämtas från Windows Store. Mer information finns i [Separat inläsning av en Windows-app](app-sideload-windows.md).
- **Apple VPP-token**: Tillämpa och visa dina licenser för iOS/iPadOS-volymköpsprogrammet (VPP). Mer information finns i [Volyminköpta iOS/iPadOS-appar](vpp-apps-ios.md).
- **Hanterat Google Play**: Google Play för företag är Googles appbutik för företag och den enda källan till appar för Android Enterprise. Du hittar mer information i [Lägg till hanterade Google Play-appar till Android enterprise-enheter med Intune](apps-add-android-for-work.md).
- **Varumärken och anpassning**: Anpassa företagsportalen efter ert varumärke. Mer information finns i [Konfiguration av Företagsportal](company-portal-app.md).

## <a name="next-steps"></a>Nästa steg

- [Lägg till en app i Microsoft Intune](apps-add.md)
