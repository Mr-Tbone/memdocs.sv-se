---
title: Krav för programuppdatering
titleSuffix: Configuration Manager
description: Läs om kraven för program uppdateringar i Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906706"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Krav för program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln anges kraven för program uppdateringar i Configuration Manager. För var och en av kraven visas de externa beroendena och interna beroendena i separata tabeller.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Program uppdaterings beroenden som är externa för att Configuration Manager  
 I följande avsnitt visas de externa beroendena för program uppdateringar.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) måste vara installerat på plats system servrarna för att köra program uppdaterings platsen, hanterings platsen och distributions platsen. Mer information finns i [Krav för platssystemroller](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) krävs för synkronisering av program uppdateringar och för sökning efter program uppdateringar på klienter. WSUS-servern måste vara installerad innan du skapar program uppdaterings plats rollen. Följande versioner av WSUS stöds för en program uppdaterings plats:  

- WSUS-10.0.14393 (roll i Windows Server 2016)
- WSUS-10.0.17763 (roll i Windows Server 2019) (kräver Configuration Manager 1810 eller senare)
- WSUS 6,2 och 6,3 (roll i Windows Server 2012 och Windows Server 2012 R2)
  - [Kb 3095113 och KB 3159706 (eller motsvarande uppdatering)](#BKMK_wsus2012) krävs för WSUS 6,2 och 6,3 om du distribuerar Windows 10-uppgraderingar.

> [!NOTE]
> - När du har flera program uppdaterings platser på en plats måste du kontrol lera att alla kör samma version av WSUS.

### <a name="wsus-administration-console"></a>WSUS-administrationskonsolen  
WSUS-administrationskonsolen krävs på Configuration Manager plats Server när program uppdaterings platsen finns på en fjärrplats system Server och WSUS inte redan är installerat på plats servern.  

> [!IMPORTANT]  
> - WSUS-versionen på plats servern måste vara samma som den WSUS-version som körs på program uppdaterings platserna.
> - Konfigurera inte WSUS-inställningar med hjälp av WSUS-administrationskonsolen. Configuration Manager ansluter till instansen av WSUS som körs på program uppdaterings platsen och konfigurerar lämpliga inställningar.  


### <a name="windows-update-agent"></a>Windows Update-agent  
 WUA-klienten (Windows Update Agent) krävs på klienterna så att de kan ansluta till WSUS-servern. WUA hämtar listan över program uppdateringar som måste genomsökas för efterlevnad.  

 När du installerar Configuration Manager hämtas den senaste versionen av WUA. När du sedan installerar Configuration Manager-klienten, uppgraderas WUA vid behov. Om installationen Miss lyckas måste du använda en annan metod för att uppgradera WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Program uppdaterings beroenden som är interna att Configuration Manager  
 I följande avsnitt visas de interna beroendena för program uppdateringar i Configuration Manager.  

### <a name="management-points"></a>Hanterings platser  
 Hanterings platser överför information mellan klient datorer och den Configuration Manager webbplatsen. Hanterings platserna krävs för program uppdateringar.  

### <a name="software-update-points"></a>Program uppdaterings platser  
 Du måste installera en program uppdaterings plats på WSUS-servern för att distribuera program uppdateringar i Configuration Manager. Mer information finns i [Installera och konfigurera en program uppdaterings plats](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Distributionsplatser  
 Distributions platser krävs för att lagra innehållet för program uppdateringar. Mer information om hur du installerar distributions platser och hanterar innehåll finns i [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Klientinställningar för programuppdateringar  
Program uppdateringar är aktiverade för klienter som standard. Det finns andra tillgängliga inställningar som styr hur och när klienterna bedömer kompatibilitet för program uppdateringar och styr hur program uppdateringarna installeras.  

 Mer information finns i följande artiklar:  

- [Klient inställningar för program uppdateringar](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services-platser  
 Platssystemrollen Rapporteringstjänstpunkt kan visa rapporter för programuppdateringar. Den här rollen är valfri men rekommenderas. Mer information om hur du skapar en repor ting Services-plats finns i [Konfigurera rapportering](../../core/servers/manage/configuring-reporting.md).  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>Vilka uppdateringar krävs för WSUS 6,2 och 6,3?

Två uppdateringar krävs för att synkronisera **uppgraderings** klassificeringen i WSUS 6,2 och 6,3. Ibland kan du se ett fel som laddar ned eller distribuerar uppgraderingar om de är synkroniserade innan KB3095113 och KB3159706 installerades. Information om möjliga problem finns i nästa avsnitt.  

- Du måste installera [KB 3095113](https://support.microsoft.com/kb/3095113), som lanserades i oktober 2015, på dina program uppdaterings platser och plats servrar innan du synkroniserar **uppgraderingar** -klassificeringen.
  - Den här uppdateringen aktiverar klassificeringen **uppgraderingar** .
- För att kunna underhålla Windows 10 version 1607 och senare måste du installera och konfigurera [KB 3159706](https://support.microsoft.com/help/3159706). KB 3159706 släpptes i maj 2016.
  - Den här uppdateringen gör att WSUS kan dekryptera filerna som används för att uppgradera Windows 10 version 1607 och senare.

>[!IMPORTANT]
> Både KB 3095113 och KB 3159706 ingår i den **samlade säkerheten för månads kvalitet** med början i juli 2017. Det innebär att du kanske inte ser KB 3095113 och KB 3159706 som installerade uppdateringar eftersom de kan ha installerats med en samlad uppdatering. Men om du behöver någon av dessa uppdateringar rekommenderar vi att du installerar en **säkerhets samlad månads kvalitet** från och med oktober 2017 eftersom de innehåller en ytterligare WSUS-uppdatering för att minska minnes användningen på WSUS-ClientWebService.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Hämtning av Windows 10-uppgraderingar Miss lyckas med "fel: ogiltig certifikat signatur" eller 0xc1800118

Uppdateringarna och problemet som beskrivs i det här avsnittet gäller endast för WSUS som körs på Windows Server 2012-eller Windows Server 2012 R2-datorer (WSUS 6,2 och 6,3). Normalt visas bara de problem som beskrivs i det här avsnittet om du har installerat WSUS före 2017 juli och du nyligen har aktiverat klassificeringen **uppgraderingar** . Det är dock möjligt att se de här problemen i andra situationer.

### <a name="historical-information-about-kb-3095113"></a>Historisk information om KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) [släpptes som en snabb korrigering](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113) i oktober 2015 för att lägga till stöd för Windows 10-uppgraderingar i WSUS. Uppdateringen gör att WSUS kan synkronisera och distribuera uppdateringar i klassificeringen **uppgraderingar** för Windows 10.

Om du synkroniserar eventuella uppgraderingar utan att först ha installerat [KB 3095113](https://support.microsoft.com/kb/3095113), fyller du i WSUS-databasen (SUSDB) med oanvändbara data. Dessa data måste rensas innan uppgraderingar kan distribueras korrekt. Windows 10-uppgraderingar i det här läget kan inte hämtas med hjälp av guiden hämta program uppdateringar.

Fel som liknar följande visas på sidan slut för ande i guiden hämta program uppdateringar:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Dessutom loggas fel som liknar följande i filen PatchDownloader. log:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Historiskt sett, när dessa fel uppstod, löses de genom att göra en modifierad version av [lösnings stegen för WSUS](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus). Eftersom de här stegen liknar lösningen för att inte utföra de manuella stegen som krävs efter installationen av KB 3159706 har vi kombinerat båda uppsättningarna med steg till en enda lösning i avsnittet nedan:

- [För att återställa från synkronisering av uppgraderingar innan du installerar kb 3095113 eller kb 3159706](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>Historisk information om KB 3159706

KB 3148812 släpptes ursprungligen i april 2016 för att aktivera att WSUS ska dekryptera. ESD-filer som används för att uppgradera Windows 10-paket. [Kb 3148812 orsakade problem för vissa kunder](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) och ersattes med [KB 3159706](https://support.microsoft.com/help/3159706). KB 3159706 måste installeras på alla dina program uppdaterings platser och plats servrar innan du kan underhålla Windows 10-version 1607 och senare enheter. Problem kan dock uppstå om du inte inser att KB kräver följande manuella steg efter installationen:

1. Kör en upphöjd kommando tolk `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` .
1. Starta om WSUS-tjänsten på alla WSUS-servrar.

Om du inte inser att KB 3159706 hade manuella steg efter installationen, eller om du har synkroniserat i uppgraderingen för Windows 10 1607 innan du installerade KB 3159706, skulle du kunna köra problem med att ansluta till WSUS-konsolen och distribuera uppgraderingen. När en klient hämtade uppgraderings filen får den en [ **0xC1800118** -felkod](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Eftersom lösnings stegen liknar lösningen för att synkronisera uppgraderingar innan du installerar KB 3095113 har vi kombinerat båda uppsättningarna steg till en enda lösning i nästa avsnitt.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>Återställa från att synkronisera uppgraderingar innan du installerar KB 3095113 eller KB 3159706

Följ stegen nedan för att lösa både 0xc1800118-fel och "fel: ogiltig certifikat signatur":

1. Inaktivera klassificeringen **uppgraderingar** i både WSUS och Configuration Manager. Du vill inte att synkroniseringen ska ske förrän du har dirigerat dessa instruktioner.  
   - Avmarkera klassificeringen **uppgraderingar** i egenskaperna för komponenten för program uppdaterings platsen på platsen på den översta nivån.
     - Mer information finns i [Konfigurera klassificeringar och produkter](../get-started/configure-classifications-and-products.md).
   - Avmarkera klassificeringen **uppgraderingar** från WSUS under **produkter och klassificeringar** på [sidan **alternativ** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations), eller Använd PowerShell ISE som kör som administratör.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - Om du delar WSUS-databasen mellan flera WSUS-servrar behöver du bara avmarkera **uppgraderingarna** en gång för varje databas.  
1. Från en upphöjd kommando tolk på varje WSUS-server kör du: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` . Starta sedan om WSUS-tjänsten på alla WSUS-servrar.
   -  WSUS placerar databasen i [enanvändarläge](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) innan den kontrollerar för att se om servicen behövs. Underhållet körs eller körs inte utifrån resultatet av kontrollen. Databasen placeras sedan i läget för flera användare. 
   - Om du delar WSUS-databasen mellan flera WSUS-servrar behöver du bara utföra den här underhållet en gång för varje databas.
1. Ta bort alla Windows 10-uppgraderingar från varje WSUS-databas med hjälp av PowerShell ISE som kör som administratör.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Ta bort filer från tabellen tbFile från alla WSUS-databaser som används av dina program uppdaterings platser. Kör följande kommandon från SQL Server Management Studio på WSUS-databasen:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Starta synkroniseringen av program uppdateringar på platsen på den översta nivån i Configuration Manager och vänta tills den är klar. En fullständig synkronisering sker eftersom vi gjorde en ändring i klassificeringarna Configuration Manager när vi tog bort **uppgraderingar**. (Mer information finns i [Synkronisera program uppdateringar](../get-started/synchronize-software-updates.md).
1. Välj klassificeringen **uppgraderingar** i egenskaperna för komponenten för program uppdaterings plats. Starta sedan en annan synkronisering av program uppdateringar för att flytta tillbaka **uppgraderingarna** till WSUS och Configuration Manager. Du behöver inte aktivera klassificeringen **uppgraderingar** i WSUS eftersom Configuration Manager gör det åt dig.
1. Om dina klienter har fått **0xC1800118** -felkoden vid hämtning av en uppgradering, måste du ta bort det data lager som används av Windows Update agenten. Du kan också behöva ta bort den dolda mappen ~ BT på enheten. Nästa gång klienten genomsöks, kommer den att vara en fullständig genomsökning mot WSUS-servern i stället för en delta. Du kan använda ett PowerShell-skript som liknar följande exempel skript:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Nästa steg
[Förbered för hantering av programuppdateringar](../get-started/prepare-for-software-updates-management.md)
