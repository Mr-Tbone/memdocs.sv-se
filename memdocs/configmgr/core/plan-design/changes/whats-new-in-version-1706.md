---
title: Ny version 1706
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1706 av Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2e823aad8fcf69861d21a99f0e65dcf8aaa40dcd
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993394"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Vad&#39;s nya i version 1706 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1706 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1606, 1610 eller 1702.

> [!TIP]  
> Om du vill installera en ny plats måste du använda en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)  

Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1706 av Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Plats infrastruktur

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-microsoft-365"></a>Stöd för klient-peer-cache för Express-installationsfiler för Windows 10 och Microsoft 365  
<!-- 1352486 -->
Från och med den här versionen stöder peer-cache distribution av installationsfiler för innehålls Express för Windows 10 och uppdaterings filer för Microsoft 365. Det krävs inga ytterligare konfigurationer för att stödja den här ändringen.

### <a name="updates-for-the-data-warehouse"></a>Uppdateringar för data lagret
<!-- 1277922 -->
Data lagret är inte längre en för hands versions funktion. Vi har även uppdaterat kraven för att inkludera stöd för databasen på SQL Server Always on-tillgänglighetsgrupper och redundanskluster. Mer information finns i [informations lager service platsen](../../servers/manage/data-warehouse.md).

### <a name="accessibility-improvements"></a>Förbättrad användbarhet
<!-- 1253000 -->
Vi har lagt till ytterligare förbättringar av hjälpmedel för Configuration Manager-konsolen. Mer information finns i [hjälpmedels funktioner](../../understand/accessibility-features.md).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Förbättringar för SQL Server Always on-tillgänglighetsgrupper
<!-- 1352094 -->
Med den här versionen kan du nu använda asynkrona inchecknings repliker i SQL Server Always on-tillgänglighetsgrupper som du använder med Configuration Manager. Det innebär att du kan lägga till fler repliker i dina tillgänglighets grupper som du kan använda som fjärranslutna platser och sedan använda dem i ett katastrof återställnings scenario.  
- Configuration Manager stöder användningen av den asynkrona commit-replikeringen för att återställa din synkrona replik. Se [återställnings alternativ för plats databas](../../servers/manage/recover-sites.md#site-database-recovery-options) i avsnittet säkerhets kopiering och återställning för information om hur du kan göra detta.
- Den här versionen stöder inte redundans för att använda den asynkrona commit-repliken som plats databas.
Mer information finns i [förbereda för att använda Always on-tillgänglighetsgrupper](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="update-reset-tool"></a>Uppdateringsverktyg för återställning
<!-- 1324589 -->
Från och med version 1706 innehåller Configuration Manager primära platser och Central administrations plats verktyget Configuration Manager uppdaterings återställning **CMUpdateReset.exe**. Använd det här verktyget med alla versioner av den aktuella grenen som finns kvar i supporten för att åtgärda problem när uppdateringar i konsolen har problem med att ladda ned eller replikera. Mer information finns i [Uppdatera återställnings verktyget](../../servers/manage/update-reset-tool.md).

### <a name="high-dpi-console-support"></a>Stöd för hög DPI-konsol  
<!-- 1353476 -->
I den här versionen, problem med hur Configuration Manager-konsolen skalar och visar olika delar av användar gränssnittet när de visas på hög DPI-enheter (t. ex. en Surface Book) bör åtgärdas.

### <a name="improved-boundary-groups-for-software-update-points"></a>Förbättrade avgränsnings grupper för program uppdaterings platser
<!-- 1324591 -->
Den här versionen innehåller förbättringar för hur program uppdaterings platser fungerar med gränser grupper. Följande sammanfattar det nya återställnings beteendet:
- Återställningen för program uppdaterings platser använder nu en konfigurerbar tid för att återgå till intilliggande gräns grupper.
- Oberoende av återställnings konfigurationen försöker en klient komma åt den senaste program uppdaterings platsen som den använde i 120 minuter. Efter att ha misslyckats med att kontakta servern i 120 minuter, kontrollerar klienten sin pool med tillgängliga program uppdaterings platser så att den kan hitta en ny.
- Efter att ha misslyckats med att komma åt den ursprungliga servern i två timmar växlar klienten till en kortare cykel för att kontakta en ny program uppdaterings plats. Det innebär att om en klient inte kan ansluta till en ny server, väljer den snabbt nästa server från poolen med tillgängliga servrar och försöker kontakta den.

Mer information finns i [program uppdaterings platser](../../servers/deploy/configure/boundary-groups.md#bkmk_sup) i avsnittet gränser grupper för Current Branch.

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD-integrering med Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
I den här versionen har vi förbättrat integreringen av Configuration Manager och Azure Active Directory (Azure AD).  Dessa förbättringar effektiviserar hur du konfigurerar de Azure-tjänster som du använder med Configuration Manager och hjälper dig att hantera klienter och användare som autentiseras med Azure AD.

Den förbättrade integrationen gör följande möjligt:  
- Guiden Azure-tjänster – i den här guiden får du en gemensam konfigurations upplevelse som ersätter de enskilda arbets flödena och konfigurerar följande Azure-tjänster som du använder med Configuration Manager.
  - **Moln hantering** Aktivera klienter för autentisering med hjälp av Azure Active Directory (Azure AD). Du kan också konfigurera identifiering av Azure AD-användare.
  - **Log Analytics koppling** Anslut till Azure Log Analytics och synkronisera samlings data.
  - **Uppgraderingsberedskap** Anslut till Uppgraderingsberedskap och Visa information om klient uppgradering – kompatibilitet.
  - **Windows Store för företag** Anslut till Online Store för Windows Store för företag och hämta appar för din organisation som du kan distribuera med Configuration Manager.


  Detta görs med hjälp av en [Azure-webbapp](/azure/app-service/app-service-authentication-overview) för att tillhandahålla prenumerations-och konfigurations information som du annars anger varje gången du konfigurerar en ny Configuration Manager komponent eller tjänst med Azure. Mer information finns i [guiden Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md).

- Använd Azure AD för att autentisera klienter på Internet för att få åtkomst till dina Configuration Manager-platser. Azure AD ersätter behovet av att konfigurera och använda certifikat för klientautentisering. Detta kräver plats system rollen för Cloud Management Gateway. Mer information finns i [Installera och tilldela Configuration Manager-klienter från Internet med Azure AD för autentisering](../../clients/deploy/deploy-clients-cmg-azure.md).

- Installera och hantera Configuration Manager-klienten på datorer som finns på Internet. Detta kräver att plats system rollen för Cloud Management Gateway används. Mer information finns i [Installera och tilldela Configuration Manager-klienter från Internet med Azure AD för autentisering](../../clients/deploy/deploy-clients-cmg-azure.md).

- Konfigurera identifiering av Azure AD-användare.  Använd guiden Azure-tjänster för att konfigurera den här nya identifierings metoden. Den här nya metoden skickar frågor till Azure AD för användar data som du sedan kan använda för traditionella identifierings data på andra sidan.  Både fullständig och delta-synkronisering stöds.  Mer information finns i [identifiering av Azure AD-användare](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="peer-cache-improvements"></a>Förbättringar i peer-cache
<!-- 1252345 -->
Peer-cachen använder inte längre nätverks åtkomst kontot för att autentisera nedladdnings begär Anden från peer-datorer. Det finns ett villkor för detta när kontot fortfarande krävs av klienter. Detta är ett krav för klienter som startar i WinPE och sedan kommer åt innehåll från en peer-cache-källa. Mer information finns i [krav och överväganden för peer-cache](../hierarchy/client-peer-cache.md#requirements).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Kompatibilitetsinställningar

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nya konfigurations inställningar för Windows 10-enheter som inte hanteras med Configuration Manager-klienten
<!-- 1354715 -->
I den här versionen har vi lagt till nya inställningar för konfigurations objekt för Windows 10-enheter som har registrerats med Intune eller som hanteras lokalt av Configuration Manager. Inställningarna är:

- **Lösenord**
  - Enhets kryptering
- **Enhet**
  - Ändring av regions inställningar (endast skriv bord)
  - Ändra energi-och vilo läges inställningar
  - Ändra språk inställningar
  - Ändring av system tid
  - Ändring av enhets namn
- **Lagringsplats**
  - Uppdatera appar automatiskt från Store
  - Använd endast privat lagring
  - Start av app från Store-app
- **Microsoft Edge**
  - Blockera åtkomst till about: Flags
  - Åsidosätt SmartScreen-prompt
  - Åsidosättning av SmartScreen-meddelanden för filer
  - WebRTC localhost-IP-adress
  - Standard sökmotor
  - OpenSearch-XML-URL
  - Start sidor (endast skriv bord)

Information om alla inställningar för Windows 10 finns i [så här skapar du konfigurations objekt för windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-device-compliance-policy-rules"></a>Nya regler för efterlevnadsprinciper för enheter

* **Krav på lösen ords typ**. Ange om användaren måste skapa ett alfanumeriskt lösen ord eller ett numeriskt lösen ord. För alfanumeriska lösen ord anger du också det minsta antal teckenuppsättningar som lösen ordet måste innehålla. De fyra teckenuppsättningarna är: gemener, versaler, symboler och siffror.

  **Stöds på:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
  <br></br>
* **Blockera USB-felsökning på enheten**. Du behöver inte konfigurera de här inställningarna eftersom USB-felsökning redan har inaktiverats på Android for Work-enheter.

  **Stöds på:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Blockera appar från okända källor**. Kräv att enheter förhindrar installation av appar från okända källor. Du behöver inte konfigurera den här inställningen eftersom Android for Work-enheter alltid begränsar installationen från okända källor.

  **Stöds på:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Kräv hot genomsökning på appar**. Den här inställningen anger att funktionen Verifiera appar är aktive rad på enheten.

  **Stöds på:**
  * Android 4,2 till 4,4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Programhantering

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Kör PowerShell-skript från Configuration Manager-konsolen
<!-- 1236459 -->

I Configuration Manager kan du distribuera skript till klient enheter med hjälp av paket och program. I den här versionen har vi lagt till nya funktioner som gör att du kan vidta följande åtgärder:

- Importera PowerShell-skript till Configuration Manager
- Redigera skripten från Configuration Manager-konsolen (endast för osignerade skript)
- Markera skript som godkända eller nekade för att förbättra säkerheten
- Kör skript på samlingar av Windows-klientdatorer och lokala hanterade Windows-datorer. Du distribuerar inte skript istället körs de i nära real tid på klient enheter.
- Granska resultaten som returnerades av skriptet i Configuration Manager-konsolen.

Mer information finns i [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nya princip inställningar för hantering av mobil program    
<!--1324760-->
Från och med den här versionen kan du använda tre nya princip inställningar för hantering av mobil program (MAM):

- **Blockera skärmdump (endast Android-enheter):** Anger att skärm bilds funktionerna på enheten är blockerade när du använder den här appen.


## <a name="operating-system-deployment"></a>Distribution av operativsystem

### <a name="hardware-inventory-collects-secure-boot-information"></a>Maskin varu inventering samlar in information om säker start
Maskin varu inventering samlar nu in information om huruvida säker start är aktiverat på klienter. Den här informationen lagras i **SMS_Firmware** -klassen (lanserades i version 1702) och aktive ras i maskin varu inventeringen som standard. Mer information om maskin varu inventering finns i  [så här konfigurerar du maskin varu inventering](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="collapsible-task-sequence-groups"></a>Komprimerbara aktivitetssekvenser
Den här versionen ger möjlighet att expandera och minimera grupper av aktivitetssekvenser. Du kan expandera eller komprimera enskilda grupper eller expandera eller komprimera alla grupper samtidigt.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Läs in start avbildningar igen med den aktuella Windows PE-versionen
När du kör **uppdaterings distributions platser** på en vald start avbildning kan du nu välja att läsa in den senaste versionen av Windows PE (från installations katalogen för Windows ADK) i Start avbildningen. Mer information finns i [Uppdatera distributions platser med start avbildningen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Programuppdateringar

### <a name="improvements-to-express-update-download-time"></a>Förbättringar av snabb uppdatering av hämtnings tid
I den här versionen har vi avsevärt förbättrat hämtnings tiden för Express uppdateringar. Mer information finns i [Hantera snabb installationsfiler för Windows 10-uppdateringar](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Hantera uppdateringar av Microsoft Surface-drivrutiner
<!-- 1098490 -->
Du kan nu använda Configuration Manager för att hantera uppdateringar av Microsoft Surface-drivrutiner.    


#### <a name="prerequisites"></a>Förutsättningar
- Alla program uppdaterings platser måste köra Windows Server 2016.    
- Detta är en för hands versions funktion som du måste aktivera för att den ska vara tillgänglig. Mer information finns i [Använda förhandsversionsfunktioner från uppdateringar](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Hantera uppdateringar för Surface-drivrutiner

1. Aktivera synkronisering för Microsoft Surface-drivrutiner. Använd proceduren i [Konfigurera klassificering och produkter](../../../sum/get-started/configure-classifications-and-products.md) och markera kryss rutan **Inkludera uppdateringar av Microsoft-Surface-drivrutiner och inbyggd program vara** på fliken **klassificeringar** för att aktivera Surface-drivrutiner.
2. [Synkronisera Microsoft Surface-drivrutiner](../../../sum/get-started/synchronize-software-updates.md).
3. [Distribuera synkroniserade Microsoft Surface-drivrutiner](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurera Windows Update för principer för avstängning av företag
<!-- 1290890 -->
Nu kan du konfigurera regler för avstängning för Windows 10-funktions uppdateringar eller kvalitets uppdateringar för Windows 10-enheter som hanteras direkt av Windows Update för företag. Du kan hantera uppskjutnings principerna i noden nya **Windows Update för affärs principer** under **program varu bibliotek**  >  **Windows 10-Underhåll**.

Mer information finns i [integration med Windows Update för företag i Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-microsoft-365-updates"></a>Förbättrade användar meddelanden för Microsoft 365 uppdateringar
Förbättringar har gjorts för att använda Office Klicka-och-kör-funktionen när en klient installerar en Microsoft 365 uppdatering. Detta inkluderar popup-meddelanden och meddelanden i appen och en nedräknings upplevelse. Mer information finns i [omstarts beteende och klient meddelanden för Microsoft 365 uppdateringar](../../../sum/deploy-use/manage-office-365-proplus-updates.md)

## <a name="reporting"></a>Rapportering

### <a name="use-windows-analytics-with-configuration-manager"></a>Använd Windows Analytics med Configuration Manager
<!-- 1318608 -->
Windows Analytics är en uppsättning lösningar som gör att du kan utforma insikter i miljöns aktuella tillstånd. Enheter i din miljö rapporterar information om Windows-telemetri. Data kan nås via Azure Portal. Om Uppgraderingsberedskap data är direkt tillgängliga i noden övervakning i Configuration Manager-konsolen.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Hantering av mobila enheter

### <a name="updates-to-android-for-work-sharing-configuration"></a>Uppdateringar av konfiguration av Android for Work-delning
<!-- 1338403 -->
I den här versionen har värdena för inställningen **Tillåt data delning mellan arbets profilen och den personliga profilen** i **arbets profil** inställnings gruppen uppdaterats. Vi har också lagt till en anpassad inställning för att blockera kopiering – klistra in mellan arbets profiler och personliga profiler.


### <a name="android-and-ios-enrollment-restrictions"></a>Registrerings begränsningar för Android och iOS
<!-- 1290826 -->
I den här versionen kan du nu ange att användare inte kan registrera personliga Android-eller iOS-enheter. Med de nya inställningarna för enhets begränsningar kan du begränsa registrering av Android-enheter till fördeklarerade enheter. För iOS-enheter kan du blockera registrering av alla enheter förutom de som registrerats med Apples Programmet för enhetsregistrering, Apple Configurator eller Intune-kontot för enhets registrerings hanteraren.

## <a name="protect-devices"></a>Skydda enheter

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inkludera förtroende för vissa filer och mappar i en Device Guard-princip
<!--1324676-->
I den här versionen har vi lagt till ytterligare funktioner i hantering av enhets skydd.

Du kan nu välja att lägga till förtroende för vissa filer för mappar i en Device Guard-princip. På så sätt kan du:

- Lösa problem med hanterade installations beteenden
- Verksamhetsbaserade appar som inte kan distribueras med Configuration Manager
- Lita på appar som ingår i en distributions avbildning för operativ system

Mer information finns i [hantering av enhets Guard med Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).