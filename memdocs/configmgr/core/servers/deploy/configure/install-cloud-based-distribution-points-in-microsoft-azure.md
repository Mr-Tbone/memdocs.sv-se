---
title: Installera moln distributions platser
titleSuffix: Configuration Manager
description: Använd de här stegen för att konfigurera en moln distributions plats i Configuration Manager.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30cd61240b09f821d8b18c37e6accc7450f35817
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718849"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Installera en moln distributions plats för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Implementeringen av delning av innehåll från Azure har ändrats. Använd en innehålls aktive rad Cloud Management Gateway genom att aktivera alternativet för att **tillåta att CMG fungerar som en moln distributions plats och hanterar innehåll från Azure Storage**. Mer information finns i [ändra en CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Du kommer inte att kunna skapa en traditionell moln distributions plats i framtiden. Mer information finns i [borttagna och föråldrade funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Den här artikeln beskriver stegen för att installera en Configuration Manager moln distributions plats i Microsoft Azure. Den innehåller följande avsnitt:

- [Innan du börjar](#bkmk_before)
- [Konfigurera](#bkmk_setup)
- [Konfigurera DNS](#bkmk_dns)
- [Konfigurera plats serverns proxy](#bkmk_proxy)
- [Distribuera innehåll och konfigurera klienter](#bkmk_client)
- [Hantera och övervaka](#bkmk_monitor)
- [Ändra](#bkmk_modify)
- [Avancerad fel sökning](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a>Innan du börjar

Börja med att läsa artikeln [Använd en moln distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Den artikeln hjälper dig att planera och utforma dina moln distributions platser.

Använd följande check lista för att kontrol lera att du har nödvändig information och förutsättningar för att skapa en moln distributions plats:  

- Plats servern kan ansluta till Azure. Om nätverket använder en proxyserver [konfigurerar du plats system rollen](#bkmk_proxy).  

- **Azure-miljön** som ska användas. Till exempel det offentliga Azure-molnet eller Azure amerikanska myndigheters molnet.  

- Från och med version 1806 och *rekommenderas*använder du **Azure Resource Manager-distributionen**. Den har följande krav:<!--1322209-->  

    - Integrering med [Azure Active Directory](azure-services-wizard.md) för **moln hantering**. Identifiering av Azure AD-användare krävs inte.  

    - ID för Azure **-prenumerationen**.  

    - Azure- **resurs gruppen**.  

    - Ett **prenumerations administratörs konto** måste logga in i guiden.  

- Ett **certifikat för serverautentisering**, exporterat som. PFX-fil.  

- Ett globalt unikt **tjänst namn** för moln distributions platsen.  

    > [!TIP]  
    > Innan du begär certifikatet för serverautentisering som använder tjänst namnet, kontrollerar du att det önskade Azure-domännamnet är unikt. Till exempel *WallaceFalls.CloudApp.net*.
    >
    > 1. Logga in på [Azure Portal](https://portal.azure.com).
    > 1. Välj **alla resurser**och välj sedan **Lägg till**.
    > 1. Sök efter **moln tjänst**. Välj **Skapa**.
    > 1. I fältet **DNS-namn** anger du det prefix som du vill använda, till exempel *WallaceFalls*. Gränssnittet visar om domän namnet är tillgängligt eller redan används av en annan tjänst.
    >
    > Skapa inte tjänsten i portalen. Använd bara den här processen för att kontrol lera namn tillgänglighet.

- Azure- **regionen** för den här distributionen.  

- Om du fortfarande behöver använda den klassiska Azure **-tjänstedistributionen** i Configuration Manager version 1810 eller tidigare behöver du följande krav:  

    > [!Important]  
    > Från och med version 1810 föråldras klassiska tjänst distributioner i Azure i Configuration Manager. Börja använda Azure Resource Manager distributioner för moln distributions platsen. Mer information finns i [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av moln distributions platsen.<!-- 3605704 -->

    - ID för Azure **-prenumerationen**.  

    - Ett Azure- **hanterings certifikat**som exporteras som båda. CER och. PFX-filer. En administratör för Azure-prenumeration måste lägga till. CER-hanterings certifikat till prenumerationen i [Azure Portal](https://portal.azure.com).  

### <a name="branchcache"></a>BranchCache

Om du vill aktivera en moln distributions plats för att använda Windows BranchCache installerar du BranchCache-funktionen på plats servern.<!-- SCCMDocs-pr#4054 -->

- Om plats servern har en plats system roll för en lokal distributions plats konfigurerar du alternativet i rollens egenskaper för att **Aktivera och konfigurera BranchCache**. Mer information finns i [Konfigurera en distributions plats](install-and-configure-distribution-points.md#bkmk_config-general).

- Om plats servern inte har en distributions plats roll, installerar du funktionen BranchCache i Windows. Mer information finns i [installera BranchCache-funktionen](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Om du redan har distribuerat innehåll till en moln distributions plats och sedan bestämmer dig för att aktivera BranchCache måste du först installera funktionen. Distribuera sedan om innehållet till moln distributions platsen.

> [!NOTE]  
> Om du har fler än en moln distributions plats i Configuration Manager version 1810 och senare, måste du manuellt ange lösen frasen för BranchCache-nyckeln. Mer information finns i [Microsoft Support KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a>Konfigurera  

Utför den här proceduren på webbplatsen som värd för den här moln distributions platsen enligt din [design](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **Cloud Services**och välj **moln distributions platser**. I menyfliksområdet väljer du **skapa moln distributions plats**.  

2. Konfigurera följande inställningar på sidan **Allmänt** i guiden skapa distributions plats för moln:  

    1. Ange först **Azure-miljön**.  

    2. Från och med version 1806 och *rekommenderas*väljer du **Azure Resource Manager distribution** som distributions metod. Välj **Logga** in för att autentisera med ett administratörs konto för Azure-prenumeration. Guiden fyller automatiskt i de återstående fälten från den information som lagras under krav för Azure AD-integration. Om du äger flera prenumerationer väljer du det **prenumerations-ID** för önskad prenumeration som du vill använda.  

    > [!Note]  
    > Från och med version 1810 föråldras klassiska tjänst distributioner i Azure i Configuration Manager.
    >
    > Om du behöver använda en klassisk tjänst distribution väljer du det alternativet på den här sidan. Ange först ditt ID för Azure **-prenumeration**. Välj sedan **Bläddra** och välj. PFX-fil för Azures hanterings certifikat.  

3. Välj **Nästa**. Vänta medan platsen testar anslutningen till Azure.  

4. På sidan **Inställningar** anger du följande inställningar och väljer sedan **Nästa**:  

    - **Region**: Välj den Azure-region där du vill skapa moln distributions platsen.  

    - **Resurs grupp** (endast Azure Resource Manager distributions metod)  

        - **Använd befintlig**: Välj en befintlig resurs grupp i den nedrullningsbara listan.  

        - **Skapa ny**: Ange det nya resurs grupps namnet som ska skapas i din Azure-prenumeration.  

    - **Primär plats**: Välj den primära platsen för att distribuera innehåll till den här distributions platsen.

    - **Certifikat fil**: Välj **Bläddra** och välj. PFX-fil för den här moln distributions platsens certifikat för serverautentisering. Det egna namnet från det här certifikatet fyller i fälten **FQDN** för obligatoriska tjänster och **tjänst namn** .  

        > [!NOTE]  
        > Certifikat för moln distributions plats serverns autentisering stöder jokertecken. Om du använder ett jokertecken, ersätter du asterisken`*`() i fältet för **tjänstens FQDN** med det önskade värd namnet för tjänsten.  

5. På sidan **aviseringar** ställer du in lagrings kvoter, överförings kvoter och i vilken procent andel av kvoterna som du vill Configuration Manager generera aviseringar. Välj **Nästa**.  

6. Slutför guiden.  

### <a name="monitor-installation"></a>Övervaka installation  

Webbplatsen börjar skapa en ny värdbaserad tjänst för moln distributions platsen. När du har stängt guiden övervakar du installations förloppet för moln distributions platsen i Configuration Manager-konsolen. Övervaka också filen **CloudMgr. log** på den primära plats servern. Om det behövs övervakar du etableringen av moln tjänsten i Azure Portal.  

> [!NOTE]  
> Det kan ta upp till 30 minuter att etablera en ny distributions plats i Azure. Filen **CloudMgr. log** upprepar följande meddelande tills lagrings kontot har tillhandahållits:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> När den etablerar lagrings kontot skapas och konfigureras tjänsten.  

### <a name="verify-installation"></a>Verifiera installationen

Kontrol lera att installationen av moln distributions platsen har slutförts med följande metoder:  

- Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **Cloud Services**och välj noden **distributions platser i molnet** . Hitta den nya moln distributions platsen i listan. Kolumnen status måste vara **klar**.  

- Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **system status**och välj noden **komponent status** . Visa alla meddelanden från **SMS_CLOUD_SERVICES_MANAGER** -komponenten och leta efter status meddelande-ID **9409**.  

- Om det behövs går du till Azure Portal. **Distributionen** av moln distributions platsen visar statusen **klar**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a>Konfigurera DNS  

Innan klienter kan använda moln distributions platsen måste de kunna matcha namnet på moln distributions platsen med en IP-adress som hanteras av Azure. Hanterings platsen ger dem **tjänstens FQDN** för moln distributions platsen. Moln distributions platsen finns i Azure som **tjänst namnet**. Se de här värdena på fliken **Inställningar** i egenskaperna för moln distributions platsen.

> [!Note]  
> Noden **moln distributions platser** i-konsolen innehåller en kolumn med namnet **tjänst namn**, men visar i själva verket **FQDN-** värdet. Om du vill se båda värdena öppnar du **Egenskaper** för moln distributions platsen och växlar till fliken **Inställningar** .  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Certifikatets nätverks namn för serverautentisering måste innehålla ditt domän namn. Det här namnet måste anges när du köper ett certifikat från en offentlig leverantör. Vi rekommenderar att du utfärdar det här certifikatet från din PKI. Till exempel `WallaceFalls.contoso.com`. När du anger det här certifikatet i guiden skapa distributions plats för molnet fyller det egna namnet på **tjänstens FQDN** -egenskap (`WallaceFalls.contoso.com`). **Tjänst namnet** tar samma värdnamn (`WallaceFalls`) och lägger till det i Azure- `cloudapp.net`domännamnet. I det här scenariot måste klienterna matcha domänens **FQDN** -namn`WallaceFalls.contoso.com`() till Azure **-tjänstens namn** (`WallaceFalls.cloudapp.net`). Skapa ett CNAME-alias för att mappa dessa namn.

### <a name="create-cname-alias"></a>Skapa CNAME-alias

Skapa en kanonisk namn post (CNAME) i din organisations offentliga, Internet-riktad DNS. Den här posten skapar ett alias för moln distributions platsens **FQDN-** egenskap som klienter får till Azure **-tjänstens namn**. Skapa till exempel en ny CNAME-post för `WallaceFalls.contoso.com` till `WallaceFalls.cloudapp.net`.  

### <a name="client-name-resolution-process"></a>Process för klient namns matchning

Följande process visar hur en klient matchar namnet på moln distributions platsen:  

1. Klienten hämtar FQDN för **tjänsten** för moln distributions platsen i listan med innehålls källor. Till exempel `WallaceFalls.contoso.com`.  

2. Den frågar DNS, som löser FQDN-namnet med hjälp av CNAME-aliaset till namnet på Azure **-tjänsten**. Till exempel `WallaceFalls.cloudapp.net`.  

3. Den frågar DNS igen, vilket löser Azure-tjänstens namn till den offentliga Azure-IP-adressen.  

4. Klienten använder den här IP-adressen för att starta kommunikationen med moln distributions platsen.  

5. Moln distributions platsen visar certifikatet för serverautentisering till klienten. Klienten använder förtroende kedjan för certifikatet som ska verifieras.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a>Konfigurera plats serverns proxy  

Den primära plats servern som hanterar moln distributions platsen måste kommunicera med Azure. Om din organisation använder en proxyserver för att kontrol lera Internet åtkomst konfigurerar du den primära plats servern så att den använder den här proxyn.  

Mer information finns i [stöd för proxy server](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a>Distribuera innehåll och konfigurera klienter

Distribuera innehåll till moln distributions platsen på samma sätt som andra lokala distributions platser. Hanterings platsen omfattar inte moln distributions platsen i listan över innehålls platser om den inte har det innehåll som klienten begär. Mer information finns i [distribuera och hantera innehåll](deploy-and-manage-content.md).

Hantera en moln distributions plats på samma sätt som andra lokala distributions platser. Dessa åtgärder omfattar tilldelning av den till en distributions plats grupp och hantering av innehålls paket. Mer information finns i [Installera och konfigurera distributions platser](install-and-configure-distribution-points.md).

Standard klient inställningarna gör att klienterna automatiskt kan använda moln distributions platser. Kontrol lera åtkomsten till alla moln distributions platser i hierarkin med följande klient inställning:  

- I gruppen **moln inställningar** ändrar du inställningen **Tillåt åtkomst till moln distributions platser**.  

    - Som standard är den här inställningen inställd på **Ja**.  

    - Ändra och distribuera den här inställningen för både användare och enheter.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a>Hantera och övervaka  

Övervaka innehåll som du distribuerar till en moln distributions plats på samma sätt som med andra lokala distributions platser. Mer information finns i [Övervaka innehåll](monitor-content-you-have-distributed.md).

### <a name="alerts"></a><a name="bkmk_alerts"></a>Aviseringar  

Configuration Manager kontrollerar regelbundet Azure-tjänsten. Om tjänsten inte är aktiv eller om det finns problem med prenumerationer eller certifikat genererar Configuration Manager en avisering.

Konfigurera tröskelvärden för den mängd data som du vill lagra på moln distributions platsen och för den mängd data som klienterna laddar ned från distributions platsen. Använd aviseringar för dessa tröskelvärden för att hjälpa dig att avgöra när du ska stoppa eller ta bort moln tjänsten, justera det innehåll som du lagrar på moln distributions platsen eller ändra vilka klienter som kan använda tjänsten.

- **Lagrings aviserings kvot**: lagrings aviserings kvoten anger en övre gräns i GB för den mängd data eller innehåll som du vill lagra på moln distributions platsen. Som standard är det här tröskelvärdet 2 000 GB. Configuration Manager genererar varnings-och kritiska aviseringar när det återstående lediga utrymmet når de nivåer som du anger. Som standard sker de här aviseringarna vid 50% och 90% av tröskelvärdet.  

- **Månatlig överförings aviserings kvot**: månatlig överförings aviserings kvot hjälper dig att övervaka den mängd innehåll som överförs från distributions platsen till klienter under en 30-dagarsperiod. Som standard är det här tröskelvärdet 10 000 GB. Platsen genererar varnings-och kritiska aviseringar när överföringar når värden som du definierar. Som standard sker de här aviseringarna vid 50% och 90% av tröskelvärdet.  

    > [!IMPORTANT]  
    > Configuration Manager övervakar data överföringen, men stoppar inte överföringen av data utöver det angivna tröskelvärdet för överförings aviseringar.  

Ange tröskelvärden för varje distributions plats i molnet under installationen eller Använd fliken **aviseringar** i egenskaperna för moln distributions platsen.  

> [!NOTE]  
> Aviseringar för en moln distributions plats beror på användnings statistik från Azure, som kan ta upp till 24 timmar innan den blir tillgänglig. Mer information om Lagringsanalys för Azure finns i [Lagringsanalys](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Den primära plats som övervakar moln distributions platsen laddar ned transaktions data från Azure i en Tim cykel. Dessa transaktions data lagras i `CloudDP-<ServiceName>.log` filen på plats servern. Configuration Manager utvärderar sedan denna information mot lagrings-och överförings kvoterna för varje distributions plats i molnet. När överföringen av data når eller överskrider den angivna volymen för varningar eller kritiska aviseringar, genererar Configuration Manager lämplig avisering.  

> [!WARNING]  
> Eftersom platsen hämtar information om data överföringar från Azure varje timme kan användningen överskrida en varning eller ett kritiskt tröskelvärde innan Configuration Manager kan komma åt data och utlösa en avisering.  


## <a name="modify"></a><a name="bkmk_modify"></a>Gör

Visa information på hög nivå om distributions platsen i noden **distributions platser i molnet** under **Cloud Services** i arbets ytan **Administration** i Configuration Manager-konsolen. Välj en distributions plats och välj **Egenskaper** för att se mer information.  

När du redigerar egenskaperna för en moln distributions plats innehåller följande flikar inställningar som du kan redigera:  

#### <a name="settings"></a>Inställningar

- **Beskrivning**  

- **Certifikat fil**: innan certifikatet för serverautentisering upphör att gälla, utfärda ett nytt certifikat med samma egna namn. Lägg sedan till det nya certifikatet här för att tjänsten ska börja använda. Om certifikatet upphör att gälla, kommer klienter inte att lita på och använda tjänsten.  

#### <a name="alerts"></a>Aviseringar

Justera data tröskelvärdena för lagring och månatliga överförings varningar.  

#### <a name="content"></a>Innehåll

Hantera innehåll på samma sätt som för en lokal distributions plats.  

### <a name="redeploy-the-service"></a>Distribuera om tjänsten

Mer betydande ändringar, till exempel följande konfigurationer, kräver omdistribution av tjänsten:

- Klassisk distributions metod för att Azure Resource Manager
- Prenumeration
- Tjänstnamn
- Privat till offentlig PKI
- Azure-region

Från och med version 1806, om du har en befintlig moln distributions plats på den klassiska distributions metoden, för att kunna använda metoden för Azure Resource Manager distribution måste du distribuera en ny distributions plats för molnet. Det finns två alternativ:

- Om du vill återanvända samma tjänst namn:  

    1. Ta först bort den klassiska moln distributions platsen. Om det inte finns någon annan moln distributions plats kan det hända att klienterna inte kan hämta innehåll.  

    2. Skapa en ny distributions plats för molnet med hjälp av en Resource Manager-distribution. Återanvänd samma certifikat för serverautentisering.  

    3. Distribuera nödvändiga programpaket innehåll till den nya moln distributions platsen.  

- Om du vill använda ett nytt tjänst namn:  

    1. Skapa en ny distributions plats för molnet med hjälp av en Resource Manager-distribution. Använd ett nytt certifikat för serverautentisering.  

    2. Distribuera nödvändiga programpaket innehåll till den nya moln distributions platsen.  

    3. Ta bort den klassiska moln distributions platsen.

> [!Tip]  
> Så här fastställer du den aktuella distributions modellen för en moln distributions plats:<!--SCCMDocs issue #611-->  
>
> 1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **distributions platser i molnet** .  
> 2. Lägg till attributet för **distributions modell** som en kolumn i list visningen. För en Resource Manager-distribution är det här attributet **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Stoppa eller starta moln tjänsten på begäran

Stoppa en moln distributions plats när som helst i Configuration Manager-konsolen. Den här åtgärden förhindrar omedelbart att klienter laddar ned ytterligare innehåll från tjänsten. Starta om moln tjänsten från Configuration Manager-konsolen för att återställa åtkomsten för klienterna. Du kan till exempel stoppa en moln tjänst när den når ett data tröskelvärde.  

När du stoppar en moln distributions plats tar moln tjänsten inte bort innehållet från lagrings kontot. Det förhindrar inte heller att plats servern överför ytterligare innehåll till moln distributions platsen. Hanterings platsen returnerar fortfarande moln distributions platsen till klienter som en giltig innehålls källa.

Använd följande procedur för att stoppa en moln distributions plats:  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **Cloud Services**och välj noden **distributions platser i molnet** .  

2. Välj moln distributions plats. Om du vill stoppa moln tjänsten som körs i Azure väljer du **stoppa tjänst** i menyfliksområdet.  

3. Välj **Starta tjänst** för att starta om moln distributions platsen.  

### <a name="delete-a-cloud-distribution-point"></a>Ta bort en moln distributions plats

Om du vill avinstallera en moln distributions plats väljer du distributions platsen i Configuration Manager-konsolen och väljer sedan **ta bort**.  

När du tar bort en moln distributions plats från en-hierarki tar Configuration Manager bort innehållet från moln tjänsten i Azure.

Om du tar bort alla komponenter i Azure manuellt blir systemet inkonsekvent. Det här läget lämnar överblivna information och oväntade beteenden kan uppstå.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a>Avancerad fel sökning

Om du behöver samla in diagnostikloggning från virtuella Azure-datorer för att felsöka problem med moln distributions platsen, använder du följande PowerShell-exempel för att aktivera tjänstens diagnostiska tillägg för prenumerationen:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Följande exempel är en **Diagnostics. wadcfgx** -fil som refereras till i **public_config** -variabeln i PowerShell-skriptet ovan. Mer information finns i [konfigurations schema för Azure-diagnostik-tillägg](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
