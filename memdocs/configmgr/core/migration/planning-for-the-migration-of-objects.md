---
title: Migrera objekt
titleSuffix: Configuration Manager
description: Lär dig hur du planerar migrering av objekt mellan hierarkier i en Configuration Manager aktuella gren miljö.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9777fb12a2d63a990587386ac33cb2749bf19a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719654"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Planera för migrering av Configuration Manager objekt till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager aktuella grenen kan du migrera många av de olika objekt som är associerade med olika funktioner som finns på en käll plats.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a>Planera migreringen av program uppdateringar  
 Du kan migrera program uppdaterings objekt, t. ex. program uppdaterings paket och program uppdaterings distributioner.  

 För att kunna migrera program uppdaterings objekt måste du först ställa in målhierarkin med konfigurationer som matchar din källhierarki-miljö. Detta kräver följande åtgärder:  

-   Distribuera en aktiv program uppdaterings plats i målhierarkin  

-   Konfigurera en katalog med produkter och språk som matchar konfigurationen av källhierarkin  

-   Synkronisera program uppdaterings platsen i målhierarkin med Windows Server Update Services (WSUS)  

När du migrerar programuppdateringar måste du tänka på följande:  

-   Migreringen av program uppdaterings objekt kan inte slutföras när du inte har synkroniserat information i målhierarkin för att matcha konfigurationen för din källhierarki.  

    > [!WARNING]  
    >  Configuration Manager stöder inte användning av WSUSutil-verktyget för att synkronisera data mellan en käll-och målhierarkin.  

-   Du kan inte migrera anpassade uppdateringar som publicerats med System Center Updates Publisher. Istället måste anpassade uppdateringar publiceras om till målhierarkin.  

När du migrerar från en Configuration Manager 2007-källhierarki ändrar migreringsprocessen vissa program uppdaterings objekt till det format som används av målhierarkin. Använd följande tabell som hjälp för att planera migreringen av program uppdaterings objekt från Configuration Manager 2007.  

|Configuration Manager 2007-objekt|Objektets namn efter migrering|  
|-----------------------------------|---------------------------------|  
|Programuppdateringslistor|Programuppdateringslistor konverteras till programuppdateringsgrupper.|  
|Distribution av programuppdateringar|Programuppdateringsdistributioner konverteras till distributioner och uppdateringsgrupper.<br /><br /> När du har migrerat en program uppdaterings distribution från Configuration Manager 2007 måste du aktivera den i målhierarkin innan du kan distribuera den.|  
|Programuppdateringspaket|Programuppdateringspaket förblir programuppdateringspaket.|  
|Programuppdateringsmallar|Programuppdateringsmallar förblir programuppdateringsmallar.<br /><br /> **Varaktighet** svärdet i Configuration Manager 2007-distributionsmall migreras inte.|  

När du migrerar objekt från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki, ändras inte program uppdaterings objekt.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a>Planera att migrera innehåll  
 Du kan migrera innehåll från en källhierarki som stöds till en målhierarki. För en Configuration Manager 2007-källhierarki innehåller det här innehållet program distributions paket och program och virtuella program, t. ex. Microsoft Application Virtualization (App-V). För System Center 2012 Configuration Manager och Configuration Manager aktuella Branch source-hierarkier, innehåller det här innehållet program och App-V virtuella program. När du migrerar innehåll mellan hierarkier migreras de komprimerade källfilerna till målhierarkin.  

### <a name="packages-and-programs"></a>Paket och program  
 När du migrerar paket och program ändras de inte av migreringen. Innan du migrerar dem måste du dock konfigurera varje paket så att det använder en Universal Naming Convention-sökväg (UNC) för käll filens plats. Som en del av konfigureringen för att migrera paket och program måste du tilldela en plats i målhierarkin som hanterar det här innehållet. Innehållet migreras inte från den tilldelade platsen, men efter migreringen kommer den tilldelade platsen åt den ursprungliga käll fils platsen med hjälp av UNC-mappningen.  

 När du har migrerat ett paket och program till målhierarkin, och medan migreringen från källhierarkin fortfarande är aktiv, kan du göra innehållet tillgängligt för klienter i den hierarkin med hjälp av en delad distributions plats. För att det ska gå att använda en delad distributionsplats måste innehållet förbli åtkomligt på distributionsplatsen på källplatsen. Mer information om delade distributions platser finns i [dela distributions platser mellan käll-och mål-hierarkier](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) i [Planera en strategi för migrering av innehålls distribution](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 För innehåll som har migrerats, om innehålls versionen ändras i källhierarkin eller målhierarkin, kan klienterna inte längre komma åt innehållet från den delade distributions platsen i målhierarkin. I det här scenariot måste du migrera om innehållet för att återställa en konsekvent version av paketet mellan källhierarkin och målhierarkin. Den här informationen synkroniseras under data insamlings cykeln.  

> [!TIP]  
>  För varje paket du migrerar uppdaterar du paketet i målhierarkin. Den här åtgärden kan förhindra problem med att distribuera paketet till distributionsplatserna i målhierarkin. Men när du uppdaterar ett paket på distributions platsen i målhierarkin kommer klienter i den hierarkin inte längre att kunna hämta det paketet från en delad distributions plats. Om du vill uppdatera ett paket i målhierarkin går du till program biblioteket i Configuration Manager-konsolen, högerklickar på paketet och väljer sedan **Uppdatera distributions platser**. Utför den här åtgärden för varje paket som du migrerar.  

> [!TIP]  
> Använd Package Conversion Manager för att konvertera paket och program till Configuration Manager program. Mer information finns i [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Virtuella program  
När du migrerar App-V-paket från en Configuration Manager 2007-plats som stöds konverterar migreringsprocessen dem till program i målhierarkin. Dessutom skapas följande distributions typer i målhierarkin, baserat på befintliga annonser för App-V-paketet:  

-   Om det inte finns några annonser skapas en distributionstyp som använder standardinställningarna för distributionstyp.  

-   Om det finns en annons skapas en distributions typ som använder samma inställningar som Configuration Manager 2007-annonsen.  

-   Om det finns flera annonser skapas en distributions typ för varje Configuration Manager 2007-annons med hjälp av inställningarna för den annonsen.  

> [!IMPORTANT]  
>  Om du migrerar ett tidigare migrerat Configuration Manager 2007 App-V-paket Miss lyckas migreringen eftersom virtuella programpaket inte stöder överskrivning av migreringen. I den här situationen måste du ta bort det migrerade virtuella programpaketet från målhierarkin och sedan skapa ett nytt migreringsjobb som migrerar det virtuella programmet.  

> [!NOTE]  
>  När du har migrerat ett App-V-paket kan du använda guiden Uppdatera innehåll för att ändra käll Sök vägen för program-V-distributions typer. Mer information om hur du uppdaterar innehåll för en distributions typ finns i hantera distributions typer i [hanterings uppgifter för Configuration Manager program](../../apps/deploy-use/management-tasks-applications.md).  

När du migrerar från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki kan du migrera objekt för den virtuella App-V-miljön, förutom App-V-distributions typer och program. Mer information om App-V-miljöer finns i [distribuera virtuella app-v-program](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Annonser  
Du kan migrera annonser från en Configuration Manager 2007-datakälla som stöds till målhierarkin genom att använda samlings-baserad migrering. Om du uppgraderar en klient behåller den historiken över annonser som körts tidigare, för att hindra klienten från att reprisera migrerade annonser.  

> [!NOTE]  
>  Du kan inte migrera annonser för virtuella paket. Detta är ett undantag till migrering av annonser.  

### <a name="applications"></a>Program  
 Du kan migrera program från en System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki till en målhierarkin. Om du omtilldelar en klient från käll- till målhierarkin, behåller den historiken över tidigare installerade program, för att hindra klienten från att köra ett migrerat program igen.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a>Planera migreringen av samlingar  
 Du kan migrera villkoren för samlingar från en System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki. För detta använder du ett Objektbaserade migreringsjobb. När du migrerar en samling migrerar du reglerna för samlingen, inte information om samlingens medlemmar eller information eller objekt som hör till samlingens medlemmar.  

 Migrering av samlingsobjektet stöds inte när du migrerar från en Configuration Manager 2007-källhierarki.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a>Planera att migrera operativ Systems distributioner  
Du kan migrera följande operativsystemdistributionsobjekt från en källhierarki som stöds:  

-   Operativsystemavbildningar och paket Käll Sök vägen för start avbildningarna uppdateras till standard avbildnings platsen för Windows AIK (Windows Administrative Installation Kit) på mål platsen. Följande är krav och begränsningar för migrering av operativsystemavbildningar och paket:  

    -   För att kunna migrera bildfiler måste dator kontot för SMS-providerns plats på den översta nivån ha **Läs** -och **Skriv** behörighet till källfilerna för käll platsens Windows AIK-plats.  

    -   När du migrerar ett installations paket för operativ systemet måste du kontrol lera att paketets konfiguration på käll platsen pekar på den mapp som innehåller WIM-filen och inte själva WIM-filen. Om installationspaketet pekar på WIM-filen misslyckas migreringen av installationspaketet.  

    -   När du migrerar ett start avbildnings paket från en Configuration Manager 2007-käll plats behålls inte paket-ID: t för paketet på mål platsen. Resultatet av detta är att klienter i målhierarkin inte kan använda startavbildningspaket som är tillgängliga på delade distributionsplatser.  

-   Aktivitetssekvenser. När du migrerar en aktivitetssekvens som innehåller en referens till ett klient installations paket, ersätts den referensen med en referens till klient installations paketet för målhierarkin.  

    > [!NOTE]  
    >  När du migrerar en aktivitetssekvens kan Configuration Manager migrera objekt som inte är obligatoriska i målhierarkin. Dessa objekt omfattar start avbildningar och Configuration Manager 2007-klient installations paket.  

-   Drivrutiner och drivrutinspaket. När du migrerar driv rutins paket måste dator kontot för SMS-providern i målhierarkin ha fullständig behörighet till paket källan.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a>Planera att migrera önskad konfigurations hantering  
Du kan migrera konfigurationsobjekt och konfigurationsbaslinjer.  

> [!NOTE]  
>  Feltolkade konfigurations objekt från Configuration Manager 2007-käll-hierarkier stöds inte för migrering. Du kan inte migrera eller importera dessa konfigurationsobjekt till målhierarkin. Mer information om feltolkade konfigurations objekt finns i avsnittet [om konfigurations objekt i Desired Configuration Management](https://go.microsoft.com/fwlink/?LinkId=103846) i dokumentations biblioteket för Configuration Manager 2007.  

Du kan importera Configuration Manager 2007-konfigurations paket. Import processen konverterar automatiskt konfigurations paketen så att de är kompatibla med Configuration Manager aktuella grenen.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a>Planera för att migrera gränser  
 Du kan migrera gränser mellan hierarkier. När du migrerar gränser från Configuration Manager 2007 migreras varje gräns från käll platsen samtidigt och läggs till i en ny gräns grupp som skapas i målhierarkin. När du migrerar gränser från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-hierarki läggs varje gräns du väljer till i en ny gräns grupp i målhierarkin.  

 Alla automatiskt skapade gränsgrupper aktiveras för innehållsplats men inte för platstilldelning. Det här förhindrar överlappande gränser för platstilldelning mellan käll- och målhierarkierna. När du migrerar från en Configuration Manager 2007-käll plats hjälper detta till att förhindra nya Configuration Manager 2007-klienter som installeras från felaktigt tilldelade till målhierarkin. Configuration Manager aktuella gren klienter tilldelas som standard inte automatiskt till Configuration Manager 2007-platser.  

 Om du under migreringen delar en distributionsplats med målhierarkin migreras alla gränser som är associerade med den distributionen automatiskt till målhierarkin. I målhierarkin skapar migreringen en ny skrivskyddad gränser grupp för varje delad distributions plats. Om du ändrar gränserna för distributionsplasten i källhierarkin uppdateras gränsgruppen i målhierarkin med ändringarna vid nästa datainsamlingscykel.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a>Planera att migrera rapporter  
Configuration Manager stöder inte migrering av rapporter. Exportera i stället rapporter från källhierarkin med SQL Server Reporting Services Report Builder och importera dem sedan till målhierarkin.  

> [!NOTE]  
>  Eftersom det finns schema ändringar för rapporter mellan Configuration Manager 2007 och Configuration Manager aktuell gren, testar du varje rapport som du importerar från en Configuration Manager 2007-hierarki för att säkerställa att den fungerar som förväntat.  

Mer information om rapportering finns i [Introduktion till rapportering](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a>Planera för att migrera organisations-och sökmappar  
 Du kan migrera organisationsmappar och sökmappar från en källhierarki som stöds till en målhierarki. Från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki kan du dessutom migrera villkoren för en sparad sökning till en målhierarkin.  

 När du migrerar behålls som standard sökmappen och strukturerna för administrationsmappar för objekt och samlingar. I guiden Skapa migreringsjobb, på sidan **Inställningar** , kan du dock konfigurera ett migreringsjobb så att organisations strukturen för objekt inte migreras genom att avmarkera kryss rutan för det här alternativet. Samlingarnas organisationsstrukturer behålls alltid.  

 Ett undantag är sökmappar som innehåller virtuella program. När ett App-V-paket migreras omvandlas App-V-paketet till ett program i Configuration Manager. Efter migreringen av sökmappen hittas bara de återstående paketen och sökmappen kan inte hitta ett App-V-paket på grund av den här konverteringen till ett program när App-V-paketet migreras.  

 När du migrerar en sparad sökning från en System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki migrerar du villkoren för sökningen och inte informationen om Sök resultaten. Migrering av en sparad sökning kan inte tillämpas från en Configuration Manager 2007-käll plats.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a>Planera för att migrera Tillgångsinformation anpassningar  
 Du kan migrera anpassningar för tillståndsinformation från en källhierarki som stöds till en målhierarki. Det finns inga betydande ändringar i strukturen för Tillgångsinformation anpassningar mellan Configuration Manager 2007 och Configuration Manager aktuella grenen.  

> [!NOTE]  
> Configuration Manager aktuella grenen har inte stöd för migrering av Tillgångsinformation objekt från en Configuration Manager 2007-webbplats som använder Tillgångsinformation service 2,0 (AIS 2,0).  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a>Planera att migrera anpassningar av regler för avläsning av program vara  
 Det finns inga betydande ändringar i avläsning av program vara mellan Configuration Manager 2007 och Configuration Manager aktuella grenen. Du kan migrera anpassningar för regler för avläsning av programvara från en källhierarki som stöds till en målhierarki.  

 Som standard associeras inte regler för avläsning av programvara som du migrerar till en målhierarki med en specifik plats i målhierarkin, utan gäller i stället för alla klienter i hierarkin. Om du vill tillämpa en regel för avläsning av programvara på klienter på en specifik plats måste du redigera avläsningsregeln när den har migrerats.  
