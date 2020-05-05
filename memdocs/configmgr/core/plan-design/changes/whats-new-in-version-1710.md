---
title: Ny version 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1710 av Configuration Manager.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073627"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Vad&#39;s nya i version 1710 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1710 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1610, 1702 eller 1706.

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Följande ytterligare uppdateringar av den här versionen är nu tillgängliga:
- [Samlad uppdatering för Configuration Manager aktuell gren, version 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Samlad uppdatering 2 för Configuration Manager aktuella grenen, version 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Om du vill installera en ny plats måste du använda en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1710 av Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Plats infrastruktur

### <a name="updates-for-peer-cache-----sms500850---"></a>Uppdateringar för peer-cache  <!-- sms500850 -->
Från och med den här versionen är peer-cache inte längre en för hands versions funktion.  Inga andra ändringar för peer-cachen introduceras i den här versionen. Mer information finns i [peer-cache för Configuration Manager klienter](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Distributions plats stöd i molnet för Azure Government Cloud   <!-- sms491428 -->
Nu kan du använda [molnbaserade distributions platser](../hierarchy/use-a-cloud-based-distribution-point.md) i Azure Government molnet.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Inventering av standard enhets revision <!-- sms503697 -->
Eftersom enheterna nu inkluderar hård diskar med storlekar i GB (GB), terabyte (TB) och större skalor, ändrar den här versionen standardenheten (SMS_Units) som används i många vyer från megabyte (MB) till GB. Till exempel kan värdet för v_gs_LogicalDisk. ledigt utrymme nu rapporter GB enheter.


<!-- ## Migration  -->


## <a name="client-management"></a>Klienthantering

### <a name="co-management-for-windows-10-devices"></a>Samhantering för Windows 10-enheter    
<!-- 1350871 -->
I de tidigare Windows 10-uppdateringarna kan du redan ansluta en Windows 10-enhet till en lokal Active Directory (AD) och molnbaserad Azure AD samtidigt (hybrid Azure AD). Från och med Configuration Manager version 1710 drar samhanteringen nytta av den här förbättringen och gör att du samtidigt kan hantera Windows 10, version 1709 (kallas även skapare Creators Update)-enheter med hjälp av både Configuration Manager och Intune. Det är en lösning som ger en brygga från traditionell till modern hantering och ger dig en sökväg för att göra över gången med en stegvis metod. Mer information finns i [Co-Management för Windows 10-enheter](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Starta om datorer från Configuration Manager-konsolen  <!-- 1356283 -->
Från och med den här versionen kan du använda Configuration Manager-konsolen för att identifiera klient enheter som kräver en omstart och sedan använda en klient meddelande åtgärd för att starta om dem.

Se [Hantera klienter](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Programhantering
### <a name="improvements-for-run-scripts------1236459---"></a>Förbättringar för körning av skript   <!-- 1236459 -->
Den här versionen ger flera förbättringar av funktionen **Kör skript** , som gör att du kan distribuera PowerShell-skript för att köra på hanterade enheter. Den här funktionen introducerades först i version 1706.

Förbättringarna är:
- Använd säkerhets omfattningar för att kontrol lera vem som kan använda kör skript
- Real tids övervakning av de skript som du kör
- Parametrar för skript visning i guiden skapa skript, stöd för verifiering och identifieras som obligatoriska eller valfria.

Mer information om hur du använder kör skript finns i [skapa och köra skript](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nya princip inställningar för hantering av mobil program
<!-- 1324760 -->
Följande inställningar har lagts till i princip inställningarna för hantering av mobil program:
- **Inaktivera synkronisering av kontakter**: förhindrar att appen sparar data till den interna appen Kontakter på enheten.
- **Inaktivera utskrift**: förhindrar att appen skriver ut arbets-eller skol data.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center förvränger inte längre ikoner som är större än 250x250  
<!-- 1356194 -->

I den här versionen kommer Software Center inte längre att snedvrida ikoner som är större än 250x250. Software Center gjorde sådana ikoner mer suddiga. Nu kan du ange en ikon med en pixel dimension på upp till 512x512 och den visas utan förvrängning.

Information om hur du lägger till en ikon för din app i Software Center finns i [skapa program](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>Distribution av operativsystem
 > [!TIP]   
 > <!-- 1354281 -->
 > Från och med Windows 10, version 1709 (kallas även skapare Creators Update), innehåller Windows Media flera versioner. När du konfigurerar en aktivitetssekvens för att använda ett uppgraderings paket för operativ system eller en operativ system avbildning måste du välja en [version som stöds för användning av Configuration Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Lägg till underordnade aktivitetssekvenser i en aktivitetssekvens
<!-- 1261338 -->

Du kan lägga till ett nytt steg i aktivitetssekvensen som kör en annan aktivitetssekvens, vilket skapar en överordnad/underordnad relation mellan aktivitetssekvenser. På så sätt kan du skapa fler modulära aktivitetssekvenser som du kan använda igen.  

Om du vill veta mer om den underordnade aktivitetssekvensen, se [underordnad](../../../osd/understand/task-sequence-steps.md#child-task-sequence)aktivitetssekvens.

## <a name="software-center-customization"></a>Anpassning av Software Center
<!-- 1351224 -->
Du kan lägga till företags anpassnings element och ange synlighet för flikar i Software Center. Du kan lägga till ett visst företags namn för Software Center, ange ett färg schema för Software Center-konfiguration, ange en företags logo typ och ange de synliga flikarna för klient enheter.

Mer information finns i [Planera för och konfigurera program hantering](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Programuppdateringar

### <a name="surface-driver-updates-----1098490---"></a>Uppdateringar av Surface-drivrutin  <!-- 1098490 -->
Från och med den här versionen är hantering av driv rutins uppdateringar inte längre en för hands versions funktion.  


## <a name="reporting"></a>Rapportering

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Begränsa Windows 10 Enhanced data så att endast data som är relevanta för Windows Analytics skickas Enhetens hälsotillstånd
<!-- 1356148 -->

Nu kan du ange att Windows 10-diagnostikens data insamlings nivå ska bli **utökad (begränsad)**. Med den här inställningen kan du få användbara insikter om enheter i din miljö utan att enheterna rapporterar alla data på den **förbättrade** nivån med Windows 10 version 1709 eller senare.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Hantering av mobila enheter

### <a name="actions-for-non-compliance"></a>Åtgärder vid inkompatibilitet 
<!--1321366 -->    
Nu kan du konfigurera en tidsordnad sekvens med åtgärder som tillämpas på enheter som inte uppfyller kraven. Du kan till exempel meddela användare av icke-kompatibla enheter via e-post eller markera enheterna som inte är kompatibla.

### <a name="windows-10-arm64-device-support"></a>Stöd för Windows 10 ARM64-enheter
<!-- 1355000 -->

Hanterings scenarier för Hybrid mobil enheter (MDM) stöds på ARM64-enheter som kör Windows 10 när enheterna är tillgängliga.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Förbättrad VPN-profil i Configuration Manager-konsolen 
<!-- 1318232 -->

I den här versionen har vi uppdaterat guiden VPN-profil och egenskaps sidor för att visa lämpliga inställningar för den valda plattformen:


- Varje plattform har sitt eget arbets flöde, vilket innebär att nya VPN-profiler bara innehåller inställningen som stöds av plattformen.
- Sidan **plattformar som stöds** visas nu efter sidan **Allmänt** .  Nu väljer du plattform innan du anger egenskaps värden.
- När plattformen är inställd på **Android**, **Android for Work**eller **Windows Phone 8,1**behövs inte sidan **plattformar som stöds** och visas inte.
- Det Configuration Manager klientbaserade arbets flödet har kombinerats med klientbaserade Windows 10-arbetsflöden (hybrid Mobile Device). de har stöd för samma inställningar.
- Varje plattforms arbets flöde innehåller bara de inställningar som är lämpliga för det arbets flödet.  Android-arbetsflödet innehåller till exempel inställningar som är lämpliga för Android. inställningar som är lämpliga för iOS eller Windows 10 Mobile visas inte längre i Android-arbetsflödet.
- Den automatiska VPN-sidan är föråldrad och har tagits bort.

Dessa ändringar gäller för nya VPN-profiler.  

För att minimera kompatibiliteten är befintliga VPN-profiler oförändrade.  När du redigerar en befintlig profil visas inställningarna som de gjorde när profilen skapades.  

Mer information finns i [VPN-profiler på mobila enheter](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Begränsat stöd för kryptografi: CNG-certifikat (Next Generation) <!-- 1356191 -->

Configuration Manager har begränsat stöd för kryptografi: CNG-certifikat (Next Generation). Configuration Manager klienter kan använda certifikat för PKI-klientautentisering med privat nyckel i CNG Key Storage Provider (KSP). Med KSP-stöd har Configuration Manager-klienter stöd för maskinvarubaserad privat nyckel, t. ex. TPM-KSP för certifikat för PKI-klientautentisering.

Mer information finns i [Översikt över CNG-certifikat](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Skydda enheter

### <a name="create-and-deploy-exploit-guard-policies"></a>Skapa och distribuera sårbarhets Guard-principer
<!-- 1355468 -->

Du kan [skapa och distribuera principer](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) som hanterar alla fyra komponenter i Windows Defender sårbarhets Guard, inklusive minskning av attack ytan, styrd mappåtkomst, sårbarhets skydd och nätverks skydd.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Skapa och distribuera Windows Defender Application Guard-princip
<!-- 1351960 -->

Du kan [skapa och distribuera Windows Defender Application Guard-principer](../../../protect/deploy-use/create-deploy-application-guard-policy.md) med hjälp av Configuration Manager Endpoint Protection.

### <a name="device-guard-policy-changes"></a>Ändringar i Device Guard-princip
<!-- 1355092 -->
Följande tre ändringar har gjorts i förhållande till Device Guard-principer:

- Device Guard-principer har bytt namn till Windows Defender program kontroll principer. Till exempel heter **guiden skapa enhets skydds princip** guiden **skapa Windows Defender Application Control-princip**.
- Enheter som använder uppdateringarna för Windows-version 1709 kräver ingen omstart för att tillämpa Windows Defender-program kontroll principer. Omstart är fortfarande standard, men du kan [inaktivera omstarter](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- Du kan [ställa in enheter för att automatiskt köra program vara](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) som är betrodd av intelligent Security Graph.





## <a name="next-steps"></a>Nästa steg
När du är redo att installera den här versionen, se [uppdateringar för Configuration Manager](../../servers/manage/updates.md).
