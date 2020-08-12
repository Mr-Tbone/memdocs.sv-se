---
title: Konfigurera BitLocker-portaler
titleSuffix: Configuration Manager
description: Installera hanterings komponenter för BitLocker för självbetjänings portalen och webbplatsen för administration och övervakning
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dbd782c97d11f8077c18796c87c7880eb26f3f3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129162"
---
# <a name="set-up-bitlocker-portals"></a>Konfigurera BitLocker-portaler

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

Om du vill använda följande komponenter för BitLocker-hantering i Configuration Manager måste du först installera dem:

- Självbetjänings Portal för användare
- Webbplatsen för administration och övervakning (supportavdelningen)

Du kan installera portalerna på en befintlig plats Server eller plats system server med IIS installerat eller använda en fristående webb server för att vara värd för dem.

> [!NOTE]
> Från och med version 2006 kan du installera tjänsten BitLocker-självbetjänings Portal och webbplatsen för administration och övervakning på den centrala administrations webbplatsen.<!-- 5925693 -->
>
> I version 2002 och tidigare installerar du bara självbetjänings portalen och webbplatsen för administration och övervakning med en primär plats databas. I en-hierarki installerar du de här webbplatserna för varje primär plats.

Innan du börjar ska du kontrol lera [kraven](../../plan-design/bitlocker-management.md#prerequisites) för de här komponenterna.

## <a name="run-the-script"></a>Kör skriptet

Utför följande åtgärder på mål webb servern:

> [!NOTE]
> Beroende på din webbplats design kan du behöva köra skriptet flera gånger. Du kan till exempel köra skriptet på hanterings platsen för att installera webbplatsen för administration och övervakning. Kör den sedan igen på en fristående webb server för att installera självbetjänings portalen.

1. Kopiera följande filer från `SMSSETUP\BIN\X64` mappen Configuration Manager-installationsmapp på plats servern till en lokal mapp på mål servern:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Kör PowerShell som administratör och kör skriptet som liknar följande kommando rad:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Exempel:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > I det här kommando rads exemplet används alla möjliga parametrar för att visa deras användning. Justera din användning enligt dina krav i din miljö.

Efter installationen får du åtkomst till portalerna via följande URL: er:

- Självbetjänings Portal:`https://webserver.contoso.com/SelfService`
- Webbplatsen för administration och övervakning:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft rekommenderar men kräver inte användning av HTTPS. Mer information finns i [så här konfigurerar du SSL i IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="script-usage"></a>Skript användning

Den här processen använder ett PowerShell-skript MBAMWebSiteInstaller.ps1 för att installera dessa komponenter på webb servern. Den accepterar följande parametrar:

- `-SqlServerName <ServerName>`(obligatoriskt): det fullständigt kvalificerade domän namnet för den primära platsens databas server.

- `-SqlInstanceName <InstanceName>`: SQL Server instans namnet för den primära plats databasen. Ta inte med den här parametern om SQL använder standard instansen.

- `-SqlDatabaseName <DatabaseName>`(obligatoriskt): namnet på den primära plats databasen, till exempel `CM_ABC` .

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: Webb tjänstens URL för den primära platsens rapporterings tjänst plats. Det är **URL-värdet för webb tjänsten** i **repor ting Services Configuration Manager**.

    > [!NOTE]
    > Den här parametern är att installera **rapporten för återställnings granskning** som är länkad från webbplatsen för administration och övervakning. Som standard innehåller Configuration Manager andra hanterings rapporter för BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Till exempel `contoso\BitLocker help desk users` . En domän användar grupp vars medlemmar har åtkomst till **hanterings** områden för TPM och **enhets återställning** på webbplatsen för administration och övervakning. När du använder dessa alternativ måste den här rollen fylla i alla fält, inklusive användarens domän och konto namn.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Till exempel `contoso\BitLocker help desk admins` . En domän användar grupp vars medlemmar har åtkomst till alla återställnings områden på webbplatsen för administration och övervakning. När hjälpa användare att återställa sina enheter, behöver den här rollen bara ange återställnings nyckeln.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Till exempel `contoso\BitLocker report users` . En domän användar grupp vars medlemmar har skrivskyddad åtkomst till **rapport** avsnittet på webbplatsen för administration och övervakning.

    > [!NOTE]
    > Installations skriptet skapar inte de domän användar grupper som du anger i parametrarna **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**och **-MbamReportUsersGroupName** . Innan du kör skriptet ska du se till att skapa dessa grupper.
    >
    > När du anger parametrarna **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**och **-MbamReportUsersGroupName** , måste du ange både domän namnet och grupp namnet. Använd formatet `"domain\user_group"`. Uteslut inte domän namnet. Om domän namnet eller grupp namnet innehåller blank steg eller specialtecken, omger du parametern med citat tecken ( `"` ).

- `-SiteInstall Both`: Ange vilken av komponenterna som ska installeras. Giltiga alternativ är:
  - `Both`: Installera båda komponenterna
  - `HelpDesk`: Installera endast webbplatsen Administration och övervakning
  - `SSP`: Installera endast självbetjänings portalen

- `-IISWebSite`: Den webbplats där skriptet installerar MBAM-webbprogram. Som standard används IIS-standardwebbplatsen. Skapa den anpassade webbplatsen innan du använder den här parametern.

- `-InstallDirectory`: Sökvägen där skriptet installerar filerna för webb programmet. Den här sökvägen är som standard `C:\inetpub` . Skapa den anpassade katalogen innan du använder den här parametern.

- `-Uninstall`: Avinstallerar webb Portal webbplatser för BitLocker-hantering på en webb server där de redan har installerats.

## <a name="verify"></a>Verifiera

Övervaka och Felsök med hjälp av följande loggar:

- Windows-händelseloggar under **Microsoft-Windows-MBAM-Web**. Mer information finns i [om händelse](../../tech-ref/bitlocker/about-event-logs.md) loggar för BitLocker och [Server händelse loggar](../../tech-ref/bitlocker/server-event-logs.md).

- Spårnings loggar för varje komponent finns på följande standard platser:

  - Självbetjänings Portal:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Webbplatsen för administration och övervakning:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Mer felsöknings information finns i [Felsöka BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Nästa steg

[Anpassa självbetjäningsportalen](customize-self-service-portal.md)

Mer information om hur du använder de komponenter som du har installerat finns i följande artiklar:

- [Webbplatsen för administration och övervakning av BitLocker](helpdesk-portal.md)
- [Själv service portal för BitLocker](self-service-portal.md)
