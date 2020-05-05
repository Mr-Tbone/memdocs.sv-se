---
title: Installera programuppdateringar
titleSuffix: Configuration Manager
description: Rekommendationer för att använda steget aktivitetssekvens installera program uppdateringar i Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6528e979222bc6ecea2a57a003ff5266b5c096c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719997"
---
# <a name="install-software-updates"></a>Installera programuppdateringar

*Gäller för: Configuration Manager (aktuell gren)*

Steget **installera program uppdateringar** används ofta i Configuration Manager aktivitetssekvenser. När du installerar eller uppdaterar operativ systemet, utlöses program uppdaterings komponenterna för att söka efter och distribuera uppdateringar. Det här steget kan orsaka utmaningar för vissa kunder, t. ex. tids gräns fördröjningar eller uteblivna uppdateringar. Använd informationen i den här artikeln för att minimera vanliga problem med det här steget och för bättre fel sökning när saker går fel.

Mer information om steget finns i [installera program uppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Rekommendationer

Använd följande rekommendationer för att hjälpa den här processen att lyckas:

- [Använd offlineunderhåll](#use-offline-servicing)
- [Enskilt index](#single-index)
- [Minska bild storleken](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Använd offlineunderhåll

Använd Configuration Manager för att regelbundet installera tillämpliga program uppdateringar på dina bildfiler. Den här metoden minskar sedan antalet uppdateringar som du behöver installera under aktivitetssekvensen.

Mer information finns i [tillämpa program uppdateringar på en avbildning](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Enskilt index

Många bildfiler innehåller flera index, till exempel för olika versioner av Windows. Minska avbildnings filen till ett enda index som du behöver. Den här metoden minskar hur lång tid det tog att tillämpa program uppdateringar på avbildningen. Du kan också använda nästa rekommendation för att minska bild storleken.

Från och med version 1902 automatiserar du den här processen när du lägger till en OS-avbildning på platsen. Mer information finns i [lägga till en OS-avbildning](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a>Minska bild storleken

När du använder program uppdateringar på avbildningen optimerar du utdata genom att ta bort alla ersatta uppdateringar. Använd kommando rads verktyget DISM, till exempel:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Från och med version 1902 finns det ett nytt alternativ för att automatisera processen. Mer information finns i [optimerade avbildnings underhåll](../get-started/manage-operating-system-images.md#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Bild tekniks beslut

När du utformar din avbildnings process finns det flera alternativ som kan påverka installationen av program uppdateringar:

- [Avbilda om avbildningen med jämna mellanrum](#bkmk_goldimage)  
- [Använd offlineunderhåll](#bkmk_offline)  
- [Använd endast standard avbildning](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a>Avbilda om avbildningen med jämna mellanrum

Du har en automatiserad process för att avbilda en anpassad OS-avbildning enligt ett regelbundet schema. Den här aktivitetssekvensen installerar de senaste program uppdateringarna. Dessa uppdateringar kan omfatta ackumulerade, icke-kumulativa och andra viktiga uppdateringar som service stack-uppdateringar (SJÄLVBETJÄNINGS). Aktivitetssekvensen för distribution installerar eventuella ytterligare uppdateringar sedan avbildningen.

Mer information om den här processen finns i [skapa en aktivitetssekvens för att avbilda ett operativ system](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Fördelar

- Färre uppdateringar som ska tillämpas vid distributions tiden per klient, vilket sparar tid och bandbredd under distributionen
- Färre uppdateringar att bekymra dig om att orsaka omstarter
- Anpassad bild för organisationen
- Färre variabler vid distributions tiden

#### <a name="disadvantages"></a>Nackdelar

- Tid för att skapa och avbilda avbildning, även om det är mest automatiserat
- Ökad tid för att distribuera avbildningen till distributions platser, som kan visas som avbrott för aktiva distributioner
- Tiden för att testa i för produktions miljöer kan vara längre än operativ systemets korrigerings cykel, vilket kan göra den uppdaterade avbildningen mer irrelevant


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a>Använd offlineunderhåll

Schemalägg Configuration Manager för att tillämpa program uppdateringar på dina avbildningar.

Mer information finns i [tillämpa program uppdateringar på en avbildning](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Fördelar

- Färre uppdateringar som ska tillämpas vid distributions tiden per klient, vilket sparar tid och bandbredd under distributionen
- Färre uppdateringar att bekymra dig om att orsaka omstarter
- Du kan schemalägga underhålls processen på platsen

#### <a name="disadvantages"></a>Nackdelar

- Manuellt val av uppdateringar
- Ökad tid för att distribuera avbildningen till distributions platser
- Stöder endast CBS-baserade uppdateringar. Det går inte att använda Office-uppdateringar

> [!Tip]  
> Du kan automatisera valet av program uppdateringar med hjälp av PowerShell. Använd cmdleten [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) för att hämta en lista över uppdateringar. Använd sedan cmdleten [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) för att skapa ett schema för offline-underhåll. I följande exempel visas en metod för att automatisera den här åtgärden:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a>Använd endast standard avbildning

Använd standard avbildnings filen Windows Install. wim i distributionens aktivitetssekvens.

#### <a name="advantages"></a>Fördelar

- En känd källa, vilket minskar risken för att en avbildning skadas som ett möjligt problem
- Eliminerar ändringar av avbildning som ett möjligt problem

#### <a name="disadvantages"></a>Nackdelar

- Potential för hög volym uppdateringar under distributionen
- Ökad distributions tid för varje enhet
- Kanske inte behöver anpassningar, kräver ytterligare aktivitetssekvenser för att anpassa



## <a name="flowchart"></a>Sammanför

Diagrammet i flödesschemat visar processen när du inkluderar steget installera program uppdateringar i en aktivitetssekvens.

[Visa diagrammet i full storlek](media/ts-step-install-software-updates.svg)

![Flödes schema för aktivitetssekvens i steget installera program uppdateringar](media/ts-step-install-software-updates.svg)  

1. **Processen startar på klienten**: en aktivitetssekvens som körs på en klient omfattar steget installera program uppdateringar.
2. **Kompilera och utvärdera principer**: klienten kompilerar alla program uppdaterings principer till WMI RequestedConfigs-namnrymden. (CIAgent. log)
3. *Är den här instansen första gången den kallas?*  
    1. **Ja**: gå till **fullständig sökning**  
    2. **Nej**: *är steget konfigurerat med alternativet att [utvärdera program uppdateringar från cachelagrade genomsöknings resultat](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)?*
        1. **Ja**: gå till **Genomsök från cachelagrade resultat**
        2. **Nej**: gå till **fullständig sökning**
4. Skannings process: en fullständig genomsökning eller genomsökning från cachelagrade resultat med övervaknings processen parallellt.
    1. **Fullständig genomsökning**: aktivitetssekvensen anropar program uppdaterings agenten via API för uppdaterings sökning och gör en *fullständig* genomsökning. (WUAHandler. log, ScanAgent. log)  
        1. **Sum agent Scan-full**: normal skannings process via Windows Update Agent (WUA) som kommunicerar med program uppdaterings platsen som kör WSUS. Alla tillämpliga uppdateringar läggs till i det lokala uppdaterings arkivet. (WindowsUpdate. log, UpdateStore. log)
    2. **Genomsök från cachelagrade resultat**: aktivitetssekvensen anropar program uppdaterings agenten via API för uppdaterings sökning för att söka igenom cachelagrade metadata. (WUAHandler. log, ScanAgent. log)
        1. **Sum agent-genomsökning – cachelagrat**: Windows Update Agent (WUA) kontrollerar om det redan finns cachelagrade uppdateringar i det lokala uppdaterings lagret. (WindowsUpdate. log, UpdateStore. log)
    3. **Starta genomsökning timer**: aktivitetssekvensen startar en timer och väntar. (Den här processen sker parallellt med antingen den fullständiga genomsökningen eller sökningen från cachelagrat resultat process.)
        1. **Övervakning**: modulen för AKTIVITETSSEKVENSER övervakar summerings agenten för status.
        2. *Vad är svaret från SUM-agenten?*
            - **Pågår**: har timern nått värdet i variabeln för aktivitetssekvensen [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)? (Standard 1 timme)
                - **Ja**: det går inte att utföra åtgärden.
                - **Nej**: gå till **övervakning**
            - **Misslyckades**: det gick inte att utföra åtgärden.
            - **Slutför**: gå till **räkna upp uppdaterings listan**
5. **Räkna upp uppdaterings lista**: sum-agenten räknar upp listan över uppdateringar som returneras av genomsökningen, vilket avgör vilka som är tillgängliga eller obligatoriska.
6. *Finns det några uppdateringar i listan över Sök Resultat?*
    - **Ja**: gå till **Installera uppdateringar**
    - **Nej**: inget att installera, steget slutförs.
7. Distributions process: installations uppdaterings processen sker parallellt med processen för distributions övervakning.
    1. **Installera uppdateringar**: aktivitetssekvensen ANROPAr sum-agenten via API för uppdaterings distribution för att installera alla tillgängliga eller endast obligatoriska uppdateringar. Det här beteendet baseras på konfigurationen av steget, om du väljer **krävs för installation-endast obligatoriska program uppdateringar** eller **tillgängliga för installation-alla program uppdateringar**. Du kan också ange det här beteendet med [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) -variabeln.
        1. **Sum-agent installation**: normal installations process med hjälp av en befintlig cachelagrad lista med uppdateringar med standard hämtning av innehåll. Installera Update via Windows Update Agent (WUA). (UpdatesDeployment. log, UpdatesHandler. log, WuaHandler. log, WindowsUpdate. log)
    2. **Starta timer för distribution och Visa förlopp**: aktivitetssekvensen startar en installations-timer, visar under förlopp vid 10% intervall i användar gränssnittet för användar gränssnittet och väntar.
        1. **Övervakning**: modulen för aktivitetssekvenser AVsöker summerings agenten för status.
        2. *Vad är svaret från SUM-agenten?*
            - **Pågår**: *har installations processen varit inaktiv i 8 timmar?*
                - **Ja**: det går inte att utföra åtgärden.
                - **Nej**: gå till **övervakning**
            - **Misslyckades**: det gick inte att utföra åtgärden.
            - **Slutför**: gå till *steget har kon figurer ATS med alternativet att **utvärdera program uppdateringar från cachelagrade genomsöknings resultat**?*


### <a name="timeouts"></a>Timeouter

Diagrammet innehåller två av de timeout-variabler som gäller för det här steget. Det finns andra standard timers från andra komponenter som kan påverka den här processen.

- Timeout för uppdaterings genomsökning: 1 timme (Smsts. log)  
- Timeout för plats begär ande: 1 timme (filen LocationServices. log, ca. log)  
- Timeout för innehålls hämtning: 1 timme (DTS. log)  
- Tids gräns för inaktiv distributions plats: 1 timme (filen LocationServices. log, ca. log)  
- Total inaktiv tids gräns för installation: 8 timmar (Smsts. log)  



## <a name="troubleshooting"></a>Felsökning

Använd följande resurser och ytterligare information som hjälper dig att felsöka problem med det här steget:

- Se till att du riktar dina program uppdaterings distributioner till samma samling som aktivitetssekvensdistribution.  

- Se till att inkludera program uppdaterings platser i gränser grupper. Mer information finns i den här [Microsoft Support artikeln](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Information om hur du felsöker hanterings processen för program uppdateringar finns i [hantering av programuppdateringar fel sökning](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Minska storleken på program uppdaterings katalogen för att förbättra den övergripande prestandan. Ett exempel:  

    - Ta bort onödiga klassificeringar, produkter och språk. Mer information finns i [Konfigurera klassificeringar och produkter som ska synkroniseras](../../sum/get-started/configure-classifications-and-products.md).  

    - Indexera om plats databasen och återskapa statistiken. Mer information finns i [fakta bladet om Configuration Manager prestanda och skalnings vägledning](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Neka onödiga uppdateringar, till exempel:
        - Ersatt (från och med version 1810, Configuration Manager utför åtgärden åt dig. Mer information finns i [rensnings beteende för WSUS från och med version 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itanium
        - Beta
        - Nästa version
        - ARM
        - Versioner av Windows som du inte distribuerar
