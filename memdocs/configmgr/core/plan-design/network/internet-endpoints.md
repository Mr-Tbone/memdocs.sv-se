---
title: Krav för Internet-åtkomst
titleSuffix: Configuration Manager
description: Lär dig om Internet-slutpunkter så att du kan använda alla funktioner i Configuration Manager funktioner.
ms.date: 06/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78958809aeed5db9d2a36d960b91572b91eafe05
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502365"
---
# <a name="internet-access-requirements"></a>Krav för Internet-åtkomst

Vissa Configuration Manager funktioner är beroende av Internet anslutning för fullständig funktionalitet. Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, så se till att tillåta dessa slut punkter.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Tjänst anslutnings punkt

Dessa konfigurationer gäller för den dator som är värd för tjänst anslutnings punkten och eventuella brand väggar mellan datorn och Internet. Båda måste tillåta kommunikation via utgående port **tcp 443** för https och utgående port **TCP 80** för http till nedanstående Internet platser.

Tjänst anslutnings punkten har stöd för användning av en webbproxy (med eller utan autentisering) för att använda dessa platser. Mer information finns i [stöd för proxy server](proxy-server-support.md).

Mer information om tjänst anslutnings punkten finns i [om tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md).

Andra Configuration Manager-funktioner kan kräva ytterligare slut punkter från tjänst anslutnings punkten. Mer information finns i de andra avsnitten i den här artikeln.

> [!TIP]  
> Tjänst anslutnings punkten använder Microsoft Intune tjänsten när den ansluter till `go.microsoft.com` eller `manage.microsoft.com` . Det finns ett känt problem där Intune Connector upplever anslutnings problem om Baltimore CyberTrust-rotcertifikatet inte är installerat eller är skadat på tjänst anslutnings punkten. Mer information finns i [KB 3187516: tjänst anslutnings punkten hämtar inte uppdateringar](https://support.microsoft.com/help/3187516).  

Från och med version 2002, om Configuration Manager-platsen inte kan ansluta till obligatoriska slut punkter för en moln tjänst, genererar den en kritisk status meddelande-ID 11488. När den inte kan ansluta till tjänsten ändras SMS_SERVICE_CONNECTOR komponent status till kritisk. Visa detaljerad status i noden [komponent status](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) i Configuration Manager-konsolen.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a>Uppdateringar och underhåll

Mer information om den här funktionen finns i [uppdateringar och underhåll för Configuration Manager](../../servers/manage/updates.md).

> [!Tip]  
> Aktivera de här slut punkterna för [insikts](../../servers/manage/management-insights.md) regeln för hantering, **Anslut platsen till Microsoft Cloud för Configuration Manager uppdateringar**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10-underhåll

Mer information om den här funktionen finns i [hantera Windows som en tjänst](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure-tjänster

Mer information om den här funktionen finns i [Konfigurera Azure-tjänster för användning med Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com`(Offentligt Azure-moln)
- `management.usgovcloudapi.net`(Azure-moln för amerikanska myndigheter)

## <a name="co-management"></a>Samhantering

Om du registrerar Windows 10-enheter till Microsoft Intune för samhantering kontrollerar du att enheterna kan komma åt de slut punkter som krävs av Intune. Mer information finns i [nätverks slut punkter för Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store för företag

Om du integrerar Configuration Manager med [Microsoft Store för företag](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)kontrollerar du att tjänst anslutnings punkten och de riktade enheterna har åtkomst till moln tjänsten. Mer information finns i [konfiguration av Microsoft Store för företag-proxy](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="delivery-optimization"></a>Leveransoptimering

Om du använder leverans optimering måste klienterna kommunicera med sin moln tjänst:`*.do.dsp.mp.microsoft.com`

Distributions platser som har stöd för Microsoft Connected cache kräver även dessa slut punkter.

Mer information finns i följande artiklar:

- [Vanliga frågor och svar om leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Grundläggande begrepp för innehålls hantering i Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Microsoft Connected cache i Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Moln tjänster

<!-- SCCMDocs-pr #3402 -->

I det här avsnittet beskrivs följande funktioner:

- Cloud Management Gateway (CMG)
- Distributions plats för moln (CDP)
- Azure Active Directory (Azure AD)-integration
- Azure AD-baserad identifiering

Mer information om CMG finns i [Planera för CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

I följande avsnitt visas slut punkterna efter roll. Vissa slut punkter refererar till en tjänst av `<name>` , som är moln tjänst namnet för CMG eller CDP. Om din CMG till exempel är `GraniteFalls.CloudApp.Net` , är den faktiska lagrings slut punkten `GraniteFalls.blob.core.windows.net` .<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>Tjänstanslutningspunkt

För distribution av CMG/CDP-tjänst behöver tjänst anslutnings punkten åtkomst till:

- Specifika Azure-slutpunkter är olika per miljö beroende på konfigurationen. Configuration Manager lagrar dessa slut punkter i plats databasen. Fråga tabellen **AzureEnvironments** i SQL Server efter listan över Azure-slutpunkter.

- [Azure-tjänster](#azure-services)

- För identifiering av Azure AD-användare:

  - Version 1902 och senare: Microsoft Graph slut punkt`https://graph.microsoft.com/`

  - Version 1810 och tidigare: Azure AD Graph-slutpunkt`https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG kopplings punkt

CMG-anslutnings punkten behöver åtkomst till följande tjänst slut punkter:

- Namn på moln tjänst (för CMG eller CDP):
  - `<name>.cloudapp.net`(Offentligt Azure-moln)
  - `<name>.usgovcloudapp.net`(Azure-moln för amerikanska myndigheter)

- Service Management-slut punkt:`https://management.core.windows.net/`  

- Lagrings slut punkt (för innehålls aktive rad CMG eller CDP):
  - `<name>.blob.core.windows.net`(Offentligt Azure-moln)
  - `<name>.blob.core.usgovcloudapi.net`(Azure-moln för amerikanska myndigheter)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

Plats systemet för CMG-anslutnings punkten stöder användning av en webbproxy. Mer information om hur du konfigurerar den här rollen för en proxy finns i [stöd för proxy server](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Anslutnings punkten för CMG måste bara ansluta till CMG-tjänstens slut punkter. Den behöver inte åtkomst till andra Azure-slutpunkter.

### <a name="configuration-manager-client"></a>Configuration Manager-klient

- Namn på moln tjänst (för CMG eller CDP):
  - `<name>.cloudapp.net`(Offentligt Azure-moln)
  - `<name>.usgovcloudapp.net`(Azure-moln för amerikanska myndigheter)

- Lagrings slut punkt (för innehålls aktive rad CMG eller CDP):
  - `<name>.blob.core.windows.net`(Offentligt Azure-moln)
  - `<name>.blob.core.usgovcloudapi.net`(Azure-moln för amerikanska myndigheter)

- För Azure AD-token hämtar Azure AD-slut punkten:
  - `login.microsoftonline.com`(Offentligt Azure-moln)
  - `login.microsoftonline.us`(Azure-moln för amerikanska myndigheter)

### <a name="configuration-manager-console"></a>Configuration Manager-konsolen

- För Azure AD-token hämtar Azure AD-slut punkten:

  - Offentligt Azure-moln
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure-moln för amerikanska myndigheter
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a>Program uppdateringar

Tillåt att den aktiva program uppdaterings platsen får åtkomst till följande slut punkter så att WSUS och automatiska uppdateringar kan kommunicera med Microsoft Update moln tjänsten:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Mer information om program uppdateringar finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).

### <a name="intranet-firewall"></a>Intranät brand vägg

Du kan behöva lägga till slut punkter till en brand vägg som är mellan två plats system i följande fall:

- Om underordnade platser har en program uppdaterings plats
- Om det finns en fjärran sluten Active Internet-baserad program uppdaterings plats på en plats

#### <a name="software-update-point-on-the-child-site"></a>Programuppdateringsplats på den underordnade platsen

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Hantera Office 365

> [!NOTE]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

Om du använder Configuration Manager för att distribuera och uppdatera Microsoft 365 appar för företag kan du tillåta följande slut punkter:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`Synkronisera program uppdaterings platsen för Microsoft 365 appar för företags klient uppdateringar

- `config.office.com`så här skapar du anpassade konfigurationer för Microsoft 365 appar för företags distributioner

- `contentstorage.osi.office.net`stöd för utvärdering av Office-tillägget för beredskap<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Configuration Manager-konsolen

Datorer med Configuration Manager-konsolen kräver åtkomst till följande Internet slut punkter för vissa funktioner:

### <a name="in-console-feedback"></a>Feedback i konsolen

- `http://petrol.office.microsoft.com`

Mer information om den här funktionen finns i [produkt feedback](../../understand/find-help.md#product-feedback).

### <a name="community-workspace"></a>Community-arbetsyta

#### <a name="documentation-node"></a>Noden dokumentation

Mer information om den här konsol noden finns i [använda Configuration Manager-konsolen](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Community-hubb

Mer information om den här funktionen finns i [Community Hub](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>Arbets ytan övervakning, noden platshierarki

Om du använder den **geografiska vyn**ger du åtkomst till följande slut punkt:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Mer information om vilka slut punkter som krävs för moln tjänsten för Skriv bords analys finns i [Aktivera data delning](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="tenant-attach"></a>Klientkoppling

Mer information om vilka slut punkter som krävs för klient kopplings funktioner finns i [Aktivera klient anslutning](../../../tenant-attach/device-sync-actions.md#internet-endpoints).

## <a name="microsoft-public-ip-addresses"></a>Offentliga IP-adresser från Microsoft

Mer information om IP-adressintervall för Microsoft finns i [Microsofts offentliga IP-utrymme](https://www.microsoft.com/download/details.aspx?id=53602). Dessa adresser uppdateras regelbundet. Det finns ingen kornig het för tjänsten. alla IP-adresser i dessa intervall kan användas.

## <a name="see-also"></a>Se även

- [Portar som används i Configuration Manager](../hierarchy/ports.md)

- [Stöd för proxyserver i Configuration Manager](proxy-server-support.md)
