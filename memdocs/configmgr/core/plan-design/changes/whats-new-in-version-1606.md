---
title: Nytt i version 1606
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1606 av Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3817551c75557a275c98e8c62faef46185438a25
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993615"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Vad&#39;s nya i version 1606 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1606 för Configuration Manager är tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1511 eller 1602. Version 1511 är den ursprungliga bas linje versionen som du använder för att installera nya Configuration Manager-platser.
> [!TIP]  
> Läs mer om:  
>   
> - [Installera nya platser](../../servers/deploy/install/prepare-to-install-sites.md) (med en bas linje version som 1511)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md) (t. ex. uppdatering 1602 eller 1606)  

 Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1606 av Configuration Manager.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Uppdateringar och service

### <a name="changes-for-the-updates-and-servicing-node"></a>Ändringar för noden uppdateringar och underhåll
Följande är ändringar i noden uppdateringar och underhåll i Configuration Manager-konsolen:
> [!NOTE]
> Dessa ändringar är inte tillgängliga förrän du har installerat version 1606.

- **Ändra nodnamn:**

    På arbets ytan **övervakning** har noden **plats underhålls status** bytt namn till **uppdateringar och underhålls status**.
- **Mer installations status information:**

    När du visar uppdateringens installations status för en plats visar konsolen nu en separat information för följande åtgärder:
    - **Hämta** (Detta gäller endast den plats på den översta nivån där tjänst anslutnings punktens plats system roll är installerad.)
    - **Replikering**
    - **Kravkontroll**
    - **Installation**

  Dessutom finns det nu mer detaljerad information för varje steg, inklusive vilken loggfil du kan visa för mer information.  
-   **Nytt alternativ för att försöka utföra nödvändiga fel:**

    På arbets ytan **Administration** och **övervakning** innehåller noden **uppdateringar och underhåll** en ny knapp i menyfliksområdet som kallas **Ignorera krav varningar**.

    När du installerar uppdateringar utan att använda alternativet för att ignorera krav kontroll varningar (från uppdaterings guiden) och installationen av uppdateringen stoppas på grund av en varning, kan du välja **Ignorera krav varningar** från menyfliksområdet. Detta utlöser en automatisk fortsättning av uppdaterings installationen.  



- **Renare vy över uppdateringar:**

    I noden **uppdateringar och underhåll** visas nu bara den senast installerade uppdateringen och eventuella nya uppdateringar som är tillgängliga för installation. Om du vill visa tidigare installerade uppdateringar klickar du på knappen ny **Historik** som visas i menyfliksområdet.  

-   **Omdöpt alternativ för för produktion:**

    I noden **uppdateringar och underhåll** kallas knappen **klient alternativ** nu **befordran för produktions klient**.


###  <a name="pre-release-features"></a>Förhandsfunktioner
Från och med 1606 måste du ge tillåtelse att använda för hands versions funktioner i Configuration Manager innan du kan välja och aktivera användningen. Mer information finns i [Använda förhandsversionsfunktioner från uppdateringar](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Ny distributions plats uppdaterings beteende
Uppdatering 1606 introducerar ändringar som förbättrar tillgängligheten för distributions platser när du installerar framtida uppdateringar.

När uppdatering 1606 har installerats, nästa gång du installerar en uppdatering på den platsen som kräver automatisk ominstallation av plats system roller för standard-och mottagar distributions plats, går alla distributions platser inte längre offline för att uppdatera samtidigt. I stället använder plats servern platsens innehålls distributions inställningar för att distribuera uppdateringen till en delmängd av distributions platserna vid en viss tidpunkt. Resultatet är att endast vissa distributions platser går offline för att installera uppdateringen. Detta gör att distributions platser som ännu inte har börjat uppdateras, eller som har slutfört uppdateringen, är online och kan tillhandahålla innehåll till klienter.



## <a name="accessibility"></a><a name="accessibility"></a> Tågen
Om du vill navigera mellan olika noder i en arbets yta kan du nu ange den första bokstaven i namnet på en nod. Varje tangenttryckning flyttar markören till nästa nod som börjar med den bokstaven. För användare som har en skärm läsare läser läsaren ut namnet på den noden. Mer information om hjälpmedels alternativ finns i [hjälpmedels funktioner](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a>Administration
Följande är ändringar i Administration i Configuration Manager-konsolen:
### <a name="oms-connector"></a>OMS-koppling

Nu kan du ansluta Configuration Manager som samlingar från Configuration Manager till [Microsoft Operations Management Suite (OMS)](/azure/azure-monitor/overview). Detta gör data som samlingar från din Configuration Manager-distribution synlig i OMS. Du hittar mer information i [synkronisera data från Configuration Manager till Microsoft Operations Management Suite här](/azure/azure-monitor/platform/collect-sccm).

OMS-kopplingen är en för hands versions funktion. Information om hur du aktiverar det finns i [använda för hands versions funktioner från uppdateringar](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Stöd för cachestorlek i klient inställningar

Nu kan du konfigurera storleken på cache-mappen på klient datorer med **klient inställningar** i Configuration Manager-konsolen. Tidigare kunde du bara ange klientens cachestorlek när du installerar eller installerar om klient program varan. Nu kan du ange cache-storlek som en klient inställning (antingen standard eller anpassad) och sedan använda inställningarna för nästa princip uppdatering på klienten, utan att behöva installera om klienten. Mer information finns i [Konfigurera klientcacheminne för Configuration Manager-klienter](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Lokal hantering av mobila enheter

### <a name="support-for-multiple-device-management-points"></a>Stöd för flera enhets hanterings platser

Lokal hantering av mobila enheter (MDM) har nu stöd för en ny funktion i Windows 10-uppdaterings jubileum som automatiskt konfigurerar en registrerad enhet att ha mer än en enhets hanterings plats tillgänglig för användning. Den här funktionen gör att enheten kan återgå till en annan enhets hanterings plats när den som används normalt inte är tillgänglig. Den här funktionen fungerar bara för datorer och enheter med uppdaterings minnes dag för Windows 10 installerat.


## <a name="application-management"></a>Programhantering

### <a name="manage-apps-from-the-windows-store-for-business"></a>Hantera appar från Windows Store för företag

[Windows Store för företag](https://www.microsoft.com/business-store) är där du kan hitta och köpa Windows-appar för din organisation, antingen individuellt eller i volym. Genom att ansluta butiken till Configuration Manager, kan du synkronisera listan med appar som du har köpt med Configuration Manager, visa dem i Configuration Manager-konsolen och distribuera dem precis som andra appar.

Mer information finns i [Hantera appar från Windows Store för företag med Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Hantera volyminköpta iOS-appar

Arbets flödet för att hantera iOS-appar som köpts i volym och distribuera dessa med Configuration Manager har förbättrats.


### <a name="software-center-user-interface"></a>Användar gränssnitt för Software Center

Användar gränssnittet i Software Center har effektiviserats för enklare identifiering.
*  Flikarna **installations status** och **installerad program vara** har kombinerats till en enda **installations status** -flik.
*  **Uppdateringar**, **operativ system**och **program** har delats upp i tre separata flikar.
* Flera uppdateringar kan nu väljas för installation på en gång, eller så kan alla uppdateringar installeras samtidigt genom att klicka på **Installera alla**.

### <a name="content-status-links"></a>Länkar till innehålls status
I egenskaperna för ett program eller paket finns nu en länk som leder till status för objektet.

## <a name="software-updates"></a>Programuppdateringar

### <a name="client-setting-to-manage-the-microsoft-365-client-agent"></a>Klient inställning för att hantera Microsoft 365 klient agenten
Nu kan du använda en Configuration Manager klient inställning för att hantera Microsoft 365 klient agenten. När du har konfigurerat och distribuerat Microsoft 365 uppdateringar fungerar Configuration Manager klient agenten med Microsoft 365 klient agenten för att hämta och installera Microsoft 365 uppdateringar från en distributions plats.

Mer information finns i [Hantera uppdateringar av Microsoft 365 appar med Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Växla klienter manuellt till en ny program uppdaterings plats
Nu kan du aktivera ett alternativ som låter Configuration Manager klienter växla till en ny program uppdaterings plats när det finns problem med den aktiva program uppdaterings platsen. När det är aktiverat kommer klienterna söka efter en annan programuppdateringsplats vid nästa sökning.

Mer information finns i [Planera för program uppdateringar i Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Omstartsalternativ för Windows 10-klienter efter installation av programuppdatering
När en program uppdatering som kräver en omstart distribueras med hjälp av Configuration Manager och installeras på en dator, schemaläggs en väntande omstart. En dialog ruta för omstart visas också. Från och med Configuration Manager version 1606 är alternativen **Uppdatera och starta om** och **Uppdatera och Stäng** av tillgängliga när det finns en väntande omstart för en Configuration Manager program uppdatering. De är tillgängliga i Windows energi alternativ för Windows 10-datorer. När du har använt något av dessa alternativ visas inte dialog rutan Starta om när datorn har startats om.

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Köra genomsökningen av kompatibilitet för program uppdateringar omedelbart efter att en klient installerar program uppdateringar och startar om
Du kan nu köra en kompatibilitetskontroll direkt efter att en klient installerar program uppdateringar och startar om. Om du vill konfigurera detta för en distribution, på sidan **användar upplevelse** i guiden distribuera program uppdateringar, väljer du **om någon uppdatering i distributionen kräver en systemomstart kör du utvärderings cykeln för uppdaterings distribution efter omstart**. Detta gör att klienten kan söka efter ytterligare program uppdateringar som blir tillämpliga efter att klienten startats om, och sedan installera dem (och bli kompatibla) i samma underhålls period. Mer information finns i [distribuera program uppdateringar automatiskt](../../../sum/deploy-use/automatically-deploy-software-updates.md) eller [distribuera program uppdateringar manuellt](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>Distribution av operativsystem

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Förbättringar av steget i aktivitetssekvensen: installera program uppdateringar
En ny inställning, **utvärdera program uppdateringar från cachelagrade genomsöknings resultat**, ger dig möjlighet att göra en fullständig sökning efter program uppdateringar, i stället för att använda de cachelagrade genomsöknings resultaten. Mer information finns i [stegen i aktivitetssekvensen](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Dessutom är en ny aktivitetssekvens-variabel, **SMSTSSoftwareUpdateScanTimeout**, tillgänglig. Med den här variabeln kan du styra tids gränsen för genomsökning av program uppdateringar under steget installera program uppdateringar. Standardvärdet är 30 minuter. Mer information finns i [inbyggda variabler för aktivitetssekvenser](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>OSDPreserveDriveLetter-variabeln i aktivitetssekvensen är inaktuell
Variabeln OSDPreserveDriveLetter är inaktuell. Från och med Configuration Manager version 1606 fastställer Installationsprogrammet för Windows den bästa enhets beteckningen (vanligt vis C:) som standard under en operativ Systems distribution.

Mer information finns i [inbyggda variabler för aktivitetssekvenser](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Anpassa storleken på RamDisk TFTP-fönstret för PXE-aktiverade distributions platser
Nu kan du anpassa storleken på RamDisk-fönstret för PXE-aktiverade distributions platser. Om du har anpassat nätverket kan det orsaka att hämtningen av start avbildningen inte fungerar med ett timeout-fel, eftersom fönstret är för stort. Med anpassnings fönstret för RamDisk Trivial File Transfer Protocol (TFTP) kan du optimera TFTP-trafik när du använder PXE för att uppfylla dina särskilda nätverks krav.

Mer information finns i [förbereda plats system roller för operativ Systems distributioner med Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Kompatibilitetsinställningar

### <a name="smart-lock-setting-for-android-devices"></a>Smart Lock inställning för Android-enheter
En ny inställning, **tillåt Smart Lock och andra betrodda agenter**, har lagts till i konfigurationsobjektet Android och Samsung KNOX Standard.

Med den här inställningen kan du styra Smart Lock-funktionen på kompatibla Android-enheter. Med den här telefon funktionen, som ibland kallas "betrodda agenter", kan du inaktivera eller kringgå lösen ordet för enhetens Lås skärm om enheten är på en betrodd plats. En betrodd plats kan till exempel vara när den är ansluten till en speciell Bluetooth-enhet eller när den är nära en NFC-tagg. Du kan använda den här inställningen för att förhindra att användare konfigurerar Smart Lock.


## <a name="device-configuration-and-protection"></a>Enhets konfiguration och skydd

### <a name="product-name-changes"></a>Produkt namns ändringar

* Microsoft Passport for Work kallas nu **Windows Hello för företag**.
* Företagsdataskydd kallas nu **Windows informationsskydd**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Distribution av Windows Hello för företag (Passport for Work)

Nu kan du distribuera Windows Hello för företag-principer till domänanslutna Windows 10-enheter som hanteras av Configuration Manager-klienten.

Configuration Manager-konsolen har uppdaterats för att återspegla dessa ändringar.

### <a name="ios-activation-lock"></a>iOS-Aktiveringslås
Configuration Manager kan hjälpa dig att hantera iOS Aktiveringslås, en funktion i Hitta min iPhone-appen för enheter med iOS 7,1 och senare. När aktiveringslås har aktiverats måste användarens Apple-ID och lösenord anges innan någon kan:
* Inaktivera Hitta min iPhone.
* Radera enheten.
* Återaktivera enheten.

Configuration Manager kan hjälpa dig att hantera aktiveringslås på två sätt:

- Aktivera aktiveringslåset på kontrollerade enheter.
- Kringgå aktiveringslåset på kontrollerade enheter.


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection kan hjälpa dig att hantera och övervaka Microsoft Defender Advanced Threat Protection (ATP). Microsoft Defender ATP är en ny tjänst som hjälper företag att upptäcka, undersöka och svara på avancerade attacker i sina nätverk. Configuration Manager principer kan hjälpa dig att publicera och övervaka hanterade datorer som kör Windows 10, version 1607 (build 14328) eller senare.

Mer information finns i [Microsoft Defender Avancerat skydd](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Enhetskategorier
Du kan skapa enhets kategorier, som kan användas för att placera enheter i enhets samlingar automatiskt när du använder Configuration Manager med Microsoft Intune. Användarna måste sedan välja en enhets kategori när de registrerar en enhet i Intune. Dessutom kan du ändra kategori för en enhet från Configuration Manager-konsolen.

Mer information finns i [så här kategoriserar du enheter automatiskt i samlingar med Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Fördeklarera enheter med IMEI-eller iOS-serienummer

Du kan identifiera företagsägda enheter genom att importera sina enhets nummer för mobil utrustning (IMEI) eller iOS-serienummer. Du kan ladda upp en fil med kommaavgränsade värden (. csv) som innehåller IMEI-nummer för enheten, eller så kan du ange enhets informationen manuellt. Med importerad information anges ägarskapet för de enheter som registreras som "företag" i listor över enheter. En Intune-licens krävs fortfarande för varje användare som har åtkomst till tjänsten.

### <a name="on-premises-health-attestation-service-communication"></a>Kommunikation mellan tjänster för lokal hälso deklaration

Nu kan du aktivera övervakning av hälsoattestering av tjänster för Windows 10-datorer med endast lokal infrastruktur, så att datorer utan Internet åtkomst kan rapportera Hälsoattestering för enhet (HÄLSOATTESTERING).

Mer information finns i [hälsoattestering för Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Fjärrstyrning
Ge användarna möjlighet att acceptera eller neka fil överföringar innan innehållet överförs från det delade Urklippet i en fjärrstyrningssession. Användare behöver bara bevilja behörighet en gång per session och visnings programmet har inte möjlighet att ge sig själva behörighet att fortsätta med fil överföringen. Du kan hitta den här nya inställningen på arbets ytan **Administration** . Gå till **klient inställningar**och öppna sedan panelen **fjärrverktyg** i **standardinställningar**.