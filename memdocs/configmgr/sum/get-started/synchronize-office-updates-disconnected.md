---
title: Synkronisera uppdateringar av Microsoft 365 appar utan Internet anslutning
titleSuffix: Configuration Manager
description: Synkronisera uppdateringar av Microsoft 365-appar på den översta program uppdaterings platsen som är frånkopplad från Internet.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 49e0f5e1dff466e62cdba0def917dd34510e48ee
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696777"
---
# <a name="synchronize-microsoft-365-apps-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> Synkronisera uppdateringar av Microsoft 365 appar från en frånkopplad program uppdaterings plats

*Gäller för: Configuration Manager (aktuell gren)*
<!--4065163-->
Från och med Configuration Manager version 2002 kan du använda ett verktyg för att importera uppdateringar av Microsoft 365 appar från en ansluten WSUS-server till en frånkopplad Configuration Manager-miljö. Tidigare när du exporterade och importerade metadata för program som har uppdaterats i frånkopplade miljöer kunde du inte distribuera uppdateringar av Microsoft 365 appar. Uppdateringar för Microsoft 365-appar kräver ytterligare metadata som hämtats från ett Office API och Office CDN, vilket inte är möjligt för frånkopplade miljöer.

> [!Note]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

## <a name="prerequisites"></a>Förutsättningar

- En ansluten WSUS-server med Internet som kör minst Windows Server 2012.
- WSUS-servern behöver anslutning till följande två Internet slut punkter:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Kopiera verktyget OfflineUpdateExporter och dess beroenden till den Internet anslutna WSUS-servern.
  - Verktyget och dess beroenden finns i katalogen ** &lt; ConfigMgrInstallDir>/tools/offlineupdateexporter** .
- Användaren som kör verktyget måste vara en del av gruppen **WSUS-administratörer** .
- Katalogen som har skapats för att lagra Microsoft 365 appar uppdatera metadata och innehåll bör ha lämpliga åtkomst kontrol listor (ACL: er) för att skydda filerna.
    - Katalogen måste också vara tom.
- Data som flyttas från WSUS-servern online till den frånkopplade miljön bör flyttas på ett säkert sätt.

> [!IMPORTANT]
> Innehållet kommer att hämtas för alla Microsoft 365-programmeringsspråk. Varje uppdatering kan ha cirka 10 GB innehåll.

## <a name="synchronize-then-decline-unneeded-microsoft-365-apps-updates"></a>Synkronisera sedan neka onödiga Microsoft 365 uppdateringar av appar

1. Öppna WSUS-konsolen på din Internet-anslutna WSUS.
1. Välj **alternativ** **och sedan produkter och klassificeringar**.
1. På fliken **produkter** väljer du **Office 365-klient** och väljer **uppdateringar** på fliken **klassificeringar** . [ ![ produkter och klassificeringar för uppdateringar av Microsoft 365 appar i WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Gå till **synkroniseringar** och välj **Synkronisera nu** för att hämta uppdateringar för Microsoft 365 appar till WSUS.
1. När synkroniseringen är klar avvisar du eventuella uppdateringar av Microsoft 365 appar som du inte vill distribuera med Configuration Manager. Du behöver inte godkänna uppdateringar av Microsoft 365 appar för att de ska kunna laddas ned.  
   - Om du avböjer oönskade uppdateringar av Microsoft 365 appar i WSUS så hindras de inte från att exporteras under en WsusUtil.exe export, men den stoppar OfflineUpdateExporter-verktyget från att hämta innehållet för dem.
   - OfflineUpdateExporter-verktyget hämtar uppdateringar för Microsoft 365 appar åt dig. Andra produkter måste fortfarande godkännas för nedladdning om du exporterar uppdateringar för dem.
    - Skapa en [ny uppdaterings vy i WSUS](/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) för att enkelt se och neka onödiga Microsoft 365 uppdateringar av appar i WSUS.
1. Om du godkänner andra produkt uppdateringar för hämtning och export väntar du tills innehålls hämtningen har slutförts innan du kör WsusUtil.exe exportera och kopiera innehållet i mappen WSUSContent. Mer information finns i avsnittet om att [Synkronisera program uppdateringar från en frånkopplad program uppdaterings plats](synchronize-software-updates-disconnected.md)

## <a name="exporting-the-microsoft-365-apps-updates"></a>Exportera uppdateringar för Microsoft 365-appar

1. Kopiera mappen OfflineUpdateExporter från Configuration Manager till den anslutna Internet-WSUS-servern.
    - Verktyget och dess beroenden finns i katalogen ** &lt; ConfigMgrInstallDir>/tools/offlineupdateexporter** .
1. Från en kommando tolk på den Internet anslutna WSUS-servern kör du verktyget med följande användning: **OfflineUpdateExporter.exe-O-D &lt; mål sök väg>**

   |OfflineUpdateExporter-parameter|Beskrivning|
   |---|---|
   |**-O**|  **-Kontor**. Anger att produkten för uppdaterings export är Office 365 eller Microsoft 365 appar|
   |**-D**|**-Destination**. Målet är en obligatorisk parameter och hela sökvägen till målmappen behövs.|

   - **OfflineUpdateExporter** -verktyget gör följande:
      - Ansluter till WSUS
      - Läser Microsoft 365 appar uppdatera metadata i WSUS
      - Laddar ned innehållet och eventuella ytterligare metadata som krävs av Microsoft 365 appar uppdateringar till målmappen

1. I kommando tolken på den Internet anslutna WSUS-servern navigerar du till mappen som innehåller WsusUtil.exe. Som standard finns verktyget i%*ProgramFiles*% \ Update Services\Tools. Om verktyget exempelvis finns på standardplatsen skriver du **cd %ProgramFiles%\Update Services\Tools**.
   - Om du använder Windows Server 2012 kontrollerar du att [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) är installerat på WSUS-servrarna.
   - Användaren som kör WsusUtil-verktyget måste vara medlem i den lokala gruppen Administratörer på-servern.

1. Skriv följande för att exportera metadata för program uppdateringar till en GZIP-fil:  

    **WsusUtil.exe exportera***PackageName*-*loggfil*      

    Exempel:  

    **WsusUtil.exe exportera export.xml. gz export. log**

1. Kopiera filen **export.xml. gz** till WSUS-servern på den översta nivån på det frånkopplade nätverket.
1. Om du har godkänt uppdateringar för andra produkter kopierar du innehållet i mappen WSUSContent till den mappade mappen WSUSContent i den översta nivån.
1. Kopiera målmappen som används för **OfflineUpdateExporter** till den översta nivån Configuration Manager plats Server på det frånkopplade nätverket.

## <a name="import-the-microsoft-365-apps-updates"></a>Importera uppdateringar för Microsoft 365 appar

1. På den frånkopplade WSUS-servern på den översta nivån importerar du metadata för uppdateringen från den **export.xml. gz** som du genererade på den Internet anslutna WSUS-servern.
   
    Exempel:  

    **WsusUtil.exe importera export.xml. gz import. log**
    
    Som standard finns WsusUtil.exe-verktyget i%*ProgramFiles*% \ Update Services\Tools.

1. När importen är klar måste du konfigurera en plats kontroll egenskap på den frånkopplade Configuration Manager plats servern på den översta nivån. Den här konfigurations ändringen pekar Configuration Manager till innehållet för Microsoft 365 appar. Ändra egenskapens konfiguration:
   1. Kopiera [PowerShell-skriptet O365OflBaseUrlConfigured](#bkmk_o365_script) till den översta nivån frånkopplade Configuration Manager plats servern.
   1. Ändra `"D:\Office365updates\content"` till den fullständiga sökvägen till den kopierade katalogen som innehåller Microsoft 365 Apps innehåll och metadata som genererats av OfflineUpdateExporter.
      > [!IMPORTANT]
      > Endast lokala sökvägar fungerar för egenskapen O365OflBaseUrlConfigured.
   1. Spara skriptet som `O365OflBaseUrlConfigured.ps1`
   1. Kör på en upphöjd PowerShell-period på den frånkopplade Configuration Manager plats servern på den översta nivån `.\O365OflBaseUrlConfigured.ps1` .
   1. Starta om **SMS_EXECUTIVE** -tjänsten på plats servern.
1. I **Configuration Manager** -konsolen navigerar du till **Administration**  >  **plats konfiguration**  >  **platser**.
1. Högerklicka på platsen på den högsta nivån och välj sedan **Konfigurera plats komponenter**  >  **program uppdaterings plats**.
1. På fliken **klassificeringar** väljer du *uppdateringar*. På fliken **produkter** väljer du *Office 365-klient*.
1. [Synkronisera program uppdateringar](synchronize-software-updates.md#manually-start-software-updates-synchronization) för Configuration Manager
1. När synkroniseringen är klar använder du din normala process för att distribuera uppdateringar för Microsoft 365 appar.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> Proxykonfiguration

- Proxykonfigurationen är inte inbyggt i verktyget. Om proxy anges i Internet alternativen på den server där verktyget körs, så kommer det i teorin att användas och ska fungera korrekt.
   - Från en kommando tolk kör `netsh winhttp show proxy` du för att se den konfigurerade proxyn.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> Ändra egenskapen O365OflBaseUrlConfigured

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Nästa steg

[Lägga till programuppdateringar i en uppdateringsgrupp](../deploy-use/add-software-updates-to-an-update-group.md)