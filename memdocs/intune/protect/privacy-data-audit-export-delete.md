---
title: Granska, exportera eller ta bort personliga data
titleSuffix: Microsoft Intune
description: Lär dig hur du granskar, exporterar eller tar bort personliga data.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2bdf057893ff24cd4bc5b671d53fbb5c75f597f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996001"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Granska, exportera eller ta bort personliga data i Intune

Intune-administratörer kan använda spårningsloggar för att spåra aktiviteter som berör personliga data. Administratörer kan även exportera och ta bort personliga data.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Granska personliga data

Spårningsloggar ger klientorganisationsadministratörer en post med aktiviteter som genererar en ändring i Microsoft Intune. Spårningsloggarna är tillgängliga för många hanteringsaktiviteter, vanligtvis åtgärder för att skapa, uppdatera (redigera), ta bort och tilldela. Fjärråtgärder som genererar granskningshändelser kan också granskas. Dessa spårningsloggar kan innehålla personliga data från användare vars enheter har registrerats i Intune.  

Av säkerhetsskäl kan Intune bevara spårningsloggar för användar- och enhetsåtgärder i ett år. De här loggarna tas bort automatiskt efter kvarhållningsintervallet på ett år.

Om du vill granska spårningsloggar läser du [Spårningsloggar för Intune-aktiviteter](../fundamentals/monitor-audit-logs.md). 

Administratörer kan inte ta bort spårningsloggar.

Dessa spårningsloggar bevaras i ett år. Klientorganisationsadministratörer kan begära spårningsloggar med [det här formuläret för supportbegäran](https://privacy.microsoft.com/en-US/privacy-questions?).

## <a name="export-personal-data"></a>Exportera personliga data

Administratörer kan exportera slutanvändares personliga data, inklusive konton, tjänstdata och associerade loggar för att uppfylla DSR-begäranden (Data Subject Rights). Det är upp till dig och din organisation att bestämma om ni ska tillhandahålla den registrerade en kopia av personliga data eller om ni har ett giltigt affärsskäl att undanhålla dem. Om du vill tillhandahålla dem kan du ge den registrerade en kopia av det faktiska dokumentet, en korrekt redigerad version eller en skärmbild av de delar som du bedömer som lämpliga att dela.

Om du vill exportera en användares personliga data kan du använda: 
- Intune MDM-enhetsbladet för att exportera en lista över enheter. Du kan även kopiera enhetsdata direkt.
- [Export-IntuneData.ps1-skriptet](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Ta bort slutanvändares personliga data

Det finns tre sätt att ta bort personliga data från Intune-hantering:
- Ta bort användaren från Azure Active Directory
- Återställa enheten till fabriksinställningarna
- Självborttagning av användare

### <a name="delete-a-user-from-intune"></a>Ta bort en användare från Intune

För att en användares personliga data ska kunna tas bort från Intune måste en administratör [ta bort användaren från Azure Active Directory (AAD)](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user). När användaren tas bort från AAD (permanent borttagning) tar Intune emot borttagningssignalen från AAD och börjar sedan automatiskt att rensa alla användarens personliga data från Intune-tjänsten. Användarens information tas bort från Intune-tjänsten inom 30 dagar från borttagningsåtgärden.

### <a name="reset-device-to-factory-settings"></a>Återställa enhet till fabriksinställningarna
Återställning till fabriksinställningarna återställer alla företagsdata, personliga data och inställningar till de ursprungliga fabriksinställningarna. Det är användbart för att ge en enhet till en ny medarbetare. Användarfiler, användarinstallerade program och andra inställningar än standardinställningarna tas bort, och dessa data tas bort från Intune-tjänsten inom 30 dagar från borttagningsåtgärden.

### <a name="user-self-removal-from-intune-management"></a>Självborttagning av användare från Intune-hantering
Användare kan ta bort sin personliga [Android-, Apple- eller Windows-enhet](../user-help/unenroll-your-device-from-intune-android.md) från Intune-hantering utan hjälp från administratör.   

### <a name="retire"></a>Pensionera
Åtgärden **Dra tillbaka** tar bort Intune-etablerade data, till exempel företagsprogram, data om appar som Intune hanterar, principinställningar och e-postprofiler som etablerats via Intune. Med den här åtgärden lämnas användarens personliga data kvar på enheten.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Ta bort en klientorganisation från Microsoft Intune

Om en Intune-klientorganisationskund avbryter sitt Intune-konto tas alla klientorganisationsdata bort inom 180 dagar efter att kunden har stängt Intune-kontot. Om Azure AD-klientorganisationen är associerad med andra Microsoft-företagsprenumerationer (Azure, Microsoft 365) tas endast Intune-kunddata bort. Azure AD-klientorganisationsresursen underhålls för användning av de andra prenumerationerna. Om Intune-kontot är den enda prenumeration som associeras med Azure AD-klientorganisationen tas klientorganisationen bort, och alla resurser och kunddata tas också bort.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du [granskar, exporterar och tar bort](privacy-data-audit-export-delete.md) personliga data i Intune.