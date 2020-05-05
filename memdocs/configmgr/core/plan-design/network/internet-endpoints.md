---
title: Krav för Internet-åtkomst
titleSuffix: Configuration Manager
description: Lär dig om Internet-slutpunkter så att du kan använda alla funktioner i Configuration Manager funktioner.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58afaf564a8afaba4569755575fcc7c1757c5529
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110142"
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
> Tjänst anslutnings punkten använder Microsoft Intune tjänsten när den ansluter till `go.microsoft.com` eller. `manage.microsoft.com` Det finns ett känt problem där Intune Connector upplever anslutnings problem om Baltimore CyberTrust-rotcertifikatet inte är installerat eller är skadat på tjänst anslutnings punkten. Mer information finns i [KB 3187516: tjänst anslutnings punkten hämtar inte uppdateringar](https://support.microsoft.com/help/3187516).  

Från och med version 2002, om Configuration Manager-platsen inte kan ansluta till obligatoriska slut punkter för en moln tjänst, genererar den en kritisk status meddelande-ID 11488. När den inte kan ansluta till tjänsten ändras SMS_SERVICE_CONNECTOR komponent status till kritisk. Visa detaljerad status i noden [komponent status](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) i Configuration Manager-konsolen.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/>Uppdateringar och underhåll

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

- `management.azure.com`  

## <a name="co-management"></a>Samhantering

Om du registrerar Windows 10-enheter till Microsoft Intune för samhantering kontrollerar du att enheterna kan komma åt de slut punkter som krävs av Intune. Mer information finns i [nätverks slut punkter för Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).

## <a name="microsoft-store-for-business"></a>Microsoft Store för företag

Om du integrerar Configuration Manager med [Microsoft Store för företag](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)kontrollerar du att tjänst anslutnings punkten och de riktade enheterna har åtkomst till moln tjänsten. Mer information finns i [konfiguration av Microsoft Store för företag-proxy](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Moln tjänster

<!-- SCCMDocs-pr #3402 -->

I det här avsnittet beskrivs följande funktioner:

- Cloud Management Gateway (CMG)
- Distributions plats för moln (CDP)
- Azure Active Directory (Azure AD)-integration
- Azure AD-baserad identifiering

För distribution av CMG/CDP-tjänst behöver **tjänst anslutnings punkten** åtkomst till:

- Specifika Azure-slutpunkter är olika per miljö beroende på konfigurationen. Configuration Manager lagrar dessa slut punkter i plats databasen. Fråga tabellen **AzureEnvironments** i SQL Server efter listan över Azure-slutpunkter.  

**CMG-anslutnings punkten** behöver åtkomst till följande tjänst slut punkter:

- Service Management-slut punkt:`https://management.core.windows.net/`  

- Lagrings slut `<name>.blob.core.windows.net` punkt: och`<name>.table.core.windows.net`

    Där `<name>` är namnet på moln tjänsten för din CMG eller CDP. Om din CMG till exempel är `GraniteFalls.CloudApp.Net`, så är den första lagrings slut punkten som `GraniteFalls.blob.core.windows.net`tillåts.<!-- SCCMDocs#2288 -->

För hämtning av Azure AD-token av **Configuration Manager-konsolen** och- **klienten**:

- ActiveDirectoryEndpoint`https://login.microsoftonline.com/`  

För identifiering av Azure AD-användare behöver **tjänst anslutnings punkten** åtkomst till:

- Version 1810 och tidigare: Azure AD Graph-slutpunkt`https://graph.windows.net/`  

- Version 1902 och senare: Microsoft Graph slut punkt`https://graph.microsoft.com/`

Plats systemet för moln hanterings platsen (CMG) stöder användning av en webbproxy. Mer information om hur du konfigurerar den här rollen för en proxy finns i [stöd för proxy server](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Anslutnings punkten för CMG måste bara ansluta till CMG-tjänstens slut punkter. Den behöver inte åtkomst till andra Azure-slutpunkter.

Mer information om CMG finns i [Planera för CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).

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

## <a name="configuration-manager-console"></a>Configuration Manager-konsolen

Datorer med Configuration Manager-konsolen kräver åtkomst till följande Internet slut punkter för vissa funktioner:

### <a name="in-console-feedback"></a>Feedback i konsolen

- `http://petrol.office.microsoft.com`

Mer information om den här funktionen finns i [produkt feedback](../../understand/find-help.md#product-feedback).

### <a name="community-workspace-documentation-node"></a>Community-arbetsyta, noden dokumentation

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Mer information om den här konsol noden finns i [använda Configuration Manager-konsolen](../../servers/manage/admin-console.md).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Arbets ytan övervakning, noden platshierarki

Om du använder den **geografiska vyn**ger du åtkomst till följande slut punkt:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Mer information om vilka slut punkter som krävs för moln tjänsten för Skriv bords analys finns i [Aktivera data delning](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Offentliga IP-adresser från Microsoft

Mer information om IP-adressintervall för Microsoft finns i [Microsofts offentliga IP-utrymme](https://www.microsoft.com/download/details.aspx?id=53602). Dessa adresser uppdateras regelbundet. Det finns ingen kornig het för tjänsten. alla IP-adresser i dessa intervall kan användas.

## <a name="see-also"></a>Se även

- [Portar som används i Configuration Manager](../hierarchy/ports.md)

- [Stöd för proxyserver i Configuration Manager](proxy-server-support.md)
