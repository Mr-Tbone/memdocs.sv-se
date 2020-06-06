---
title: Microsoft Connected Cache
titleSuffix: Configuration Manager
description: Använd din Configuration Manager distributions plats som en lokal cache-server för leverans optimering
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70d4930da712eccff8bdb1f1986a68aa5fe77644
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455284"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Microsoft Connected cache i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--3555764-->

Från och med version 1906 kan du installera en Microsoft-ansluten cache-server på dina distributions platser. Genom att cachelagra det här innehållet lokalt kan dina klienter dra nytta av leverans optimerings funktionen, men du kan skydda WAN-länkar.

> [!NOTE]
> Från och med version 1910 heter funktionen nu **Microsoft Connected cache**. Det kallades tidigare för leverans optimering i nätverket.

Den här cache-servern fungerar som en transparent cache på begäran för innehåll som hämtas av leverans optimering. Använd klient inställningar för att kontrol lera att den här servern endast erbjuds till medlemmar i den lokala Configuration Managers gränser gruppen.

Den här cachen är separat från Configuration Manager distributions plats innehåll. Om du väljer samma enhet som distributions plats rollen lagrar den innehåll separat.

> [!Note]  
> Den anslutna cache-servern är ett program som är installerat på Windows Server. Det här programmet är fortfarande under utveckling.

## <a name="how-it-works"></a>Så här fungerar det

När du konfigurerar klienter att använda den anslutna cache-servern, begär de inte längre Microsoft Cloud-hanterat innehåll från Internet. Klienterna begär det här innehållet från den cache-server som är installerad på distributions platsen. Den lokala servern cachelagrar det här innehållet med hjälp av IIS-funktionen för-routning av programbegäran (ARR). Sedan kan cache-servern snabbt svara på eventuella framtida förfrågningar om samma innehåll. Om den anslutna cache-servern inte är tillgänglig eller om innehållet inte har cachelagrats, laddar klienterna ned innehållet från Internet. Klienter använder också leverans optimering, så du kan ladda ned delar av innehållet från peer-datorer i nätverket.

![Diagram över hur anslutna cache fungerar](media/3555764-microsoft-connected-cache.png)

1. Klienten söker efter uppdateringar och hämtar adressen för Content Delivery Network (CDN).

2. Configuration Manager konfigurerar inställningar för leverans optimering (inställningar) på klienten, inklusive cache server namnet.

3. Klient A begär innehåll från Server-cache-servern.

4. Om cacheminnet inte innehåller innehållet hämtar cache-servern den från CDN.

5. Om cache-servern inte svarar, laddar klienten ned innehållet från CDN.

6. Klienter använder gör för att hämta delar av innehållet från peer-datorer.

## <a name="prerequisites-and-limitations"></a>Krav och begränsningar

- En *lokal* distributions plats med följande konfigurationer:

  - Köra Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 eller Windows Server 2019

  - Standard webbplatsen som är aktive rad på port 80

  - Förinstallera inte funktionen för IIS- [programbegäran](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (arr). Den anslutna cachen installerar ARR och konfigurerar dess inställningar. Microsoft kan inte garantera att den anslutna cachens ARR-konfiguration inte hamnar i konflikt med andra program på servern som också använder den här funktionen.

  - Distributions platsen kräver Internet åtkomst till Microsoft-molnet. De speciella URL: erna kan variera beroende på det aktuella molnbaserade innehållet. Se till att även tillåta slut punkter för leverans optimering. Mer information finns i [krav för Internet åtkomst](../network/internet-endpoints.md).

  - Från och med version 2002 kan det anslutna cache-programmet använda en oautentiserad proxyserver för Internet åtkomst. Mer information finns i [Konfigurera proxyservern för en plats system Server](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

- Klienter som kör Windows 10 version 1709 eller senare

## <a name="enable-connected-cache"></a>Aktivera ansluten cache

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** .

1. Välj en *lokal* distributions plats och välj sedan **Egenskaper**i menyfliksområdet.

1. I egenskaperna för distributions plats rollen går du till fliken **Allmänt** och konfigurerar följande inställningar:  

    1. Aktivera alternativet för att **tillåta att den här distributions platsen används som Microsoft-ansluten cache-server**  

        Visa och godkänn licens villkoren.

    2. **Lokal enhet som ska användas**: Välj den disk som ska användas för cacheminnet. **Automatisk** är standardvärdet som använder den disk som har mest ledigt utrymme. <sup> [Anmärkning 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Du kan ändra den här enheten senare. Cachelagrat innehåll försvinner, om du inte kopierar det till den nya enheten.

    3. **Disk utrymme**: Välj mängden disk utrymme som ska reserveras i GB eller en procent andel av det totala disk utrymmet. Som standard är det här värdet 100 GB.

        > [!Note]  
        > Standard storleken för cacheminnet bör vara tillräcklig för de flesta kunder. Du kan ändra cache-storleken senare.
        >
        > Om cachestorleken på disken överskrider det allokerade utrymmet rensar ARR utrymme genom att ta bort innehållet baserat på dess inbyggda heuristik.<!-- SCCMDocs#2045 -->

    4. **Behåll cachen när den anslutna cache-servern inaktive ras**: om du tar bort cache-servern och aktiverar det här alternativet, behåller servern cacheminnets innehåll på disken.  

1. I klient inställningar i gruppen för **leverans optimering** konfigurerar du inställningen för att **Aktivera enheter som hanteras av Configuration Manager att använda Microsoft-anslutna cache-servrar för innehålls hämtning**.  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a>Anmärkning 1: om val av enhet

Om du väljer **Automatisk**används **No_sms_on_drive. SMS** -filen när Configuration Manager installerar den anslutna cache-komponenten. Distributions platsen har till exempel filen `C:\no_sms_on_drive.sms` . Även om enheten C: har mest ledigt utrymme, Configuration Manager konfigurerar det anslutna cacheminnet för att använda en annan enhet för cacheminnet.

Om du väljer en speciell enhet som redan har **No_sms_on_drive. SMS** -filen ignorerar Configuration Manager filen. Det finns en uttrycklig avsikt att konfigurera den anslutna cachen för att använda enheten. Distributions platsen har till exempel filen `F:\no_sms_on_drive.sms` . När du konfigurerar distributions platsens egenskaper för att använda enhets enheten **f:** Configuration Manager konfigureras den anslutna cachen så att den använder enheten f: för dess cacheminne.

Ändra enheten efter att du har installerat den anslutna cachen:

- Konfigurera distributions platsens egenskaper manuellt så att de använder en viss enhets beteckning.

- Om värdet är inställt på automatisk skapar du först filen **No_sms_on_drive. SMS** . Gör sedan några ändringar i egenskaperna för distributions platsen för att utlösa en konfigurations ändring.

### <a name="automation"></a>Automation

<!-- SCCMDocs#1911 -->

Du kan använda Configuration Manager SDK för att automatisera konfigurationen av Microsoft Connected cache-inställningar på en distributions plats. När det gäller alla webbplats roller använder du [klassen SMS_SCI_SYSRESUSE WMI](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md). Mer information finns i [programmering av plats roller](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles).

När du uppdaterar **SMS_SCI_SysResUse** -instansen för distributions platsen anger du följande egenskaper:

- **AgreeDOINCLicense**: ange att `1` accepterar licens villkoren.
- **Flaggor**: aktivera `|= 4` , inaktivera`&= ~4`
- **DiskSpaceDOINC**: Ange till `Percentage` eller`GB`
- **RetainDOINCCache**: Ange till `0` eller`1`
- **LocalDriveDOINC**: Ange till `Automatic` , eller en speciell enhets beteckning, till exempel `C:` eller`D:`

## <a name="verify"></a>Verifiera

När klienter laddar ned moln hanterat innehåll använder de leverans optimering från den cache-server som är installerad på distributions platsen. Moln hanterat innehåll innehåller följande typer:

- Microsoft Store-appar
- Windows-funktioner på begäran, till exempel språk
- Om du aktiverar [Windows Update för affärs principer](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md): Windows 10-funktions-och kvalitets uppdateringar
- För [samhanterings arbets belastningar](../../../comanage/workloads.md):
  - Windows Update för företag: Windows 10 funktions-och kvalitets uppdateringar
  - Office Klicka-och-kör-appar: Office-appar och uppdateringar
  - Klient program: Microsoft Store appar och uppdateringar
  - Endpoint Protection: definitions uppdateringar för Windows Defender

I Windows 10 version 1809 eller senare kontrollerar du det här beteendet med Windows PowerShell-cmdleten **Get-DeliveryOptimizationStatus** . I cmdlet-utdata granskar du **BytesFromCacheServer** -värdet. Mer information finns i [övervaka leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Om cache-servern returnerar HTTP-problem går leverans optimerings klienten tillbaka till den ursprungliga moln källan.

Mer detaljerad information finns i [felsöka Microsoft Connected cache i Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a>Stöd för Intune Win32-appar

<!--5032900-->

Från och med version 1910 kan de hantera Microsoft Intune Win32-appar till samhanterade klienter när du aktiverar ansluten cache på Configuration Manager distributions platser.

### <a name="prerequisites"></a>Krav

#### <a name="client"></a>Klient

- Uppdatera klienten till den senaste versionen.

- Klient enheten måste ha minst 4 GB minne.

    > [!TIP]
    > Använd följande grup princip inställning: dator konfiguration > Administrativa mallar > Windows-komponenter > leverans optimering > **minsta ram-kapacitet (inklusive) som krävs för att aktivera användning av peer-cachelagring (i GB)**.

#### <a name="site"></a>Webbplats

- Aktivera ansluten cache på en distributions plats. Mer information finns i [Microsoft Connected cache](microsoft-connected-cache.md).

- Klienten och den anslutna cache-aktiverade distributions platsen måste finnas i samma gränser grupp.

- Aktivera följande klient inställningar i [**leverans optimerings**](../../clients/deploy/about-client-settings.md#delivery-optimization) gruppen:

  - **Använd Configuration Manager gränser grupper för grupp-ID för leverans optimering**
  - **Aktivera enheter som hanteras av Configuration Manager för att använda Microsoft-anslutna cache-servrar för innehålls hämtning**

- Aktivera för hands versions funktionen **klient program för samhanterade enheter**. Mer information finns i [för hands versions funktioner](../../servers/manage/pre-release-features.md).

- Aktivera samhantering och Byt arbets belastning för **klient program** till **pilot Intune** eller **Intune**. Mer information finns i följande artiklar:

  - [Arbets belastningar – klient program](../../../comanage/workloads.md#client-apps)
  - [Aktivera samhantering](../../../comanage/how-to-enable.md)
  - [Växla arbetsbelastningar till Intune](../../../comanage/how-to-switch-workloads.md)

    Om i pilot lägger du till klienten i pilot samlingen för klient program.

#### <a name="intune"></a>Intune

- Den här funktionen stöder endast typen Intune Win32-app.

  - Skapa och tilldela (distribuera) en ny app i Intune för detta ändamål. (Appar som skapats innan Intune version 1811 fungerar inte.) Mer information finns i [Intune Win32 app Management](https://docs.microsoft.com/intune/apps/apps-win32-app-management).

  - Appen måste vara minst 100 MB stor.
  
    > [!TIP]
    > Använd följande grup princip inställning: dator konfiguration > Administrativa mallar > Windows-komponenter > leverans optimering > **minsta innehålls fil storlek för peer-cachelagring (i MB)**.

## <a name="see-also"></a>Se även

[Optimera Windows 10-uppdateringar med leverans optimering](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Felsök Microsoft Connected cache i Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
