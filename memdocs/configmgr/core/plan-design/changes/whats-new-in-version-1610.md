---
title: Ny version 1610
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1610 av Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d23880def99fd12bffe83efffe9768f94481d07e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993564"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Vad&#39;s nya i version 1610 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1610 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1511, 1602 eller 1606.


> [!TIP]  
> Om du vill installera en ny plats måste du använda en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1610 av Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Övervakning i konsolen av installations status för uppdateringar  
Från och med version 1610, när du installerar ett uppdaterings paket och övervakar installationen i-konsolen, finns en ny fas: **efter installationen**. I den här fasen ingår status för aktiviteter som att starta om nyckel tjänster och initiera övervakning av replikering. (Den här fasen är inte tillgänglig i-konsolen förrän platsen har uppdaterats till version 1610.) Mer information om installations status för uppdateringar finns [i installera uppdateringar i konsolen](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Undanta klienter från automatisk uppgradering
Du kan undanta Windows-klienter från att uppgraderas med nya versioner av klient program varan. Det gör du genom att inkludera klient datorerna i en samling som anges som utesluts från uppgradering. Klienter i den exkluderade samlingen ignorerar begär Anden om att uppdatera klient program varan.  Mer information finns i [undanta Windows-klienter från uppgraderingar](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Förbättringar av gränser grupper
I version 1610 införs viktiga ändringar av gränser grupper och hur de fungerar med distributions platser. Dessa ändringar kan förenkla utformningen av innehålls infrastrukturen och ger dig mer kontroll över hur och när klienterna återgår till att söka efter ytterligare distributions platser som innehålls käll platser. Detta omfattar både lokala och molnbaserade distributions platser.
Dessa förbättringar ersätter koncept och beteenden som du kan vara bekant med (som att konfigurera distributions platser så att de är snabba eller långsamma). Den nya modellen bör vara enklare att konfigurera och underhålla. De här ändringarna gör det också möjligt att förbättra framtida ändringar som förbättrar andra plats system roller som du associerar till gränser grupper.

När du uppdaterar till version 1610, konverterar uppdateringen dina aktuella gränser för konfiguration av gränser så att de passar den nya modellen så att dessa ändringar inte stör dina befintliga konfigurationer för innehålls distribution.

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Peer-cache för innehålls distribution till klienter
Från och med version 1610 hjälper klient- **peer-cachen** dig att hantera distribution av innehåll till klienter på fjärranslutna platser. Peer-cache är en inbyggd Configuration Manager-lösning som klienter kan använda för att dela innehåll med andra klienter direkt från deras lokala cacheminne.

När du har distribuerat klient inställningar som aktiverar peer-cache till en samling kan medlemmar i samlingen fungera som peer-innehålls källa för andra klienter i samma gränser grupp.

Du kan också använda den nya instrument panelen för **klient data källor** för att förstå användningen av innehålls källor för peer-cache i din miljö.

> [!TIP]  
> Med version 1610 är peer-cache och instrument panelen för klient data källor för hands versions funktioner. Information om hur du aktiverar dem finns i [använda för hands versions funktioner från uppdateringar](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Mer information finns i [peer-cache för Configuration Manager klienter](../hierarchy/client-peer-cache.md)och [instrument panel för klient data källor](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrera flera delade distributions platser på samma gång
Nu kan du använda alternativet för att **omtilldela distributions platsen** för att Configuration Manager processen parallellt med omtilldelningen av upp till 50 delade distributions platser på samma gång. Innan den här versionen bearbetades omtilldelade distributions platser en i taget. Mer information finns i [migrera flera delade distributions platser på samma gång](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Cloud Management Gateway för hantering av Internetbaserade klienter

Med Cloud Management Gateway får du ett enkelt sätt att hantera Configuration Manager-klienter på Internet. Tjänsten Cloud Management Gateway, som distribueras till Microsoft Azure och kräver en Azure-prenumeration, ansluter till din lokala Configuration Manager-infrastruktur med hjälp av en ny roll som kallas för moln hanterings gatewayens anslutnings punkt. När den är fullständigt distribuerad och konfigurerad kan klienter kommunicera med lokala Configuration Manager plats system roller och molnbaserade distributions platser oavsett om de är anslutna till det interna privata nätverket eller Internet. Mer information och se hur Cloud Management Gateway jämför med Internetbaserad klient hantering finns i [Hantera klienter på Internet](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Förbättringar av versionsuppgraderingsprincipen för Windows 10
I den här versionen har följande förbättringar gjorts för den här princip typen:

- Du kan nu använda versions uppgraderings principen med Windows 10-datorer som kör Configuration Manager-klienten förutom Windows 10-datorer som har registrerats med Microsoft Intune.
- Du kan uppgradera från Windows 10 Professional till någon av plattformarna i guiden som är kompatibla med maskin varan.

## <a name="manage-hardware-identifiers"></a>Hantera maskin varu identifierare
Nu kan du ange en lista med maskinvaru-ID: n som Configuration Manager ska ignorera för PXE-start och klient registrering. Det finns två vanliga problem som kan åtgärdas:

1. Många enheter, som Surface Pro 3, inkluderar inte en Ethernet-port för internt. Ett USB-till-Ethernet-kort används vanligt vis för att upprätta en tråd bunden anslutning för att distribuera ett operativ system. Men på grund av kostnader och allmän användbarhet är dessa ofta delade kort. Eftersom MAC-adressen för det här kortet används för att identifiera enheten, blir återanvändande av kortet problematisk utan ytterligare administratörs åtgärder mellan varje distribution. I Configuration Manager version 1610 kan du undanta MAC-adressen för det här kortet så att det enkelt kan återanvändas i det här scenariot.
2. SMBIOS-ID: t ska vara en unik maskin varu identifierare, men vissa maskin varu enheter skapas med dubbla ID: n. Det här problemet kanske inte är lika vanligt som USB-till-Ethernet-kortets scenario, men du kan adressera det med hjälp av listan över exkluderade maskinvaru-ID: n.

Mer information finns i [Hantera dubbletter av maskin varu identifierare](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Förbättringar av Windows Store för företag-integration med Configuration Manager
Ändringar i den här versionen:
- Tidigare kunde du bara distribuera kostnads fria appar från Windows Store för företag. Configuration Manager har nu också stöd för distribution av betalade licensierade online-appar (endast för Intune-registrerade enheter).
- Nu kan du starta en omedelbar synkronisering mellan Windows Store för företag och Configuration Manager.
- Nu kan du ändra klientens hemliga nyckel som du fick från Azure Active Directory.
- Du kan ta bort en prenumeration på butiken.

Mer information finns i [Hantera appar från Windows Store för företag med Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Princip synkronisering för Intune-registrerade enheter
Du kan nu begära en princip synkronisering för en Intune-registrerad enhet från Configuration Manager-konsolen, i stället för att behöva begära en synkronisering från Företagsportal-appen på själva enheten. Information om synkroniseringsstatus för begäran är tillgänglig som en ny kolumn i enhets visningar som kallas **fjärrsynkroniseringsstatus**. Informationen finns också i avsnittet identifierings data i dialog rutan **Egenskaper** för varje enhet.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Använd kompatibilitetsinställningar för att konfigurera Windows Defender-inställningar
Nu kan du konfigurera inställningar för Windows Defender-klienten på Intune-registrerade Windows 10-datorer med hjälp av konfigurations objekt i Configuration Manager-konsolen.
Mer information finns i avsnittet **Windows Defender** i [skapa konfigurations objekt för Windows 8,1-och Windows 10-enheter som hanteras utan Configuration Manager-klienten](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Allmänna förbättringar av Software Center
- Användarna kan nu begära appar från Software Center och Programkatalog.
- Förbättringar som hjälper användarna att förstå vilken program vara som är ny och relevant.

## <a name="new-columns-in-device-collection-views"></a>Nya kolumner i vyer för enhets samling
Nu kan du Visa kolumner för **IMEI** -och **serie nummer** (för iOS-enheter) i vyer för enhets insamling.

## <a name="customizable-branding-for-software-center-dialogs"></a>Anpassningsbar anpassning av Software Center-dialogrutor
Anpassad anpassning av Software Center introducerades i Configuration Manager version 1602. I version 1610 är anpassningen nu utökad till alla associerade dialog rutor för att ge en mer konsekvent upplevelse för Software Center-användare.

Anpassad anpassning av Software Center tillämpas enligt följande regler:

- Om plats Server rollen Programkatalog webbplats plats inte är installerad visar Software Center det organisations namn som anges i **dator agentens** klient inställning **organisations namn som visas i Software Center**. Instruktioner finns i [så här konfigurerar du klient inställningar](../../clients/deploy/configure-client-settings.md).

- Om plats Server rollen Programkatalog webbplats plats är installerad visar Software Center det organisations namn och den färg som anges i egenskaperna Programkatalog för plats Server rollen för webbplats platser. Mer information finns i [konfigurations alternativ för programkatalog webbplats](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Om en Microsoft Intune-prenumeration har kon figurer ATS och är ansluten till Configuration Managers miljön visar Software Center organisationens namn, färg och företags logo typ som anges i prenumerations egenskaperna för Intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Tvingande respitperiod för nödvändiga distributioner av app- och programuppdateringar
I vissa fall kanske du vill ge användarna mer tid för att installera nödvändiga program distributioner eller program uppdateringar utöver de tids gränser som du ställer in. Detta kan till exempel vara nödvändigt när en dator har inaktiverats under en längre tid och måste installera ett stort antal program-eller uppdaterings distributioner. Om en slutanvändare till exempel precis har returnerat från semestern kan de vänta en stund medan förfallna program distributioner installeras. För att hjälpa till att lösa det här problemet kan du nu definiera en tvingande respitperiod genom att distribuera Configuration Manager klient inställningar till en samling. 

Utför följande åtgärder för att konfigurera respitperioden:
1. På sidan **dator agent** i klient inställningar konfigurerar du den nya **periodens respitperiod för tvång efter distributionens tids gräns (timmar)** med ett värde mellan **1** och **120** timmar.
2. I en ny nödvändig program distribution, eller i egenskaperna för en befintlig distribution, går du till sidan **Schemaläggning** och markerar kryss rutan **fördröj verk ställning av distributionen enligt användar inställningar, upp till den Respitperiod som definierats i klient inställningarna**. Alla distributioner som har den här kryss rutan markerad och är riktade till enheter som du också har distribuerat klient inställningen till använder tvångs perioden för tvång.

Om du konfigurerar en tvångs Grace-period och markerar kryss rutan, kommer den att installeras i det första icke-affärsfönster som användaren har konfigurerat för den aktuella Grace-perioden när tids gränsen för program installationen har uppnåtts. Användaren kan dock fortfarande öppna Software Center och installera programmet när som helst. När Grace-perioden går ut återgår tvång till det normala beteendet för förfallna distributioner. Liknande alternativ har lagts till i guiden distribution av program uppdateringar, guiden automatiska distributions regler och egenskaps sidor.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Förbättrade funktioner i dialog rutor om nödvändig program vara
När en användare får nödvändig program vara, från inställningen **vilo läge och Påminn mig:** kan du välja i följande listruta med värden: 
- **Senare**. Anger att meddelanden ska schemaläggas baserat på de meddelande inställningar som kon figurer ATS i klient agent inställningarna.
- **Fast tid**. Anger att meddelandet ska visas igen efter den valda tiden (till exempel på 30 minuter).

![Sidan dator agent i inställningar för klient agent](media/client-notification-settings.png)

Den maximala vilo läges tiden baseras på aviserings värden som kon figurer ATS i klient agent inställningarna. Om **distributions tids gränsen är större än 24 timmar** konfigureras till exempel användaren var (timme) på sidan dator agent, och den är mer än 24 timmar före tids gränsen, ser användaren en uppsättning alternativ för vilo läge upp till men aldrig längre än 10 timmar. När tids gränsen närmar sig, är färre alternativ tillgängliga, konsekventa med relevanta klient agent inställningar för varje komponent i distributions tids linjen.

För en distribution med hög risk, till exempel en aktivitetssekvens som distribuerar ett operativ system, är användar aviserings upplevelsen nu mer påträngande. I stället för ett tillfälligt meddelande i aktivitets fältet, varje gång användaren meddelas att kritiskt program varu underhåll krävs, visas en dialog ruta som nedan på användarens dator:

![Dialog rutan nödvändig program vara](media/client-toast-notification.png)


Mer information:
- [Inställningar för att hantera högrisk distributioner](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Konfigurera klientinställningar](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Instrument panel för program uppdateringar
Använd den nya instrument panelen för program uppdateringar om du vill visa aktuell kompatibilitetsstatus för enheter i din organisation och snabbt analysera data för att se vilka enheter som är utsatta för risk. Om du vill visa instrument panelen navigerar du till **övervaknings**  >  **Översikt**  >  **säkerhets**  >  **instrument panel för säkerhets program uppdateringar**.

Mer information finns i [övervaka program uppdateringar](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Förbättringar av processen för programbegäran
När du har godkänt ett program för installation kan du senare välja att neka begäran genom att klicka på **neka** i Configuration Manager-konsolen. Tidigare var den här knappen nedtonad efter godkännande.

Den här åtgärden gör inte att programmet avinstalleras från några enheter. Det hindrar dock användarna från att installera nya kopior av programmet från Software Center.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrera efter innehålls storlek i regler för automatisk distribution
Nu kan du filtrera efter innehålls storleken för program uppdateringar i regler för automatisk distribution. Om du till exempel bara vill hämta program uppdateringar som är mindre än 2 MB kan du ange filtret för **innehålls storlek (KB)** till **< 2048**. Genom att använda det här filtret förhindrar du att stora program uppdateringar hämtas automatiskt, vilket ger bättre stöd för förenklad Windows-etablering när nätverks bandbredden är begränsad. Mer information finns i:
- [Configuration Manager och förenklad Windows-underhåll på äldre operativ system](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)
- [Distribuera programuppdateringar automatiskt](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Gör något av följande för att konfigurera fältet för **innehålls storlek (KB)** :
- När du skapar en regel för automatisk distribution går du till sidan **program uppdateringar** i guiden Skapa regel för automatisk distribution.
- I egenskaperna för en befintlig regel för automatisk distribution går du till fliken **program uppdateringar** .

## <a name="office-365-client-management-dashboard"></a>Instrument panel för Office 365-klient hantering
Instrument panelen för Office 365-klient hantering är nu tillgänglig i Configuration Manager-konsolen. Om du vill visa instrument panelen går du till översikt över **program varu bibliotek**  >  **Overview**  >  **Office 365-klient hantering**.

På instrument panelen visas diagram med följande:

- Antal Office 365-klienter
- Office 365-klient versioner
- Office 365-klient språk
- Office 365-klient kanaler

Mer information finns i [Hantera uppdateringar av Microsoft 365-appar](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Aktivitetssekvenssteg för att hantera konvertering av BIOS till UEFI
Nu kan du anpassa en aktivitetssekvens för operativ Systems distribution med en ny variabel, TSUEFIDrive, så att steget **starta om datorn** ska förbereda en FAT32-partition på hård disken för över gång till UEFI. Följande procedur visar ett exempel på hur du kan skapa steg i aktivitetssekvensen för att förbereda hård disken för BIOS till UEFI-konvertering. Mer information finns i avsnittet  [om aktivitetssekvenser för att hantera BIOS till UEFI-konvertering](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Förbättringar i aktivitetssekvensen steg: förbereda ConfigMgr-klienten för avbildning  
Steget Förbered ConfigMgr-klient tar nu bort Configuration Manager-klienten fullständigt, i stället för att bara ta bort viktig information. När aktivitetssekvensen distribuerar operativ Systems avbildningen installeras en ny Configuration Manager-klient varje gång. Mer information finns i [stegen i aktivitetssekvensen](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Intune-scheman för efterlevnadsprinciper
Nu kan du få en snabb överblick över övergripande kompatibilitet för enheter och de främsta orsakerna till inkompatibilitet, genom att använda nya diagram under arbets ytan **övervakning** i Configuration Manager-konsolen. Du kan klicka på ett avsnitt i diagrammet för att öka detalj nivån till en lista över enheterna i den kategorin. Mer information finns i [övervaka policyn för efterlevnad](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Lookout-integrering för Hybrid implementeringar för att skydda iOS-och Android-enheter
Microsoft integrerar med Lookout-lösningen för skydd av mobila hot för att skydda iOS-och Android-enheter genom att identifiera skadlig kod, riskfyllda appar med mera, på enheter. Lookout-lösningen hjälper dig att fastställa hot nivån, som kan konfigureras. Du kan skapa en regel för efterlevnadsprinciper i Configuration Manager för att fastställa enhetens efterlevnad baserat på riskbedömningen av Lookout. Genom att använda åtkomstprinciper kan du tillåta eller blockera åtkomst till företagsresurser utifrån enhetens efterlevnadsstatus.

Användare av icke-kompatibla iOS-enheter uppmanas att registrera sig. De måste installera Lookout for Work-appen på sina enheter, aktivera appen och åtgärda hot som rapporteras i Lookout for Work programmet för att få åtkomst till företagets data.


## <a name="new-compliance-settings-for-configuration-items"></a>Nya kompatibilitetsinställningar för konfigurations objekt
Det finns många nya inställningar som du kan använda i konfigurations objekt för olika enhets plattformar. Detta är inställningar som tidigare fanns i Microsoft Intune i en fristående konfiguration och som nu är tillgängliga när du använder Intune med Configuration Manager.
Mer information finns i [konfigurations objekt för enheter som hanteras utan Configuration Manager-klienten](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Nya inställningar för Android-enheter
#### <a name="password-settings"></a>Inställningar för lösenord
- **Kom ihåg tidigare lösenord**
- **Tillåt fingeravtrycksupplåsning**

#### <a name="security-settings"></a>Säkerhetsinställningar
- **Kräv kryptering på minneskort**
- **Tillåt skärmbild**
- **Tillåt sändning av diagnostikdata**

#### <a name="browser-settings"></a>Webbläsarinställningar
- **Tillåt webbläsare**
- **Tillåt Autofyll**
- **Tillåt blockering av popup-fönster**
- **Tillåt cookies**
- **Tillåt Active scripting**

#### <a name="app-settings"></a>Appinställningar
- **Tillåt Google Play-butik**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet
- **Tillåt flyttbara lagringsenheter**
- **Tillåt Wi-Fi -delning**
- **Tillåt geolokalisering**
- **Tillåt NFC**
- **Tillåt Bluetooth**
- **Tillåt röstroaming**
- **Tillåt dataroaming**
- **Tillåt SMS/MMS-meddelanden**
- **Tillåt röstassistent**
- **Tillåt röstsamtal**
- **Tillåt kopiera och klistra in**

### <a name="new-settings-for-ios-devices"></a>Nya inställningar för iOS-enheter
#### <a name="password-settings"></a>Inställningar för lösenord
- **Antal avancerade tecken som krävs i lösenord**
- **Tillåt enkla lösenord**
- **Antal minuters inaktivitet innan lösenord krävs**
- **Kom ihåg tidigare lösenord**

### <a name="new-settings-for-mac-os-x-devices"></a>Nya inställningar för Mac OS X-enheter
#### <a name="password-settings"></a>Inställningar för lösenord
- **Antal avancerade tecken som krävs i lösenord**
- **Tillåt enkla lösenord**
- **Kom ihåg tidigare lösenord**
- **Minuter av inaktivitet innan skärmsläckaren aktiveras**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nya inställningar för Station ära och mobila Windows 10-enheter
#### <a name="password-settings"></a>Inställningar för lösenord
- **Lägst antal teckenuppsättningar**
- **Kom ihåg tidigare lösenord**
- **Kräv lösenord när enheten återgår från viloläge**

#### <a name="security-settings"></a>Säkerhetsinställningar
- **Filkryptering på mobil enhet**
- **Tillåt manuell avregistrering**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet
- **Tillåt VPN via mobilnät**
- **Tillåt VPN-roaming via mobilnät**
- **Tillåt telefonåterställning**
- **Tillåt USB-anslutning**
- **Tillåt Cortana**
- **Tillåt action center meddelanden**

### <a name="new-settings-for-windows-10-team-devices"></a>Nya inställningar för Windows 10 team-enheter
#### <a name="device-settings"></a>Enhetsinställningar
- **Aktivera Operational Insights i Azure**
- **Aktivera trådlös Miracast-projektion**
- **Välj den mötesinformation som ska visas på välkomstskärmen**
- **Webbadress till bakgrundsbild för låsskärm**

### <a name="new-settings-for-windows-81-devices"></a>Nya inställningar för Windows 8,1-enheter
#### <a name="applicability-settings"></a>Tillämplighetsinställningar
- **Tillämpa alla konfigurationer på Windows 10**

#### <a name="password-settings"></a>Inställningar för lösenord
- **Lösenordstyp krävs**
- **Lägst antal teckenuppsättningar**
- **Minsta längd på lösenord**
- **Antal tillåtna, upprepade felinloggningar innan enheten rensas**
- **Antal minuter av inaktivitet innan skärmen stängs av**
- **Lösenordets giltighetstid (i dagar)**
- **Kom ihåg tidigare lösenord**
- **Förhindra återanvändning av tidigare lösenord**
- **Tillåt bildlösenord och PIN**

#### <a name="browser-settings"></a>Webbläsarinställningar
- **Tillåt automatisk identifiering av intranätsnätverk**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nya inställningar för Windows Phone 8,1-enheter
#### <a name="applicability-settings"></a>Tillämplighetsinställningar
- **Tillämpa alla konfigurationer på Windows 10**

#### <a name="password-settings"></a>Inställningar för lösenord
- **Lägst antal teckenuppsättningar**
- **Tillåt enkla lösenord**
- **Kom ihåg tidigare lösenord**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet
- **Tillåt automatisk anslutning till kostnadsfria, trådlösa surfpunkter**
