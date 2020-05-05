---
title: Vanliga frågor och svar om produkt och licensiering
titleSuffix: Configuration Manager
description: Hitta svar på vanliga produkt-och licens frågor för Configuration Manager.
ms.date: 02/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63e53c502e67d2bfbfc5f8a706006c6ec14f8fcd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722685"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Vanliga frågor och svar om Configuration Manager grenar och licenser

*Gäller för: Configuration Manager (aktuell gren) & System Center Configuration Manager (långsiktig service gren)*

Detta vanliga frågor och svar behandlar vanliga licens frågor om Configuration Manager aktuella gren-och LTSB-versioner (Long term Servicing Branch) som är tillgängliga via Microsofts volym licensierings program. Den här artikeln är i informations syfte. Den ersätter eller ersätter inte någon dokumentation som täcker Configuration Manager-licensiering. Mer information finns i [produkt villkoren](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Produkt villkoren beskriver användnings villkoren för alla Microsoft-produkter i volym licensiering.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a>Vad är nuvarande gren?

Den aktuella grenen är den produktions färdiga versionen av Configuration Manager som tillhandahåller en aktiv underhålls modell. Den här underhålls modellen liknar upplevelsen med Windows 10. Den här metoden stöder kunder som flyttar i ett moln takt och vill förnya snabbare. Med den aktuella gren underhålls modellen fortsätter du att ta emot nya funktioner. Därför kan endast kunder med aktiv Software Assurance på Configuration Manager licenser eller med motsvarande prenumerations rättigheter installera och använda den aktuella grenen av Configuration Manager.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a>Vad är LTSB (Long-term Servicing Branch)?  

LTSB är en produktions klar version av Configuration Manager. Den är avsedd för kunder som tillåter Software Assurance eller motsvarande prenumerations rättigheter att upphöra att gälla. Jämfört med den aktuella grenen har LTSB [begränsad funktionalitet](introduction-to-the-ltsb.md#features-that-arent-available). Kunder som tillåter att Software Assurance eller motsvarande prenumerations rättigheter upphör att gälla måste avinstallera den aktuella grenen av Configuration Manager. Kunder som har en beständig licens behörighet till Configuration Manager kan sedan installera och använda LTSB-versionen av den Configuration Manager versionen som är aktuell vid tidpunkten för förfallo datumet.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a>Vad betyder förkortningarna *sa* och *L&sa* i förhållande till Configuration Manager?

Både **Software Assurance** (sa) och **licens-och Software assurance** (L&sa) är licens alternativ som ger behörighet att använda Configuration Manager. SA är ett alternativ för en kund som förnyar SA-täckningen från ett tidigare avtal. L&SA är ett alternativ för en kund som köper en ny licens och SA-täckning.

- **Software Assurance (sa)**: kunder måste ha aktiva sa på Configuration Manager licenser, eller motsvarande prenumerations rättigheter, för att kunna installera och använda alternativet för den aktuella grenen för Configuration Manager.

  Även om SA är valfritt för vissa Microsoft-produkter, är det enda sättet att få behörighet att använda Configuration Manager aktuella grenen är med SA *eller motsvarande prenumerations rättigheter*. Mer information finns i [vanliga frågor och svar om Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Microsoft licens-och Software Assurance (L&sa)**: kunder som köper nya licenser för Configuration Manager måste förvärva L&sa (licens-och sa-täckningen).

  - Säkerhets associationen ger behörighet att använda den aktuella grenen.

  - Om din SA upphör att gälla och du fortfarande har en licens för Configuration Manager, kan du inte längre använda den aktuella grenen. Mer information finns i vanliga frågor [och svar om min sa upphör att gälla och jag hade L&sa, vad får jag?](#bkmk_sa-expires)

För ytterligare information om licens erbjudanden, se [sätt att köpa](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) och [licensiera produkt villkor](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a>Vad är *likvärdiga prenumerationer*?

Motsvarande prenumerationer avser program som [Enterprise Mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) eller [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Det kan finnas andra, men de här programmen är de vanligaste. Microsofts produkt villkor för volym licensiering avser dessa program som motsvarande licenser för hanterings licenser.

Configuration Manager ingår i följande planer:

- Intune-dem (User Subscription License)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F1

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager ingår inte i [Microsoft 365 businesss](https://www.microsoft.com/microsoft-365/business) planen.

### <a name="does-anything-change-with-the-rebrand-to-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a>Förändras allt med anpassningen till Microsoft Endpoint Manager?

Ja. Från den 1 december 2019, om du redan är licensierad för Configuration Manager, licensieras du också automatiskt för Intune för registrering av Windows-datorer i [samhantering](../../comanage/overview.md). Den här ändringen gör det enklare för dig att hantera Windows-enheter med Microsoft Endpoint Manager.

Nu finns en ny licens som låter Configuration Manager kunder med Software Assurance få Intune-hanterings rättigheter utan att behöva köpa ytterligare en Intune-licens för samhantering. Du behöver inte längre köpa och tilldela enskilda Intune-licenser till dina användare.

- Enheter som hanteras av Configuration Manager och som har registrerats i samhantering har nästan samma rättigheter som en fristående Intune-hanterad dator. När du återställer dem kan du dock inte etablera dem igen med hjälp av autopilot.

- Windows 10-enheter som har registrerats i Intune med hjälp av andra metoder kräver fullständiga Intune-licenser.

- Om du vill använda Intune för att hantera iOS-, Android-eller macOS-enheter behöver du en lämplig Intune-prenumeration genom en fristående Intune-licens, Enterprise Mobility + Security (EMS) eller Microsoft 365.

- Den licens som du tidigare hade för System Center Configuration Manager gäller fortfarande för Microsoft Endpoint Configuration Manager. Om du installerar en ny plats ska du använda befintliga produkt nycklar.

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a>Jag har Enterprise Mobility + Security och det har gått ut, vad behöver jag göra nu?  

EMS ger rättigheter att använda Configuration Manager aktuell gren och långsiktig tjänst gren. När dessa rättigheter upphör att gälla har du inte längre behörighet att använda någon av grenarna och måste avinstallera.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a>Om min SA upphör att gälla, och jag hade L&SA, vad får jag?

Om din SA upphör att gälla efter den 1 oktober 2016, beroende på vilket program du har köpt L&SA under, kan du behålla en beständig licens för att använda LTSB. Om du för närvarande använder den aktuella grenen måste du avinstallera den och sedan installera LTSB. Det finns inget stöd för att migrera eller konvertera till LTSB från den aktuella grenen.

Om din SA gick ut före den 1 oktober 2016 och du har bevarat en beständig licens till Configuration Manager, är ditt enda alternativ att installera och använda System Center 2012 R2 Configuration Manager och dess tillgängliga Service Pack. Du måste avinstallera den aktuella grenen när din SA upphör att gälla och installera om den tidigare versionen av produkten. Det finns inget stöd för att migrera till eller nedgradera från Configuration Manager aktuella grenen till tidigare versioner av Configuration Manager.

Om du använder System Center Endpoint Protection och din SA upphör att gälla måste du avinstallera den. System Center Endpoint Protection erbjuder inga *L-rättigheter (licens)* och ingen permanent behörighet.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a>Äger jag den aktuella grenen?

Nej. Du är licensierad att använda den aktuella grenen när du har en aktiv säkerhets Association. Till exempel, via *L&sa*, när *sa* upphör att gälla, har du bara *L (licens)* -rättigheter, som inte omfattar rättigheter att använda den aktuella grenen. Om ditt L tillhandahåller permanent behörighet kan du använda Configuration Manager LTSB i stället för den aktuella grenen. Om din SA gick ut före den 1 oktober 2016 kan du också använda System Center 2012 R2 Configuration Manager.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a>Kan jag köpa Configuration Manager fristående utan SA?

Nej. Det enda sättet att få behörighet att använda Configuration Manager är att skaffa en licens med SA eller genom en motsvarande prenumeration. Det finns program för utvecklare som MSDN där Configuration Manager erbjuds för utveckling och testning, men inte produktions användningen.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a>Kräver en icke-produktions miljö för testning eller utveckling en explicit licens?

<!-- SCCMDocs#1848 -->

- Om du använder samma aktuella Branch-programvara som produktions miljö behöver du en explicit licens. Kontakta ditt konto team för att avgöra om ditt speciella licens avtal täcker flera instanser i flera miljöer.

- Vissa program för utvecklare som MSDN erbjuder produkter som Configuration Manager för utveckling och testning, men inte produktions användning.

- För en tillfällig miljö kan du använda [utvärderings versionen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) i 180 dagar.

- För en labb miljö kan du använda den [Technical Preview-grenen](../get-started/technical-preview.md). Technical Preview har samma funktioner som aktuell gren, men har vissa begränsningar vad gäller skala och plattformar som stöds.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a>Har jag rättigheter att installera en uppdatering i Configuration Managers konsolen?

Om du har aktiva *sa*har du behörighet.

Om du inte har aktivt SA avinstallerar du den aktuella grenen och installerar sedan LTSB för Configuration Manager. LTSB tar inte emot uppdateringar för stegvisa versioner av Configuration Manager, men tar emot säkerhets uppdateringar baserat på support livs cykeln.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a>Jag har köpt EMS eller Microsoft 365 via en moln lösnings leverantör (CSP), har jag behörighet att använda Configuration Manager?

Ja, du har behörighet att använda Configuration Manager för att hantera klienter som omfattas av EMS-licensen. Börja med att ladda ned och installera [utvärderings versionen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Kontakta sedan Microsoft Support för att få licens nyckeln.<!--issue472--> När du pratar med Microsoft Support ber du dem att referera till den interna artikeln ID 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a>Är mitt prenumerations slut datum detsamma som förfallo datum för SA?

Om *sa* eller din prenumeration är aktiv, har du användnings rättigheter för Configuration Manager aktuella grenen. En aktiv prenumeration är motsvarigheten till att ha aktiva *sa*, men ingen beständig *"L" (licens)*. När prenumerationen är klar avinstallerar du den aktuella grenen. För tillfället har du inte behörighet att använda LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a>Vilka är de användnings rättigheter som är kopplade till den SQL-teknik som medföljer Configuration Manager?

Configuration Manager innehåller SQL Server teknik. Microsofts licens villkor för den här produkten gör att du endast kan använda SQL Server-teknik för att stödja Configuration Manager-komponenter. SQL Server klient åtkomst licenser krävs inte för den här användningen.

Godkända användnings rättigheter för SQL-funktionerna med Configuration Manager inkluderar:

- Plats databas roll
- Windows Server Update Services (WSUS) för rollen program uppdaterings plats
- SQL Server Reporting Services (SSRS) för rapporterings plats roll
- Tjänst punkts roll för data lager
- Databas repliker för hanterings plats roller

Den SQL Server-licens som ingår i Configuration Manager stöder varje instans av SQL Server som du installerar som värd för en databas för Configuration Manager. Men endast databaser för Configuration Manager i föregående lista kan köras på den SQL Server när du använder den här licensen. Om en databas för ytterligare en produkt från Microsoft eller tredje part delar SQL Server måste du ha en separat licens för den SQL Server-instansen.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a>Kräver lokal hantering av mobila enheter (MDM) en Intune-prenumeration?

I version 1806 och tidigare, för att börja använda lokal MDM, behöver du en Microsoft Intune prenumeration. Prenumerationen krävs endast för att spåra licensiering av enheterna och används inte för att hantera eller lagra hanterings information för enheterna. Alla hanterings data lagras i din organisation med hjälp av den lokala Configuration Managers infrastrukturen.  

Från och med version 1810 krävs en Intune-anslutning inte längre för nya lokala MDM-distributioner.<!--3607730, fka 1359124--> Din organisation kräver fortfarande Intune-licenser för att använda den här funktionen. Mer information finns i [blogg inlägget om Intune-support](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).
