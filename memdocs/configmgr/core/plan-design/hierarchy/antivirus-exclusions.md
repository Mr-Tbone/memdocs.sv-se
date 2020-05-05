---
title: Antivirus undantag
titleSuffix: Configuration Manager
description: Läs om rekommenderade Antivirus undantag för användning vid fel sökning av möjliga problem.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720298"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Rekommenderade Antivirus undantag för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller rekommendationer som kan hjälpa en administratör att fastställa orsaken till eventuell instabilitet på en dator som kör en version av Configuration Manager-plats servrar, plats system och klienter som stöds när den används tillsammans med antivirus program.

> [!IMPORTANT]
>
> - Vi rekommenderar att du tillfälligt tillämpar dessa procedurer för att utvärdera ett system. Om systemets prestanda eller stabilitet förbättras av rekommendationerna i den här artikeln kan du kontakta leverantören av antivirus programmet för instruktioner eller en uppdaterad version av antivirus programmet.
> - Den här artikeln innehåller information som visar hur du sänker säkerhets inställningar eller hur du tillfälligt inaktiverar säkerhetsfunktioner på en dator. Du kan göra dessa ändringar för att förstå vilken typ av problem som gäller. Innan du gör dessa ändringar rekommenderar vi att du utvärderar de risker som är associerade med att implementera den här lösningen i din specifika miljö.

## <a name="possible-symptoms"></a>Möjliga symptom 

Real tids skydd i Antivirus kan orsaka många problem på Configuration Manager plats servrar, plats system och klienter.

Följande är en icke-omfattande lista över möjliga symptom:

- Fjärrplatsens system komponenter är inte installerade. SiteComp. log, Distmgr. log, hman. log eller andra Configuration Manager loggfiler kan innehålla fel som fel 80070005.
- Det går inte att installera den Configuration Manager klienten med push-installation av klienter.
- Klient inventerings informationen är felaktig, saknas eller är inaktuell.
- Efter släpning sker i *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes Folders.
- Software Center är inte ifyllt av distribuerad program vara på klient system eller startar inte. Dessutom kan filen CCMRepair. log innehålla fel som liknar följande exempel:

  > Databas verifieringen misslyckades med resultatet: 0x80004005 visas men DB: C:\Windows\CCM\filename.sdf kunde inte öppnas, vilket hoppar över databas reparation.

- Det går inte att installera program vara som distribueras till klienter.
- Kompatibilitetsinformation för program varu distributioner är felaktigt.

## <a name="exclusions"></a>Undantag

För att förhindra sådana problem rekommenderar vi att du lägger till följande undantag för real tids skydd:

### <a name="default-installation-folders"></a>Standardmappar för installation

|  |  |
| - | - |
|*Installationsmapp för ConfigMgr*  |  %Program%\Microsoft-Configuration Manager  |  
|*Installations katalog för MP*  |% ProgramFiles% \ SMS_CCM  |  
|*Installationsmapp för klienter*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Mappar undantag för plats servrar

- \Inboxes för *ConfigMgr-installation*
- \Logs för *ConfigMgr-installation*
- \EasySetupPayload för *ConfigMgr-installation*

### <a name="folder-exclusions-for-site-systems"></a>Mappar undantag för plats system

- Hanterings platser
  - \ServiceData för *installation av MP*
  - Något av följande:
    - \MP\OUTBOXES för *ConfigMgr-installation*
    - \SMS\MP\OUTBOXES för *installations enhet*
- Distributionsplatser
  - *\ServiceData för installationsmapp*
  - *ContentLib_Drive*\ SMS_DP $
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG $
- Plats databas servrar
  - [Så här väljer du antivirus program som ska köras på datorer som kör SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Mappar undantag för klienter

- *Client Installation Folder*Installationsmapp för klient\*. SDF\\
- *\ServiceData för installationsmapp*
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *\Logs för installationsmapp*

### <a name="file-exclusions-for-mps"></a>Fil undantag för MPs

- POL00000. pol i
  - \PolReqStaging för *installation av MP*

### <a name="process-exclusions"></a>Processundantag

Process undantag är bara nödvändigt om aggressiva antivirus program anser Configuration Manager programfiler (. exe-filer) ska vara högrisk processer.

- \Bin\64\Smsexec.exe för *ConfigMgr-installation*
- Någon av följande processer:
  - *\Ccmexec.exe för installationsmapp*
  - \Ccmexec.exe för *installation av MP*
- \CmRcService.exe för *klient installation*(klient sidan)
- \Bin\64\Sitecomp.exe för *ConfigMgr-installation*
- \Bin\64\Smswriter.exe för *ConfigMgr-installation*
- *Installations katalogen för ConfigMgr*\bin\64\Smssqlbkup.exe eller SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- \Bin\64\Cmupdate.exe för *ConfigMgr-installation*
- \Ccmrepair.exe för *klient installation*(klient sidan)
- %*windir*% \ CCMSetup\Ccmsetup.exe (klient sidan)

## <a name="next-steps"></a>Nästa steg

Mer information om antivirus undantag finns i följande artiklar:

[Configuration Manager Current Branch Antivirus undantag – System Center Premier Field Engineer-bloggen](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[Uppdaterade System Center 2012 Configuration Manager Antivirus undantag med mer information om OSD och start avbildningar](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[Så här väljer du antivirus program som ska köras på datorer som kör SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Rekommendationer för virus genomsökning för företags datorer som kör Windows-versioner som stöds för närvarande](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
