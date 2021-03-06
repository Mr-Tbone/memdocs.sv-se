---
title: Vanliga frågor och svar om produkt och licensiering
titleSuffix: Configuration Manager
description: Hitta svar på vanliga produkt-och licens frågor för Configuration Manager.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: faf8401e6aa89a60f2acbea8e0d97f9efaf09a84
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994471"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Vanliga frågor och svar om Configuration Manager grenar och licenser

*Gäller för: Configuration Manager (aktuell gren) & System Center Configuration Manager (långsiktig service gren)*

Detta vanliga frågor och svar behandlar vanliga licens frågor om Configuration Manager aktuella gren-och LTSB-versioner (Long term Servicing Branch) som är tillgängliga via Microsofts volym licensierings program. Den här artikeln är i informations syfte. Den ersätter eller ersätter inte någon dokumentation som täcker Configuration Manager-licensiering. Mer information finns i [produkt villkoren](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Produkt villkoren beskriver användnings villkoren för alla Microsoft-produkter i volym licensiering.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> Vad är nuvarande gren?

Den aktuella grenen är den produktions färdiga versionen av Configuration Manager som tillhandahåller en aktiv underhålls modell. Den här underhålls modellen liknar upplevelsen med Windows 10. Den här metoden stöder kunder som flyttar i ett moln takt och vill förnya snabbare. Med den aktuella gren underhålls modellen fortsätter du att ta emot nya funktioner. Därför kan endast kunder med aktiv Software Assurance på Configuration Manager licenser eller med motsvarande prenumerations rättigheter installera och använda den aktuella grenen av Configuration Manager.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> Vad är LTSB (Long-term Servicing Branch)?  

LTSB är en produktions klar version av Configuration Manager. Den är avsedd för kunder som tillåter Software Assurance eller motsvarande prenumerations rättigheter att upphöra att gälla. Jämfört med den aktuella grenen har LTSB [begränsad funktionalitet](introduction-to-the-ltsb.md#features-that-arent-available). Kunder som tillåter att Software Assurance eller motsvarande prenumerations rättigheter upphör att gälla måste avinstallera den aktuella grenen av Configuration Manager. Kunder som har en beständig licens behörighet till Configuration Manager kan sedan installera och använda LTSB-versionen av den Configuration Manager versionen som är aktuell vid tidpunkten för förfallo datumet.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> Vad betyder förkortningarna *sa* och *L&sa* i förhållande till Configuration Manager?

Både **Software Assurance** (sa) och **licens-och Software assurance** (L&sa) är licens alternativ som ger behörighet att använda Configuration Manager. SA är ett alternativ för en kund som förnyar SA-täckningen från ett tidigare avtal. L&SA är ett alternativ för en kund som köper en ny licens och SA-täckning.

- **Software Assurance (sa)**: kunder måste ha aktiva sa på Configuration Manager licenser, eller motsvarande prenumerations rättigheter, för att kunna installera och använda alternativet för den aktuella grenen för Configuration Manager.

  Även om SA är valfritt för vissa Microsoft-produkter, är det enda sättet att få behörighet att använda Configuration Manager aktuella grenen är med SA *eller motsvarande prenumerations rättigheter*. Mer information finns i [vanliga frågor och svar om Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Microsoft licens-och Software Assurance (L&sa)**: kunder som köper nya licenser för Configuration Manager måste förvärva L&sa (licens-och sa-täckningen).

  - Säkerhets associationen ger behörighet att använda den aktuella grenen.

  - Om din SA upphör att gälla och du fortfarande har en licens för Configuration Manager, kan du inte längre använda den aktuella grenen. Mer information finns i vanliga frågor [och svar om min sa upphör att gälla och jag hade L&sa, vad får jag?](#bkmk_sa-expires)

För ytterligare information om licens erbjudanden, se [sätt att köpa](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) och [licensiera produkt villkor](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> Vad är *likvärdiga prenumerationer*?

Motsvarande prenumerationer avser program som [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) eller [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Det kan finnas andra, men de här programmen är de vanligaste. Microsofts produkt villkor för volym licensiering avser dessa program som motsvarande licenser för hanterings licenser.

Configuration Manager ingår i följande planer:

- Intune-dem (User Subscription License)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F3 (tidigare Microsoft 365 F1)

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager ingår inte i [Microsoft 365 Business Premium](https://www.microsoft.com/microsoft-365/business) -planen.

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> Vad är ändringar med licensiering för samhantering i Microsoft Endpoint Manager?

<!-- 7202432 -->

Med licens för samtidig hantering kan Configuration Manager kunder med Software Assurance få Intune-hanterings rättigheter utan att behöva köpa och tilldela enskilda Intune-licenser till användare. Den här licensen gör det enklare för dig att hantera Windows-enheter med Microsoft Endpoint Manager.

- Enheter som redan hanteras av Configuration Manager som du registrerar till Intune för samhantering har nästan samma rättigheter som en fristående Intune-hanterad dator. Om du återställer Windows på den här enheten kan du inte etablera den med Windows autopilot. Autopilot kräver en fullständig Intune-licens.

- Om du registrerar en Windows 10-enhet på Intune på annat sätt krävs en fullständig Intune-licens ändå. Du kan t. ex. använda autopilot för att etablera en enhet eller en användare som manuellt hanterar självbetjänings registrering.

- För befintliga Configuration Manager-hanterade enheter som ska registreras i Intune för samhantering i skala utan användar interaktion, använder Co-Management en Azure Active Directory (Azure AD) funktion som kallas Windows 10 Auto-registrering. Automatisk registrering med samhantering kräver licenser för både Azure AD Premium (AADP1) och Intune. Från den 1 december 2019 behöver du inte längre tilldela enskilda Intune-licenser för det här scenariot. Microsoft Endpoint Manager innehåller nu Intune-licenser för samhantering. Det separata licens kravet för AADP1 är detsamma för det här scenariot. Du måste fortfarande tilldela Intune-licenser för andra registrerings scenarier.

- Om du vill använda Intune för att hantera iOS-, Android-eller macOS-enheter behöver du en lämplig Intune-prenumeration via en fristående Intune-licens, Enterprise Mobility + Security (EMS) eller Microsoft 365.

- Om du inte har någon Intune-relaterad prenumerations plan för att stödja samhantering behöver du köpa minst en Intune-licens. Den här licensen är till för en administratör som aktiverar prenumerations planen och får åtkomst till administrations centret för Microsoft Endpoint Manager.

- Om du använder Microsoft 365 inbyggd [grundläggande mobilitet och säkerhet](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0)kan du inte använda den nya Co Management-licensen för en användare som också har enheter som hanteras av grundläggande mobilitet och säkerhet. Gör något av följande om du vill använda den tillsammanss hanterings licensen för användarens Configuration Manager-hanterade enhet:

  - Tilldela användaren en fullständig Intune-licens och hantera deras enheter via Intune.
  - Avregistrera enheterna från grundläggande mobilitet och säkerhet.

- Den licens som du tidigare hade för System Center Configuration Manager gäller fortfarande för Microsoft Endpoint Configuration Manager. Om du installerar en ny plats ska du använda befintliga produkt nycklar.

|Funktion | Licens för samtidig hantering | Fullständig Intune-licens |
|---------|---------|---------|
|Registrering av Windows 10|Ja (endast för befintliga ConfigMgr-hanterade enheter)|Ja|
|iOS, Android, macOS-registrering|Nej|Ja|
|Autopilot|Nej|Ja|
|Hantering av mobil program (MAM)|Nej|Ja|
|Villkorsstyrd åtkomst<br>(ytterligare AADP1 krävs)|Ja|Ja|
|Enhetsprofiler|Ja|Ja|
|Programuppdateringshanteraren|Ja|Ja|
|Inventering|Ja|Ja|
|Apphantering|Ja|Ja|
|Fullständig/selektiv rensning av fjärr anslutning|Ja|Ja|
|Fjärrhjälp<br>(TeamViewer-licens krävs)|Ja|Ja|
|Skriv bords analys<br>(Licenser för Windows-prenumeration krävs|Ja|Ej tillämpligt|
|Klientkoppling|Ja|Ej tillämpligt|
|Slutpunktsanalys|Ja|Ja|

Mer information finns i följande artiklar:

- [Krav för samhantering](../../comanage/overview.md#prerequisites)
- [Windows autopilot-krav](/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Krav för Skriv bords analys](../../desktop-analytics/overview.md#prerequisites)
- [Krav för klient anslutning](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Krav för slut punkts analys licensiering](../../../analytics/overview.md#licensing-prerequisites)
- [Använda villkorlig åtkomst med Intune](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [Krav för TeamViewer](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Jag har Enterprise Mobility + Security och det har gått ut, vad behöver jag göra nu?  

EMS ger rättigheter att använda Configuration Manager aktuell gren och långsiktig tjänst gren. När dessa rättigheter upphör att gälla har du inte längre behörighet att använda någon av grenarna och måste avinstallera.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> Om min SA upphör att gälla, och jag hade L&SA, vad får jag?

Om din SA upphör att gälla efter den 1 oktober 2016, beroende på vilket program du har köpt L&SA under, kan du behålla en beständig licens för att använda LTSB. Om du för närvarande använder den aktuella grenen måste du avinstallera den och sedan installera LTSB. Det finns inget stöd för att migrera eller konvertera till LTSB från den aktuella grenen.

Om din SA gick ut före den 1 oktober 2016 och du har bevarat en beständig licens till Configuration Manager, är ditt enda alternativ att installera och använda System Center 2012 R2 Configuration Manager och dess tillgängliga Service Pack. Du måste avinstallera den aktuella grenen när din SA upphör att gälla och installera om den tidigare versionen av produkten. Det finns inget stöd för att migrera till eller nedgradera från Configuration Manager aktuella grenen till tidigare versioner av Configuration Manager.

Om du använder System Center Endpoint Protection och din SA upphör att gälla måste du avinstallera den. System Center Endpoint Protection erbjuder inga *L-rättigheter (licens)* och ingen permanent behörighet.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> Äger jag den aktuella grenen?

Nej. Du är licensierad att använda den aktuella grenen när du har en aktiv säkerhets Association. Till exempel, via *L&sa*, när *sa* upphör att gälla, har du bara *L (licens)* -rättigheter, som inte omfattar rättigheter att använda den aktuella grenen. Om ditt L tillhandahåller permanent behörighet kan du använda Configuration Manager LTSB i stället för den aktuella grenen. Om din SA gick ut före den 1 oktober 2016 kan du också använda System Center 2012 R2 Configuration Manager.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> Kan jag köpa Configuration Manager fristående utan SA?

Nej. Det enda sättet att få behörighet att använda Configuration Manager är att skaffa en licens med SA eller genom en motsvarande prenumeration. Det finns program för utvecklare som MSDN där Configuration Manager erbjuds för utveckling och testning, men inte produktions användningen.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> Kräver en icke-produktions miljö för testning eller utveckling en explicit licens?

<!-- SCCMDocs#1848 -->

- Om du använder samma aktuella Branch-programvara som produktions miljö behöver du en explicit licens. Kontakta ditt konto team för att avgöra om ditt speciella licens avtal täcker flera instanser i flera miljöer.

- Vissa program för utvecklare som MSDN erbjuder produkter som Configuration Manager för utveckling och testning, men inte produktions användning.

- För en tillfällig miljö kan du använda [utvärderings versionen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) i 180 dagar.

- För en labb miljö kan du använda den [Technical Preview-grenen](../get-started/technical-preview.md). Technical Preview har samma funktioner som aktuell gren, men har vissa begränsningar vad gäller skala och plattformar som stöds.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> Har jag rättigheter att installera en uppdatering i Configuration Managers konsolen?

Om du har aktiva *sa*har du behörighet.

Om du inte har aktivt SA avinstallerar du den aktuella grenen och installerar sedan LTSB för Configuration Manager. LTSB tar inte emot uppdateringar för stegvisa versioner av Configuration Manager, men tar emot säkerhets uppdateringar baserat på support livs cykeln.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> Jag har köpt EMS eller Microsoft 365 via en moln lösnings leverantör (CSP), har jag behörighet att använda Configuration Manager?

Ja, du har behörighet att använda Configuration Manager för att hantera klienter som omfattas av EMS-licensen. Börja med att ladda ned och installera [utvärderings versionen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Kontakta sedan Microsoft Support för att få licens nyckeln.<!--issue472--> När du pratar med Microsoft Support ber du dem att referera till den interna artikeln ID 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> Är mitt prenumerations slut datum detsamma som förfallo datum för SA?

Om *sa* eller din prenumeration är aktiv, har du användnings rättigheter för Configuration Manager aktuella grenen. En aktiv prenumeration är motsvarigheten till att ha aktiva *sa*, men ingen beständig *"L" (licens)*. När prenumerationen är klar avinstallerar du den aktuella grenen. För tillfället har du inte behörighet att använda LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> Vilka är de användnings rättigheter som är kopplade till den SQL-teknik som medföljer Configuration Manager?

Configuration Manager innehåller SQL Server teknik. Microsofts licens villkor för den här produkten gör att du endast kan använda SQL Server-teknik för att stödja Configuration Manager-komponenter. SQL Server klient åtkomst licenser krävs inte för den här användningen.

Godkända användnings rättigheter för SQL-funktionerna med Configuration Manager inkluderar:

- Plats databas roll
- Windows Server Update Services (WSUS) för rollen program uppdaterings plats
- SQL Server Reporting Services (SSRS) för rapporterings plats roll
- Tjänst punkts roll för data lager
- Databas repliker för hanterings plats roller

Den SQL Server-licens som ingår i Configuration Manager stöder varje instans av SQL Server som du installerar som värd för en databas för Configuration Manager. Men endast databaser för Configuration Manager i föregående lista kan köras på den SQL Server när du använder den här licensen. Om en databas för ytterligare en produkt från Microsoft eller tredje part delar SQL Server måste du ha en separat licens för den SQL Server-instansen.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> Kräver lokal hantering av mobila enheter (MDM) en Intune-prenumeration?

I version 1806 och tidigare, för att börja använda lokal MDM, behöver du en Microsoft Intune prenumeration. Prenumerationen krävs endast för att spåra licensiering av enheterna och används inte för att hantera eller lagra hanterings information för enheterna. Alla hanterings data lagras i din organisation med hjälp av den lokala Configuration Managers infrastrukturen.  

Från och med version 1810 krävs en Intune-anslutning inte längre för nya lokala MDM-distributioner.<!--3607730, fka 1359124--> Din organisation kräver fortfarande Intune-licenser för att använda den här funktionen. Mer information finns i [blogg inlägget om Intune-support](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
