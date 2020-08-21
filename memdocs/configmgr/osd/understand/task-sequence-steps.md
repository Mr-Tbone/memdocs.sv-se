---
title: Aktivitetssekvenssteg
titleSuffix: Configuration Manager
description: Lär dig mer om de steg som du kan lägga till i en Configuration Manager-aktivitetssekvens.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51a636ffc4adad20e6bc1c69b3194db7a0fa72fd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697372"
---
# <a name="task-sequence-steps"></a>Aktivitetssekvenssteg

*Gäller för: Configuration Manager (aktuell gren)*

Följande steg i aktivitetssekvensen kan läggas till i en Configuration Manager-aktivitetssekvens. Mer information finns i [använda redigeraren för aktivitetssekvens](task-sequence-editor.md).  

## <a name="common-settings"></a>Vanliga inställningar

Följande inställningar är gemensamma för alla steg i aktivitetssekvensen:

### <a name="properties-for-all-steps"></a>Egenskaper för alla steg

- **Namn**: redigeraren för aktivitetssekvensen kräver att du anger ett kort namn som beskriver det här steget. När du lägger till ett nytt steg anger aktivitetssekvensen som standard namnet till typen. **Namn** längden får inte överskrida 50 tecken.  

- **Beskrivning**: Alternativt kan du ange mer detaljerad information om det här steget. **Beskrivningens** längd får inte överskrida 256 tecken.  

Resten av den här artikeln beskriver de andra inställningarna på fliken **Egenskaper** för varje steg i aktivitetssekvensen.

### <a name="options-for-all-steps"></a>Alternativ för alla steg

- **Inaktivera det här steget**: aktivitetssekvensen hoppar över det här steget när den körs på en dator. Ikonen för det här steget är nedtonad i redigeraren för aktivitetssekvensen.  

- **Fortsätt vid fel**: om ett fel inträffar när du kör steget fortsätter aktivitetssekvensen. Mer information finns i [planerings överväganden för automatisering av uppgifter](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups).  

- **Lägg till villkor**: aktivitetssekvensen utvärderar dessa villkors uttryck för att avgöra om den kör steget. Ett exempel på hur man använder en aktivitetssekvens-variabel som ett villkor finns i [använda variabler för aktivitetssekvens](using-task-sequence-variables.md#bkmk_access-condition). Mer information om villkor finns i [Redigeraren för aktivitetssekvens-villkor](task-sequence-editor.md#bkmk_conditions).

I avsnitten nedan för de olika stegen i aktivitetssekvensen beskrivs andra möjliga inställningar på fliken **alternativ** .



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Använd data avbildning

Använd det här steget för att kopiera data avbildningen till den angivna partitionen.  

Det här steget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, välja **bilder**och välja **Använd data avbildning**.

### <a name="variables-for-apply-data-image"></a>Variabler för Använd data avbildning

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Cmdletar för Använd data avbildning

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps)
- [New-CMTSStepApplyDataImage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps)
- [Remove-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps)
- [Set-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps)

### <a name="properties-for-apply-data-image"></a>Egenskaper för Använd data avbildning

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="image-package"></a>Avbildningspaket

Välj **Bläddra** för att ange det **avbildnings paket** som används av den här aktivitetssekvensen. Markera det paket du vill installera i dialogrutan **Välj ett paket**. Längst ned i dialog rutan visas den associerade egenskaps informationen för varje befintligt avbildnings paket. Använd listrutan för att välja den **Bild** du vill installera från det valda **Avbildningspaketet**.  

> [!NOTE]  
> Den här aktivitetssekvensen behandlar avbildningen som en datafil. Den här åtgärden gör inga inställningar för att starta avbildningen som ett operativ system.  

#### <a name="destination"></a>Mål

Konfigurera något av följande alternativ:

- **Nästa tillgängliga partition**: Använd nästa sekventiella partition som steget **tillämpa operativ system** eller **Använd data avbildning** i den här aktivitetssekvensen inte redan är riktad till.  

- **Speciell disk och partition**: Välj **disk** numret (startar med 0) och **partitions** numret (börjar med 1).  

- **Angiven logisk enhets beteckning**: Ange den **enhets beteckning** som tilldelas av Windows PE-partitionen. Enhets beteckningen kan skilja sig från enhets beteckningen som tilldelats av det nyligen distribuerade operativ systemet.  

- **Logisk enhets beteckning lagrad i en variabel**: Ange den aktivitetssekvens som innehåller enhets beteckningen som tilldelats partitionen av Windows PE. Den här variabeln anges vanligt vis i avsnittet Avancerat i dialog rutan **partitionsalternativ** för steget **Formatera och partitionera disk** i aktivitetssekvensen.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Ta bort allt innehåll på partitionen innan avbildningen används  

Anger att aktivitetssekvensen tar bort alla filer på mål partitionen innan avbildningen installeras. Genom att inte ta bort innehållet i partitionen kan du använda den här åtgärden för att lägga till ytterligare innehåll till en tidigare mål partition.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Använd driv Rutins paket  

Använd det här steget för att ladda ned alla driv rutiner i driv rutins paketet och installera dem på Windows-operativsystem.

Aktivitetssekvenssteget **Använd drivrutinspaketet** gör alla enhetsdrivrutiner i ett drivrutinspaket tillgängliga så att Windows kan använda dem. Lägg till det här steget mellan stegen för att **använda operativ systemet** och **Installera Windows och ConfigMgr** för att göra driv rutinerna i paketet tillgängliga för Windows. Aktivitetssekvenssteget **Använd drivrutinspaketet** är också användbart då distribution sker med fristående media.  

Placera liknande enhets driv rutiner i ett driv rutins paket och distribuera dem till lämpliga distributions platser. Du kan till exempel publicera alla driv rutiner från en tillverkare i ett driv rutins paket. Distribuera sedan paketet till distributions platser där de associerade datorerna kan komma åt dem.

Steget **Använd driv rutins paket** är användbart för fristående media. Det här steget är också användbart för att installera en speciell uppsättning driv rutiner. Dessa typer av driv rutiner innehåller enheter som Windows-Plug-and-Play inte identifierar, t. ex. nätverks skrivare.  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **driv rutiner**och väljer **Använd driv rutins paket**.

> [!TIP]
> En översikt över driv rutiner i Configuration Manager finns i [använda aktivitetssekvenser för att installera driv rutiner](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Använd för cachelagring av innehåll för att hämta ett tillämpligt driv rutins paket innan en användare installerar aktivitetssekvensen. Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Variabler för Använd driv Rutins paket

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Cmdletar för applicera driv Rutins paket

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps)

### <a name="properties-for-apply-driver-package"></a>Egenskaper för Använd driv Rutins paket

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="driver-package"></a>Drivrutinspaket

Ange det driv rutins paket som innehåller de enhets driv rutiner som behövs. Välj **Bläddra** för att starta dialog rutan **Välj ett paket** . Välj ett befintligt driv rutins paket som ska användas. Längst ned i dialog rutan visas de associerade paket egenskaperna.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Installera driv rutins paket genom att köra DISM med alternativet rekursivt

Välj det här alternativet om du vill lägga till `/recurse` parametern till DISM-kommandoraden när Windows använder driv rutins paketet.

När du aktiverar det här alternativet kan du även ange ytterligare kommando rads parametrar för DISM. Använd [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) -variabeln för att ta med fler alternativ. Mer information finns i [kommando rads alternativ för Windows 10 DISM](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Välj drivrutin för masslagringsenheter inom paketet som måste installeras före installation i Windows-versioner tidigare än Vista

Ange eventuella driv rutiner för Mass lagring som krävs för att installera ett klassiskt operativ system.  

##### <a name="driver"></a>Drivrutinen

Välj den driv rutin för Mass lagrings enhet som ska installeras före installationen av ett klassiskt OS. List rutan fylls i från det angivna paketet.  

##### <a name="model"></a>Modell

Ange den Start kritisk enhet som behövs för distributioner av operativ system för Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Gör en obevakad installation av osignerade drivrutiner på versioner av Windows där detta är tillåtet

Med det här alternativet kan Windows installera driv rutiner utan en digital signatur.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Använd Nätverks inställningar  

Använd det här steget för att ange konfigurations information för nätverks-eller arbets grupp för mål datorn. Aktivitetssekvensen lagrar dessa värden i rätt svarsfil. Installationsprogrammet för Windows använder den här svars filen under åtgärden **Konfigurera Windows och ConfigMgr** .  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **Inställningar**och väljer **tillämpa nätverks inställningar**.

> [!NOTE]
> Om du inkluderar flera instanser av det här steget i en aktivitetssekvens gäller inte villkoren. Inställningarna från den senaste instansen av det här steget i aktivitetssekvensen tillämpas på enheten. Undvik det här problemet genom att inkludera varje steg i en separat grupp med villkor i gruppen.

### <a name="variables-for-apply-network-settings"></a>Variabler för tillämpa nätverks inställningar

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Cmdletar för tillämpa nätverks inställningar

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps)

### <a name="properties-for-apply-network-settings"></a>Egenskaper för tillämpa nätverks inställningar

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="join-a-workgroup"></a>Anslut till en arbetsgrupp

Välj det här alternativet för att ansluta måldatorn till den angivna arbetsgruppen. Ange namnet på arbetsgruppen på raden **Arbetsgrupp**. Det värde som samlas in av aktivitetssekvensen för att **avbilda nätverks inställningar** kan åsidosätta det här värdet.

#### <a name="join-a-domain"></a>Ansluta till en domän

Välj det här alternativet för att ansluta måldatorn till den angivna domänen. Ange eller bläddra till domänen, till exempel `fabricam.com` . Ange eller bläddra till en LDAP-sökväg (Lightweight Directory Access Protocol) för en organisationsenhet. Till exempel: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

> [!NOTE]
> När en Azure Active Directory (Azure AD)-ansluten klient kör en aktivitetssekvens för operativ Systems distribution kommer klienten i det nya operativ systemet inte att ansluta automatiskt till Azure AD. Även om den inte är Azure AD-ansluten, hanteras klienten fortfarande.

#### <a name="account"></a>Konto

Välj **Ange** för att ange ett konto med de behörigheter som krävs för att ansluta datorn till domänen. I dialog rutan **Windows-användarkonto** anger du användar namnet i följande format: `Domain\User` . Mer information finns i [domän anslutning till konto](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Inställningar för nätverkskort

Ange nätverkskonfigurationer för varje nätverkskort på datorn. Välj **nytt** för att öppna dialog rutan **nätverks inställningar** och ange sedan nätverks inställningarna.

- Om du också använder steget **avbilda nätverks inställningar** tillämpar aktivitetssekvensen de tidigare hämtade inställningarna på nätverkskortet.
- Om aktivitetssekvensen inte tidigare har samlat in nätverks inställningarna tillämpas de inställningar som du anger i det här steget.
- Aktivitetssekvensen tillämpar dessa inställningar på nätverkskort i uppräknings ordningen för Windows-enheter.  
- Aktivitetssekvensen tillämpar inte omedelbart de inställningar som du anger i det här steget på datorn.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Använd operativ Systems avbildning  

Använd det här steget för att installera ett operativ system på mål datorn.

När åtgärden **tillämpa operativ system** körs anger den **OSDTargetSystemDrive** -variabeln till enhets beteckningen för den partition som innehåller OS-filerna.  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, välja **avbildningar**och välj **Använd operativ Systems avbildning**.

> [!TIP]
> Från och med Windows 10, version 1709, innehåller Media flera versioner. När du konfigurerar en aktivitetssekvens för att använda ett uppgraderings paket för operativ system eller en operativ system avbildning måste du välja en [version som stöds](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Använd för cachelagring av innehåll för att ladda ned ett tillämpligt uppgraderings paket för operativ system innan en användare installerar aktivitetssekvensen. Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).
>
> Steget **Installera Windows och ConfigMgr** startar installationen av Windows.

### <a name="variables-for-apply-os-image"></a>Variabler för Använd OS-avbildning

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Cmdletar för Använd OS-avbildning

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps)

### <a name="behaviors-for-apply-os-image"></a>Beteenden för Använd OS-avbildning

Det här steget utför olika åtgärder beroende på om det använder en OS-avbildning eller ett uppgraderings paket för operativ system.  

#### <a name="os-image-actions"></a>Åtgärder för operativ Systems avbildning

Steget **Använd operativ Systems avbildning** utför följande åtgärder när du använder en OS-avbildning:  

1. Ta bort allt innehåll på mål volymen, förutom filer i mappen som anges av ** \_ SMSTSUserStatePath** -variabeln.  

2. Extrahera innehållet i den angivna wim-filen till den angivna partitionen.  

3. Förbered svars filen:  

    1. Skapa en ny standard svars fil för Installationsprogrammet för Windows (Sysprep. inf eller unattend.xml) för det distribuerade operativ systemet.  

    2. Sammanfoga alla värden från den svars fil som användaren angav.  

4. Kopiera Windows Start-inläsare till den aktiva partitionen.  

5. Ange boot.ini eller start konfigurations databasen (BCD) för att referera till det nyligen installerade operativ systemet.  

#### <a name="os-upgrade-package-actions"></a>Åtgärder för uppgraderings paket för operativ system

Steget **Använd operativ Systems avbildning** utför följande åtgärder när du använder ett uppgraderings paket för operativ system:  

1. Ta bort allt innehåll på mål volymen, förutom filer i mappen som anges av ** \_ SMSTSUserStatePath** -variabeln.  

2. Förbered svars filen:  

    1. Skapa en ny svarsfil med standardvärden som skapats av Configuration Manager.  

    2. Sammanfoga alla värden från den svars fil som användaren angav.  

### <a name="properties-for-apply-os-image"></a>Egenskaper för Använd OS-avbildning

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Använd operativsystem från en avbildning

Installerar en OS-avbildning som du har hämtat. Välj **Bläddra** för att öppna dialog rutan **Välj ett paket** . Välj sedan det befintliga avbildnings paket som du vill installera. Om flera avbildningar är associerade med det angivna **avbildnings paketet**väljer du i list rutan den associerade avbildningen som ska användas för den här distributionen. Du kan visa grundläggande information om varje befintlig avbildning genom att markera den.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Använd operativsystemsavbildning från en ursprunglig installationskälla

Installerar ett operativ system med ett uppgraderings paket för operativ system, som också är en ursprunglig installations källa. Välj **Bläddra** för att öppna dialog rutan **Välj ett uppgraderings paket för operativ system** . Välj sedan det befintliga uppgraderings paket för operativ system som du vill använda. Du kan visa grundläggande information om varje befintlig avbildnings källa genom att markera den. I resultat fönstret längst ned i dialog rutan visas de associerade egenskaperna för avbildnings källan. Om det finns flera utgåvor som är associerade med det angivna paketet använder du List rutan för att välja den **version** som du vill använda.  

> [!NOTE]  
> **Uppgraderings paket för operativ system** är främst avsedda att användas med uppgraderingar på plats och inte för nya installationer av Windows. När du distribuerar nya installationer av Windows använder du alternativet **Använd operativ system från en avbildning** och **installerar. wim** från installationskällfilerna.
>
> Distribution av nya installationer av Windows via **uppgraderings paket för operativ system** stöds fortfarande, men det är beroende av driv rutiner som är kompatibla med den här metoden. När du installerar Windows från ett uppgraderings paket för operativ system installeras driv rutinerna även när du fortfarande använder Windows PE och helt enkelt matas in i Windows PE. Vissa driv rutiner är inte kompatibla med att installeras i Windows PE.
>
> Om driv rutinerna inte är kompatibla med att installeras i Windows PE kan du skapa en **operativ system avbildning** med **install. wim** från de ursprungliga installationskällfilerna. Distribuera sedan via alternativet **Använd operativ system från en avbildning** i stället.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Använda obevakad svarsfil eller sysprep-svarsfil för en anpassad installation

Använd det här alternativet om du vill ange en svarsfil för Windows-installation (**unattend.xml**, **unattend.txt**eller **Sysprep. inf**) beroende på operativ systemets version och installations metod. Filen du anger kan innehålla flera av alternativen för standardkonfigurationen som stöds av Windows svarsfiler. Du kan till exempel använda den för att ange startsida för Internet Explorer. Ange det paket som innehåller svars filen och den associerade sökvägen till filen i paketet.  

> [!NOTE]  
> Svars filen för Windows-installationen som du anger kan innehålla inbäddade variabler för aktivitetssekvenser i formuläret `%varname%` , där *varname* är namnet på variabeln. Steget **Installera Windows och ConfigMgr** ersätter variabel strängen för variabelns faktiska värde. Du kan inte använda dessa inbäddade variabler för aktivitetssekvenser i ett numeriskt fält i en unattend.xml svarsfil.  

Om du inte anger svars filen för installations programmet för Windows skapas automatiskt en svarsfil i aktivitetssekvensen.  

#### <a name="destination"></a>Mål

Konfigurera något av följande alternativ:  

- **Nästa tillgängliga partition**: Använd nästa sekventiella partition som inte redan är mål för steget **tillämpa operativ system** eller **Använd data avbildning** i den här aktivitetssekvensen.  

- **Speciell disk och partition**: Välj **disk** numret (startar med 0) och **partitions** numret (börjar med 1).  

- **Angiven logisk enhets beteckning**: Ange den **enhets beteckning** som har tilldelats partitionen av Windows PE. Enhets beteckningen kan skilja sig från enhets beteckningen som tilldelats av det nyligen distribuerade operativ systemet.  

- **Logisk enhets beteckning lagrad i en variabel**: Ange den aktivitetssekvens som innehåller enhets beteckningen som tilldelats partitionen av Windows PE. Den här variabeln anges vanligt vis i avsnittet Avancerat i dialog rutan **partitionsalternativ** för steget **Formatera och partitionera disk** i aktivitetssekvensen.  

### <a name="options-for-apply-os-image"></a>Alternativ för Använd OS-avbildning

Förutom standard alternativen konfigurerar du följande ytterligare inställningar på fliken **alternativ** i det här steget i aktivitetssekvensen:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Få åtkomst till innehåll direkt från distributions platsen

Konfigurera aktivitetssekvensen för att få åtkomst till operativ system avbildningen direkt från distributions platsen. Använd till exempel det här alternativet när du distribuerar operativ system till inbäddade enheter med begränsad lagrings kapacitet. När du väljer det här alternativet ska du också konfigurera paketets delnings inställningar på fliken **data åtkomst** i egenskaperna för operativ system avbildningen.  

> [!NOTE]  
> Den här inställningen åsidosätter det distributions alternativ som du konfigurerar på sidan **distributions platser** i **guiden distribuera program vara**. Den här åsidosättningen gäller endast för den OS-avbildning som anges i det här steget, inte för allt innehåll i aktivitetssekvensen.  

> [!IMPORTANT]  
> För bästa säkerhet rekommenderar vi starkt att du inte väljer det här alternativet. Det här alternativet har främst utformats för att användas på enheter med begränsad lagrings kapacitet. Det här alternativet är inte avsett att hjälpa till att öka hastigheten på aktivitetssekvensen. När det här alternativet är markerat verifieras inte paket-hashen för operativ system paketet. Därför går det inte att säkerställa paket integriteten eftersom det är möjligt för användare med administrativa rättigheter att ändra eller manipulera paket innehållet.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Använd Windows-inställningar

Använd det här steget för att konfigurera Windows-inställningar för mål datorn. Aktivitetssekvensen lagrar dessa värden i rätt svarsfil. Installationsprogrammet för Windows använder den här svars filen under steget **Installera Windows och ConfigMgr** .  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **Inställningar**och väljer **Använd Windows-inställningar**.

### <a name="variables-for-apply-windows-settings"></a>Variabler för att använda Windows-inställningar

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Cmdletar för att använda Windows-inställningar

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [New-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Remove-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps)
- [Set-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps)

### <a name="properties-for-apply-windows-settings"></a>Egenskaper för Använd Windows-inställningar

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="user-name"></a>Användarnamn

Ange det registrerade användar namnet som ska kopplas till mål datorn. Värdet som samlas in av aktivitetssekvensen **samla in Windows-inställningar** kan åsidosätta det här värdet.  

#### <a name="organization-name"></a>Organisationsnamn

Ange det registrerade organisations namnet som ska associeras med mål datorn. Värdet som samlas in av aktivitetssekvensen **samla in Windows-inställningar** kan åsidosätta det här värdet.  

#### <a name="product-key"></a>Produktnyckel  

Ange den produkt nyckel som ska användas för Windows-installationen på mål datorn.  

#### <a name="server-licensing"></a>Serverlicensiering

Ange serverlicensieringsläge.

- Välj **per server** eller **per användare** som licensierings läge.  
- Om du väljer **per server**anger du också det maximala antalet anslutningar som tillåts per licens avtal.  
- Om mål datorn inte är en server eller om du inte vill ange licens läget väljer du **Ange inte**.  

#### <a name="maximum-connections"></a>Maximalt antal anslutningar

> [!NOTE]
> Den här inställningen gäller endast äldre versioner av Windows som inte längre stöds.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Generera slumpmässigt lösenord för den lokala administratören och inaktivera kontot för alla plattformar som stöds (rekommenderas)  

Välj det här alternativet för att ange det lokala administratörs lösen ordet till en slumpmässigt genererad sträng. Det här alternativet inaktiverar också det lokala administratörs kontot på plattformar som har stöd för den här funktionen.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Aktivera kontot och ange lösenord för den lokala administratören  

Välj det här alternativet om du vill aktivera det lokala administratörs kontot med det angivna lösen ordet. Ange lösenordet på raden **Lösenord** och bekräfta lösenordet på raden **Bekräfta lösenord**.  

#### <a name="time-zone"></a>Tidszon

Ange vilken tidszon som ska konfigureras på måldatorn. Värdet som samlas in av aktivitetssekvensen **samla in Windows-inställningar** kan åsidosätta det här värdet.  

#### <a name="language-settings"></a>Språkinställningar

<!--5411057, 5138936-->

Från och med version 1910 styr du språk konfigurationen under operativ Systems distributionen. Om du redan använder dessa språk inställningar kan den här ändringen hjälpa dig att förenkla aktivitetssekvensen för OS-distribution. I stället för att använda flera steg per språk eller separata skript, använder du en instans per språk i det här steget med ett villkor för det språket.

Konfigurera följande inställningar:

- Inmatnings språk (standard tangentbordslayout)
- System språk
- GRÄNSSNITTs språk
- GRÄNSSNITTs språks reserv
- Användar språk

Mer information om de här svars fil värdena för Windows-installationen finns i [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Om du skapar en anpassad svarsfil för installations programmet för Windows (unattend.xml) skriver det här steget över alla befintliga värden. Om du vill automatisera en dynamisk process för de här inställningarna använder du de relaterade variablerna för aktivitetssekvens. Till exempel [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Använd driv rutiner automatiskt

Använd det här steget för att matcha och installera driv rutiner som en del av operativ Systems distributionen.  

> [!IMPORTANT]  
> Det går inte att använda steget **Använd driv rutiner automatiskt** för fristående media. Aktivitetssekvensen har ingen anslutning till Configuration Manager-platsen i det här scenariot.  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **driv rutiner**och välj **Använd driv rutiner automatiskt**.

> [!TIP]
> En översikt över driv rutiner i Configuration Manager finns i [använda aktivitetssekvenser för att installera driv rutiner](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Beteenden för automatisk tillämpning av driv rutiner

Aktivitetssekvenssteget **Använd drivrutiner automatiskt** utför följande åtgärder:  

1. Sök igenom maskin varan och hitta plug-and-Play-ID för alla enheter som finns i systemet.  

2. Skicka listan över enheter och deras plug-and-Play-ID till hanterings platsen. Hanterings platsen returnerar en lista över kompatibla driv rutiner från driv rutins katalogen för varje maskin varu enhet. Listan innehåller alla aktiverade driv rutiner oavsett vilket driv rutins paket de finns i, och driv rutiner som taggats med den angivna driv rutins kategorin.  

3. För varje maskin varu enhet väljer aktivitetssekvensen den bästa driv rutinen. Den här driv rutinen är lämplig för det distribuerade operativ systemet och finns på en tillgänglig distributions plats.  

4. Aktivitetssekvensen laddar ned de valda driv rutinerna från en distributions plats och mellanliggande driv rutiner på mål-OS.  

    1. När du använder en OS-avbildning placerar aktivitetssekvensen driv rutinerna i operativ systemets driv rutins arkiv.  

    2. När du använder ett uppgraderings paket för operativ systemet som en ursprunglig installations källa konfigurerar aktivitetssekvensen Installationsprogrammet för Windows med driv rutins platsen.  

5. Under steget **Installera Windows och ConfigMgr** i aktivitetssekvensen hittar installationsprogrammet för Windows de driv rutiner som mellanlagrats i det här steget.  

### <a name="variables-for-auto-apply-drivers"></a>Variabler för automatisk tillämpning av driv rutiner

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Cmdletar för automatisk tillämpning av driv rutiner

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps)

### <a name="properties-for-auto-apply-drivers"></a>Egenskaper för automatisk tillämpning av driv rutiner

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Installera endast de bäst matchade kompatibla drivrutinerna

Anger att aktivitetssekvenssteget endast installerar den bäst matchade drivrutinen för varje maskinvaruenhet som identifieras.  

#### <a name="install-all-compatible-drivers"></a>Installera alla kompatibla drivrutiner

Aktivitetssekvensen installerar alla driv rutiner som är kompatibla för varje identifierad maskin varu enhet. Installationsprogrammet för Windows väljer sedan den bästa driv rutinen. Det här alternativet tar mer nätverks bandbredd och disk utrymme. Aktivitetssekvensen hämtar fler driv rutiner, men Windows kan välja en bättre driv rutin.  

#### <a name="consider-drivers-from-all-categories"></a>Ta hänsyn till drivrutiner från alla kategorier

Aktivitetssekvensen söker igenom alla tillgängliga driv rutins kategorier efter lämpliga enhets driv rutiner.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Begränsa drivrutinsmatchningen till att endast ta hänsyn till drivrutiner i valda kategorier

Aktivitetssekvensen söker i de angivna driv rutins kategorierna efter lämpliga enhets driv rutiner.  

Om du väljer flera kategorier returneras alla matchande driv rutiner som finns i någon av kategorierna. Det motsvarar en `OR` åtgärd.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Gör en obevakad installation av osignerade på Windows-versioner där det är tillåtet

Med det här alternativet kan Windows installera driv rutiner utan en digital signatur.  

> [!IMPORTANT]  
> Det här alternativet gäller inte för operativ system där du inte kan konfigurera princip för signering av driv rutiner.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Avbilda nätverks inställningar

Använd det här steget för att avbilda Microsofts nätverks inställningar från datorn som kör aktivitetssekvensen. Aktivitetssekvensen sparar inställningarna i variabler för aktivitetssekvens. De här inställningarna åsidosätter standardinställningarna som du konfigurerar i steget **tillämpa nätverks inställningar** .  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **Inställningar**och väljer **avbilda nätverks inställningar**.

### <a name="variables-for-capture-network-settings"></a>Variabler för att avbilda nätverks inställningar

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Cmdletar för att avbilda nätverks inställningar

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps)

### <a name="properties-for-capture-network-settings"></a>Egenskaper för avbilda nätverks inställningar

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrera domän och arbetsgruppmedlemskap

Samlar in information om medlemskap i domän och arbetsgrupp på måldatorn.  

#### <a name="migrate-network-adapter-configuration"></a>Migrera nätverkskortskonfiguration

Samlar in konfigurationen för nätverkskort på måldatorn. Den samlar in följande information:

- Globala nätverks inställningar  
- Antal kort  
- Följande nätverks inställningar är associerade med varje kort: DNS, WINS, IP och port filter



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Avbilda operativ Systems avbildning

Det här steget samlar in en eller flera avbildningar från en referens dator. Aktivitetssekvensen skapar en Windows-avbildning (. wim) på den angivna nätverks resursen. Använd sedan guiden **Lägg till avbildnings paket för operativ system** för att importera avbildningen till Configuration Manager för avbildnings OS-distributioner.  

Configuration Manager fångar varje volym (enhet) från referens datorn till en separat avbildning i WIM-filen. Om den refererade datorn har flera volymer innehåller den resulterande. wim-filen en separat avbildning för varje volym. Det här steget fångar bara volymer som är formaterade som NTFS eller FAT32. Den hoppar över volymer med andra format och USB-volymer.  

Det installerade operativ systemet på referens datorn måste vara en version av Windows som Configuration Manager stöder. Använd SysPrep-verktyget för att förbereda operativ systemet på referens datorn. Den installerade OS-volymen och start volymen måste vara samma volym.  

Ange ett konto med Skriv behörighet för den valda nätverks resursen. Mer information om avbildnings kontot för avbildnings operativ system finns i [konton](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, välja **avbildningar**och välja **avbildning av operativ system avbildning**.

### <a name="variables-for-capture-os-image"></a>Variabler för avbildning av avbildning av operativ system

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Cmdlets för avbildning av avbildning av operativ system

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps)
- [New-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Remove-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps)
- [Set-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps)

### <a name="properties-for-capture-os-image"></a>Egenskaper för avbildning av avbildning av operativ system

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="target"></a>Mål  

Fil Systems Sök väg till den plats som Configuration Manager använder för att lagra den insamlade OS-avbildningen.  

#### <a name="description"></a>Beskrivning  

En valfri användardefinierad Beskrivning av den fångade OS-avbildningen som lagras i avbildnings filen.  

#### <a name="version"></a>Version  

Ett valfritt användardefinierat versions nummer som ska tilldelas avbildningen av den insamlade operativ systemet. Det här värdet kan vara valfri kombination av bokstäver och siffror. Den lagras i bild filen.  

#### <a name="created-by"></a>Skapades av  

Det valfria namnet på den användare som skapade operativ system avbildningen. Den lagras i bild filen.  

#### <a name="capture-operating-system-image-account"></a>Avbilda konto för operativsystemsavbildningen  

Ange det Windows-konto som har behörighet till den angivna nätverks resursen. Välj **Ange** för att ange namnet på Windows-kontot.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Avbilda användar tillstånd

I det här steget används User State Migration Tool (USMT) för att avbilda användar tillstånd och inställningar från datorn som kör aktivitetssekvensen. Detta aktivitetssekvenssteg används tillsammans med aktivitetssekvenssteget **Återställ användartillstånd**. I det här steget krypteras ständigt tillstånds lager i USMT med hjälp av en krypterings nyckel som Configuration Manager genererar och hanterar.  

Mer information om hur du hanterar användar tillstånd när du distribuerar operativ system finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

Om du vill spara och återställa inställningar för användar tillstånd från en plats för tillståndsmigrering, använder du det här steget med stegen i **begär tillstånds lager** och **Frisläpp tillstånds lager** .  

Det här steget ger kontroll över en begränsad del av de oftast använda USMT-alternativen. Ange ytterligare kommando rads alternativ med **aktivitetssekvensvariabeln OSDMigrateAdditionalCaptureOptions** -variabeln.  

Det här aktivitetssekvenssteget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **användar tillstånd**och välj **avbilda användar tillstånd**.

### <a name="variables-for-capture-user-state"></a>Variabler för avbildning av användar tillstånd

Använd följande variabler för aktivitetssekvens i det här steget:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Cmdlets för avbildning av användar tillstånd

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps)

### <a name="properties-for-capture-user-state"></a>Egenskaper för avbilda användar tillstånd

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="user-state-migration-tool-package"></a>USMT-paket

Ange det paket som innehåller User State Migration Tool (USMT). Aktivitetssekvensen använder den här versionen av USMT för att avbilda användar tillstånd och inställningar. Det här paketet kräver inte något program. Ange ett paket som innehåller 32-bitars-eller 64-bitars versionen av USMT. Arkitekturen i USMT beror på arkitekturen i operativ systemet som aktivitetssekvensen är infångad från.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Avbilda alla användarprofiler med standardalternativ

Migrera all användar profil information. Det här alternativet är standardinställningen.  

Om du väljer det här alternativet, men inte väljer **Återställ lokala dator användar profiler** i steget **Återställ användar tillstånd** , Miss lyckas aktivitetssekvensen. Configuration Manager kan inte migrera nya konton utan att tilldela dem lösen ord.

När du använder alternativet **Installera ett befintligt avbildnings paket** i guiden **Ny aktivitetssekvens** , kommer den resulterande aktivitetssekvensen att **avbilda alla användar profiler med standard alternativ**. Den här standardsekvensen för aktiviteter väljer inte alternativet att **återställa lokala dator användar profiler**eller icke-domän användar konton.  

Välj **Återställ användar profiler för lokal dator** och ange ett lösen ord för kontot som ska migreras. I en manuellt skapad aktivitetssekvens finns den här inställningen under steget **restore User State** . I en aktivitetssekvens som skapats av guiden **Ny aktivitetssekvens** finns den här inställningen på sidan **Återställ användarens filer och inställningar**.  

Den här inställningen gäller inte om du inte har några lokala användar konton.  

#### <a name="customize-how-user-profiles-are-captured"></a>Anpassa hur användarprofiler avbildas

Välj det här alternativet om du vill ange en anpassad profil fil för migrering. Välj **filer** för att välja KONFIGURATIONSFILER för USMT som ska användas med det här steget. Ange en anpassad XML-fil som innehåller regler som definierar de filer för användar tillstånd som ska migreras.  

#### <a name="click-here-to-select-configuration-files"></a>Klicka här för att välja konfigurationsfiler

Välj det här alternativet för att välja vilka konfigurationsfiler i USMT-paketet som du vill använda för att avbilda användarprofiler. Klicka på knappen **filer** för att starta dialog rutan **konfigurationsfiler** . Om du vill ange en konfigurations fil anger du namnet på filen på raden **fil namn** och klickar på knappen **Lägg till** .  

#### <a name="enable-verbose-logging"></a>Aktivera utförlig loggning

Aktivera det här alternativet för att skapa mer detaljerad information i loggfilen. När du fångar in status genererar aktivitetssekvensen som standard **ScanState. log** i mappen aktivitetssekvens `%WinDir%\ccm\logs` .  

#### <a name="skip-files-using-encrypted-file-system"></a>Hoppa över filer med krypterade filsystem

Aktivera det här alternativet om du vill hoppa över fångst av filer som krypterats med EFS (Encrypted File System). Filerna innehåller filer för användar profiler. Beroende på OS-och USMT-versionerna kanske krypterade filer inte kan läsas efter att du har återställt. Mer information finns i dokumentationen för Windows Server.  

#### <a name="copy-by-using-file-system-access"></a>Kopiera med hjälp av åtkomst tll filsystem

Aktivera det här alternativet om du vill ange någon av följande inställningar:  

- **Fortsätt om vissa filer inte kan**avbildas: Aktivera den här inställningen om du vill fortsätta migreringsprocessen även om det inte går att avbilda några filer. Om du inaktiverar det här alternativet och en fil inte kan fångas, Miss lyckas det här steget. Det här alternativet är aktiverat som standard.  

- **Avbilda lokalt genom att använda länkar i stället för att kopiera filer**: Aktivera den här inställningen om du vill använda hårda NTFS-länkar för att avbilda filer.  

    Mer information om hur du migrerar data med hårda länkar finns i [migreringsarkiv för hårda](/windows/deployment/usmt/usmt-hard-link-migration-store)länkar.  

- **Avbilda i offline-läge (endast Windows PE)**: Aktivera den här inställningen för att avbilda användar tillstånd i Windows PE i stället för det fullständiga operativ systemet.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Avbildning med hjälp av VSS (Volume Copy Shadow Service).

Med det här alternativet kan du avbilda filer även om de är låsta för redigering av ett annat program.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Avbilda Windows-inställningar

Använd det här steget för att avbilda Windows-inställningar från datorn som kör aktivitetssekvensen. Aktivitetssekvensen sparar inställningarna i variabler för aktivitetssekvens. De här inställningarna åsidosätter standardinställningarna som du konfigurerar i steget **Använd Windows-inställningar** .  

Det här steget i aktivitetssekvensen körs antingen i Windows PE eller i det fullständiga operativ systemet.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **Inställningar**och sedan **avbilda Windows-inställningar**.

### <a name="variables-for-capture-windows-settings"></a>Variabler för att avbilda Windows-inställningar

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Cmdlets för att avbilda Windows-inställningar

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps)

### <a name="properties-for-capture-windows-settings"></a>Egenskaper för att avbilda Windows-inställningar

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="migrate-computer-name"></a>Migrera datornamn

Avbilda datorns NetBIOS-datornamn.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrera registrerade användar- och organisationsnamn

Avbilda registrerade användar-och organisations namn från datorn.  

#### <a name="migrate-time-zone"></a>Migrera tidzon

Avbilda tids zons inställningen på datorn.  


## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Kontrol lera beredskap

Använd det här steget för att kontrol lera att mål datorn uppfyller de angivna kraven för distributions krav.  

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **Allmänt**och välj **kontrol lera beredskap**.

Från och med version 2002 innehåller det här steget åtta nya kontroller. Ingen av dessa nya kontroller är markerade som standard i nya eller befintliga instanser av steget.<!--6005561--> För ytterligare information om varje kontroll, se de olika avsnitten nedan.

- **Arkitektur för aktuellt operativ system**
- **Lägsta version av operativsystemet**
- **Högsta version av operativsystemet**
- **Lägsta klient version**
- **Språk för aktuellt operativ system**
- **Nätström är nätansluten**
- **Nätverkskort anslutet**
  - **Nätverkskortet är inte trådlöst**

Från och med version 2006 inkluderar det här steget en kontroll för att avgöra om enheten använder UEFI, **datorn är i UEFI-läge**.<!--6452769-->

> [!IMPORTANT]
> Om du vill dra nytta av den nya Configuration Manager-funktionen kan du, när du har uppdaterat platsen, även uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

**Smsts. log** innehåller resultatet av alla kontroller. Om en kontroll Miss lyckas fortsätter motorn för aktivitetssekvensen att utvärdera de andra kontrollerna. Steget fungerar inte förrän alla kontroller har slutförts. Om minst en kontroll Miss lyckas Miss lyckas steget och den returnerar felkoden **4316**. Den här felkoden översätts till "den resurs som krävs för den här åtgärden finns inte."

### <a name="variables-for-check-readiness"></a>Variabler för att kontrol lera beredskap

Använd följande variabler för aktivitetssekvens i det här steget:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH) (från och med version 2002)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER) (från och med version 2002)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER) (från och med version 2002)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER) (från och med version 2002)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE) (från och med version 2002)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER) (från och med version 2002)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK) (från och med version 2002)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI) (från och med version 2006)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED) (från och med version 2002)

### <a name="cmdlets-for-check-readiness"></a>Cmdletar för att kontrol lera beredskap

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps)

### <a name="properties-for-check-readiness"></a>Egenskaper för kontrol lera beredskap

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="minimum-memory-mb"></a>Minsta minnes storlek (MB)

Kontrol lera att mängden minne, i megabyte (MB), uppfyller eller överskrider den angivna mängden. Steget aktiverar den här inställningen som standard.  

#### <a name="minimum-processor-speed-mhz"></a>Lägsta processorhastighet (MHz)  

Kontrol lera att processorns hastighet, i megahertz (MHz), uppfyller eller överskrider den angivna mängden. Steget aktiverar den här inställningen som standard.  

#### <a name="minimum-free-disk-space-mb"></a>Minsta lediga disk utrymme (MB)

Kontrol lera att mängden ledigt disk utrymme, i megabyte (MB), uppfyller eller överskrider den angivna mängden.  

#### <a name="current-os-to-be-refreshed-is"></a>Aktuellt operativ system som ska uppdateras är

Kontrol lera att det operativ system som är installerat på mål datorn uppfyller det angivna kravet. I steget anges den här inställningen som **klient** som standard.  

#### <a name="architecture-of-current-os"></a>Arkitektur för aktuellt operativ system

Från och med version 2002 kontrollerar du om det aktuella operativ systemet är **32-bitars** eller **64-bitars**.

#### <a name="minimum-os-version"></a>Lägsta version av operativsystemet

Från och med version 2002 kontrollerar du att det aktuella operativ systemet kör en senare version än vad som anges. Ange versionen med huvud version, lägre version och build-nummer. Till exempel `10.0.16299`.

#### <a name="maximum-os-version"></a>Högsta version av operativsystemet

Från och med version 2002 kontrollerar du att det aktuella operativ systemet kör en tidigare version än den angivna. Ange versionen med huvud version, lägre version och build-nummer. Till exempel `10.0.18356`.

#### <a name="minimum-client-version"></a>Lägsta klient version

Från och med version 2002 kontrollerar du att den Configuration Manager klient versionen är minst den angivna versionen. Ange klient versionen i följande format: `5.00.8913.1005` .

#### <a name="language-of-current-os"></a>Språk för aktuellt operativ system

Från och med version 2002 kontrollerar du att det aktuella OS-språket matchar det du anger. Välj språk namnet så jämförs den associerade språk koden. Den här kontrollen jämför det språk som du väljer till egenskapen **OSLanguage** för klassen **Win32_OperatingSystem** WMI-klass på klienten.

#### <a name="ac-power-plugged-in"></a>Nätström är nätansluten

Från och med version 2002 kontrollerar du att enheten är ansluten och inte vid batteri drift.

#### <a name="network-adapter-connected"></a>Nätverkskort anslutet

Från och med version 2002 kontrollerar du att enheten har ett nätverkskort som är anslutet till nätverket. Du kan också markera kryss rutan beroende för att kontrol lera att **nätverkskortet inte är trådlöst**.

#### <a name="computer-is-in-uefi-mode"></a>Datorn är i UEFI-läge

Från och med version 2006 bestämmer du om enheten har kon figurer ATS för UEFI eller BIOS.

### <a name="options-for-check-readiness"></a>Alternativ för att kontrol lera beredskap

> [!NOTE]  
> Om du aktiverar inställningen **Fortsätt vid fel** på fliken **alternativ** i det här steget loggar den bara beredskaps kontroll resultaten. Om kontrollen Miss lyckas stoppas aktivitetssekvensen inte.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Anslut till nätverksmappen

Använd det här steget för att skapa en anslutning till en delad nätverksmapp.  

Detta steg i aktivitetssekvensen körs i hela operativ systemet eller Windows PE.  

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **Allmänt**och välj **Anslut till nätverksmapp**.

### <a name="variables-for-connect-to-network-folder"></a>Variabler för att ansluta till nätverksmappen

Använd följande variabler för aktivitetssekvens i det här steget:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Cmdletar för att ansluta till nätverksmappen

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps)

### <a name="properties-for-connect-to-network-folder"></a>Egenskaper för Anslut till nätverksmapp

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="path"></a>Sökväg  

Välj **Bläddra** för att ange sökvägen till nätverksmappen. Använd formatet `\\server\share`.

#### <a name="drive"></a>Enhet  

Välj den lokala enhets beteckning som ska tilldelas för den här anslutningen.

#### <a name="account"></a>Konto

Välj **Ange** för att ange användar kontot med behörighet att ansluta till nätverksmappen. Mer information om anslutnings kontot för en nätverksmapp finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> Inaktivera BitLocker

Använd det här steget för att inaktivera BitLocker-kryptering på den aktuella operativ system enheten eller på en angiven enhet. Den här åtgärden lämnar nyckel skyddet synliga i klartext på hård disken. Innehållet i enheten krypteras inte. Den här åtgärden slutförs nästan omedelbart.  

> [!NOTE]  
> BitLocker-kryptering ger den lägsta krypteringnivån av innehållet på en volym.  

Om du har flera krypterade enheter måste du inaktivera BitLocker på alla data enheter innan du inaktiverar BitLocker på operativ Systems enheten.  

Det här steget körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **diskar**och sedan **inaktivera BitLocker**.

### <a name="variables-for-disable-bitlocker"></a>Variabler för att inaktivera BitLocker

Från och med version 1906 använder du följande variabler för aktivitetssekvens i det här steget:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Cmdlets för att inaktivera BitLocker

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps)

### <a name="properties-for-disable-bitlocker"></a>Egenskaper för att inaktivera BitLocker

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="current-operating-system-drive"></a>Aktuell operativsystemsenhet

Inaktiverar BitLocker på den aktuella operativ system enheten.  

#### <a name="specific-drive"></a>Specfik enhet  

Inaktiverar BitLocker på en specifik enhet. Använd listrutan om du vill ange enhet där BitLocker är inaktiverat.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Återuppta skyddet när Windows har startats om det angivna antalet gånger

<!-- 4512937 -->
Från och med version 1906 använder du det här alternativet för att ange antalet omstarter för att behålla BitLocker inaktiverat. I stället för att lägga till flera instanser av det här steget anger du ett värde mellan 1 (standard) och 15.

Du kan ställa in och ändra det här beteendet med variablerna [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) och [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Ladda ned paket innehåll

Använd det här steget för att ladda ned någon av följande paket typer:  

- Operativsystemavbildningar  
- Uppgraderings paket för operativ system  
- Drivrutinspaket  
- Paket  
- Start avbildningar, <sup> [Anmärkning 1](#bkmk_note1)</sup>  

Det här steget fungerar bra i en aktivitetssekvens för att uppgradera ett operativ system i följande scenarier:  

- Om du vill använda en aktivitetssekvens för uppgraderingar som fungerar med både x86- och x64-plattformar. Inkludera två **innehålls steg för hämtnings paket** i **förberedelse för uppgraderings** gruppen. Ange villkor på fliken **alternativ** för att identifiera klient arkitekturen och hämta bara lämpligt uppgraderings paket för operativ systemet. Konfigurera varje steg för **hämtning av paket innehåll** för att använda samma variabel. Använd variabeln för medie Sök vägen i steget **Uppgradera operativ system** .  

- Om du vill ladda ned relevanta drivrutinspaket dynamiskt använder du två **Ladda ned paketinnehåll**-steg med villkor som identifierar lämplig maskinvarutyp för varje drivrutinspaket. Konfigurera varje steg för **hämtning av paket innehåll** för att använda samma variabel. Använd variabeln för det **mellanlagrade innehålls** värdet i avsnittet driv rutiner i steget **Uppgradera operativ system** .  

> [!NOTE]  
> När du distribuerar en aktivitetssekvens som innehåller det här steget ska du inte välja **Hämta allt innehåll lokalt innan du startar aktivitetssekvensen** eller **komma åt innehåll direkt från en distributions plats** för **distributions alternativ** på sidan **distributions platser** i guiden distribuera program vara.  

Det här steget körs antingen i det fullständiga operativ systemet eller Windows PE. Alternativet att spara paketet i Configuration Manager-klientcachen stöds inte i Windows PE.

> [!NOTE]  
> **Innehålls aktiviteten Ladda ned paket** stöds inte för användning med fristående media. Mer information finns i [åtgärder som inte stöds för fristående media](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).  

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **program vara**och välja **Ladda ned paket innehåll**.

### <a name="cmdlets-for-download-package-content"></a>Cmdlets för att ladda ned paket innehåll

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps)

### <a name="properties-for-download-package-content"></a>Egenskaper för Ladda ned paket innehåll

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="select-package"></a>Välj paket  

Välj ikonen för att välja det paket som ska laddas ned. När du har valt ett paket väljer du ikonen igen för att välja ett annat paket.  

#### <a name="place-into-the-following-location"></a>Placera på följande plats

Välj att spara paketet på någon av följande platser:  

- **Arbets katalog för aktivitetssekvens**: den här platsen kallas även för aktivitetssekvensen.  

- **Configuration Manager-klientcachen**: Använd det här alternativet för att lagra innehållet i klientens cacheminne. Den här sökvägen är som standard `%WinDir%\ccmcache` .  

- **Anpassad sökväg**: aktivitetssekvensen laddas först ned paketet till arbets katalogen för aktivitetssekvensen. Sedan flyttas innehållet till den här sökvägen som du anger. Motorn för aktivitetssekvenser lägger till sökvägen med paket-ID: t.  

#### <a name="save-path-as-a-variable"></a>Spara sökvägen som en variabel

Spara paketets sökväg i en anpassad aktivitetssekvens-variabel. Använd sedan den här variabeln i ett annat steg i aktivitetssekvensen.

Configuration Manager lägger till ett numeriskt suffix till variabel namnet. Du kan till exempel ange en variabel `%MyContent%` som en anpassad variabel. Det är roten där aktivitetssekvensen lagrar allt innehåll som refereras till i det här steget. Det här innehållet kan innehålla flera paket. Lägg till ett numeriskt suffix när du refererar till variabeln. För det första paketet, se `%MyContent01%` . När du refererar till variabeln i efterföljande steg, till exempel **Uppgradera operativ system**, använder `%MyContent02%` eller `%MyContent03%` , där numret motsvarar den ordning som ska användas för att **Hämta** paketets innehålls steg.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Om det inte går att ladda ned ett paket kan du fortsätta att ladda ned andra paket i listan.

Om aktivitetssekvensen inte kan ladda ned ett paket börjar det att ladda ned nästa paket i listan.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Anmärkning 1: användning av start avbildningar i steget Ladda ned paket innehåll

*Gäller för version 1910 och senare*<!-- SCCMDocs-pr #4202 -->

Om du konfigurerar [Egenskaper för aktivitetssekvens](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) för att **använda en start avbildning**, är det redundant med att lägga till en start avbildning i det här steget. Lägg endast till en start avbildning i det här steget om den inte anges i egenskaperna för aktivitetssekvensen.

#### <a name="example-use-case"></a>Exempel på användningsfall

- En aktivitetssekvens för att ladda ned innehåll i förväg:
  - Ingen associerad start avbildning.
  - Körs bara i hela operativ systemet, förmodligen utan användar interaktion.
  - Använder flera **hämtnings paket innehålls** steg med villkor. Beroende på det specifika språket och arkitekturen laddar den ned innehåll till-klientens cacheminne för att förbereda för aktivitetssekvensen för OS-distribution.
  - Det finns bara en instans av den här aktivitetssekvensen, med alla möjliga innehålls alternativ.

- Aktivitetssekvenser för flera operativ system distributioner:
  - En aktivitetssekvens för normala OS-distribution.
  - Har en start avbildning som refereras till i egenskaperna.
  - Det finns flera instanser av den här aktivitetssekvensen, med olika start avbildningar efter behov av arkitektur och språk

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> Aktivera BitLocker

BitLocker-kryptering ger den lägsta krypteringnivån av innehållet på en volym. Använd det här steget för att aktivera BitLocker-kryptering på minst två partitioner på hård disken. Den första aktiva partitionen innehåller startkoden för Windows. En annan partition innehåller operativ systemet. Startpartitionen måste vara okrypterad.  

Om du vill aktivera BitLocker på en enhet i Windows PE använder du steget [för företablering av BitLocker](#BKMK_PreProvisionBitLocker) .

Det här steget körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **diskar**och sedan **Aktivera BitLocker**.

När du anger **endast TPM**, **TPM och start nyckel på USB**eller **TPM och PIN-kod**måste Trusted Platform Module (TPM) vara i följande tillstånd innan du kan köra steget **Aktivera BitLocker** :  

- Enabled  
- Aktiverad  
- Ägarskap tillåts  

Från och med version 2006 kan du hoppa över det här steget för datorer som inte har TPM eller när TPM inte har Aktiver ATS. En ny inställning gör det lättare att hantera aktivitetssekvenser på enheter som inte har fullständigt stöd för BitLocker.<!--6995601-->

I det här steget slutförs eventuell återstående TPM-initiering. De återstående åtgärderna kräver inte fysisk närvaro eller omstarter. Med steget **Aktivera BitLocker** slutförs transparent följande återstående åtgärder vid TPM-initiering vid behov:

- Skapa bekräftelsenyckelpar  
- Skapa ägarauktoriseringsvärde och deposition till Active Directory, vilket måste har utökats för att stödja det här värdet  
- Bli ägare  
- Skapa lagringsrotnyckel eller återställ den om den redan finns men är inkompatibel  

Om du vill att aktivitetssekvensen ska vänta på att steget **Aktivera BitLocker** ska slutföra enhets krypterings processen väljer du alternativet **vänta** . Om du inte väljer alternativet **vänta** sker enhets krypteringen i bakgrunden. Aktivitetssekvensen fortsätter direkt till nästa steg.  

BitLocker kan användas för att kryptera flera enheter på ett dator system, både operativ system och data enheter. Om du vill kryptera en data enhet måste du först kryptera operativ system enheten och slutföra krypterings processen. Detta krav beror på att operativ system enheten lagrar nyckel skydd för data enheterna. Om du krypterar operativ systemet och data enheterna i samma aktivitetssekvens väljer du alternativet **vänta** i steget **Aktivera BitLocker** för operativ system enheten.  

Om hård disken redan är krypterad, men BitLocker är inaktiverat, aktiverar steget **Aktivera BitLocker** nyckel skydd igen och slutförs snabbt. Omkryptering av hård disken behövs inte i det här fallet.  

### <a name="variables-for-enable-bitlocker"></a>Variabler för att aktivera BitLocker

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>Cmdletar för att aktivera BitLocker

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps)

### <a name="properties-for-enable-bitlocker"></a>Egenskaper för aktivera BitLocker

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="choose-the-drive-to-encrypt"></a>Välj enhet som ska krypteras

Anger vilken enhet som ska krypteras. Om du vill kryptera den aktuella operativ system enheten väljer du **aktuell operativ systemen het**. Konfigurera sedan ett av följande alternativ för nyckel hantering:  

- **Endast TPM**: Välj det här alternativet om du vill använda TPM (Trusted Platform Module).  

- **Startnyckel endast på USB**: Välj det här alternativet om du vill använda en startnyckel som lagras på ett USB-minne. När du väljer det här alternativet låser BitLocker den normala startprocessen tills en USB-enhet som innehåller en startnyckel för BitLocker ansluts till datorn.  

- **TPM och startnyckel på USB**: Välj det här alternativet om du vill använda TPM och en startnyckel som lagras på ett USB-minne. När du väljer det här alternativet låser BitLocker den normala startprocessen tills en USB-enhet som innehåller en startnyckel för BitLocker ansluts till datorn.  

- **TPM och PIN-kod**: Välj det här alternativet om du vill använda TPM och ett personligt ID-nummer (PIN-kod). När du väljer det här alternativet låser BitLocker den normala startprocessen tills användaren anger PIN-koden.  

Om du vill kryptera en speciell data enhet som inte är en OS-enhet väljer du en **speciell enhet**. Välj sedan enheten i listan.  

#### <a name="disk-encryption-mode"></a>Disk krypterings läge

<!--6995601-->
Från och med version 2006 väljer du någon av följande krypteringsalgoritmer:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Som standard fortsätter steget att använda standard krypterings metoden för operativ system versionen. Om steget körs på en version av Windows som inte stöder den angivna algoritmen, går den tillbaka till standard operativ systemet. I detta fall skickar aktivitetssekvensen status meddelande 11911.

#### <a name="use-full-disk-encryption"></a>Använd fullständig disk kryptering

<!--SCCMDocs-pr issue 2671-->
Som standard krypterar det här steget bara använt utrymme på enheten. Detta är standard beteendet rekommenderas eftersom det är snabbare och mer effektivt. Om din organisation kräver kryptering av hela enheten under installationen aktiverar du det här alternativet. Installationsprogrammet för Windows väntar på att hela enheten ska krypteras, vilket tar lång tid, särskilt på stora enheter.

> [!TIP]
> Från och med version 1910 kan du skapa och distribuera hanterings principer för BitLocker, som använder *fullständig disk* kryptering. Aktivera det här alternativet om du vill hantera BitLocker på enheter när aktivitetssekvensen distribuerar operativ systemet. Mer information finns i [Planera för BitLocker-hantering](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Välj var du vill skapa återställnings nyckeln

Om du vill ange att BitLocker ska skapa återställnings lösen ordet och Depositions det i Active Directory väljer du **i Active Directory**. Det här alternativet kräver att du utökar Active Directory för BitLocker Key depositions. BitLocker kan sedan spara den associerade återställnings informationen i Active Directory. Välj **skapa inte återställnings nyckel** för att inte skapa något lösen ord. Vi rekommenderar att du skapar ett lösen ord.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Vänta tills BitLocker slutför enhetskrypteringen på alla enheter innan du fortsätter körningen av aktivitetssekvensen

Välj det här alternativet om du vill att BitLocker-diskkryptering ska slutföras innan nästa steg i aktivitetssekvensen körs. Om du väljer det här alternativet krypterar BitLocker hela disk volymen innan användaren kan logga in på datorn.  

Krypterings processen kan ta timmar att slutföra när en stor hård disk krypteras. Om du inte väljer det här alternativet kan aktivitetssekvensen fortsätta direkt.  

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Hoppa över det här steget för datorer som inte har TPM, eller där TPM inte är aktiverat

<!--6995601-->
Från och med version 2006 väljer du det här alternativet för att hoppa över enhets kryptering på en dator som inte innehåller en eller aktiverat TPM som stöds. Använd till exempel det här alternativet när du distribuerar ett operativ system till en virtuell dator. Som standard är den här inställningen inaktive rad för steget **Aktivera BitLocker** . Om du aktiverar den här inställningen och enheten inte har en fungerande TPM, loggar aktivitetssekvensen ett fel för Smsts. log och skickar status meddelandet 11912. Aktivitetssekvensen fortsätter att passera det här steget.


## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Formatera och partitionera disk

Använd det här steget för att formatera och partitionera en angiven disk på mål datorn.  

> [!IMPORTANT]  
> Alla inställningar som du anger för det här steget gäller för en angiven disk. Om du vill formatera och partitionera en annan disk på mål datorn lägger du till ett extra **format och partitionera disk** steg i aktivitetssekvensen.  

Det här steget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **diskar**och väljer **Formatera och partitionera disk**.

### <a name="variables-for-format-and-partition-disk"></a>Variabler för formatera och partitionera disk

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Cmdletar för format och partitionera disk

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps)

### <a name="properties-for-format-and-partition-disk"></a>Egenskaper för formatera och partitionera disk

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="disk-number"></a>Antal diskar

Det fysiska disk numret för disken som ska formateras. Antalet baseras på Windows diskuppräkningsordning.  

#### <a name="variable-name-to-store-disk-number"></a>Variabel namn som ska lagra disk nummer

<!--6610288-->

Från och med version 2006 använder du en aktivitetssekvens-variabel för att ange den mål disk som ska formateras. Detta variabel alternativ stöder mer komplexa aktivitetssekvenser med dynamiska beteenden. Ett anpassat skript kan till exempel identifiera disken och ange variabeln baserat på maskin varu typen. Sedan kan du använda flera instanser av det här steget för att konfigurera olika typer av maskin vara och partitioner.

Om du väljer den här egenskapen anger du ett namn på en anpassad variabel. Lägg till ett tidigare steg i aktivitetssekvensen för att ange värdet för den här anpassade variabeln till ett heltals värde för den fysiska disken.

Följande modeller steg visar ett exempel:

- **Kör PowerShell-skript**: ett anpassat skript för att samla in mål diskar
  - Uppsättningar `myOSDisk` till `1`
  - Uppsättningar `myDataDisk` till `2`

- **Formatera och partitionera disk** för OS-disk: anger `myOSDisk` variabel
  - Konfigurerar disk 1 som system disk

- **Formatera och partitionera disk** för data disk: anger `myDataDisk` variabel
  - Konfigurerar disk 2 för RAW-lagring

En variant av det här exemplet använder disk nummer och partitionerings planer för olika maskin varu typer.

> [!NOTE]
> Du kan fortfarande använda den befintliga variabeln **OSDDiskIndex**i en aktivitetssekvens. Varje instans av **disk steget format och partition** använder dock samma index värde. Använd den här variabel egenskapen om du vill ange disk numret program mässigt för flera instanser av det här steget.

#### <a name="disk-type"></a>Disktyp

Typ av disk som ska formateras. Det finns två alternativ att välja i listrutan:

- **Standard (MBR)**: Master Boot Record  
- **GPT**: GUID partition table  

> [!NOTE]  
> Om du ändrar disk typen från **Standard (MBR)** till **GPT**och partitionens layout innehåller en utökad partition, tar aktivitetssekvensen bort alla utökade och logiska partitioner från layouten. Redigeraren för aktivitetssekvens kommer att bekräfta åtgärden innan du ändrar disk typen.  

#### <a name="volume"></a>Volym

Detaljerad information om partitionen eller volymen som aktivitetssekvensen skapar, inklusive följande attribut:  

- Namn  
- Återstående diskutrymme  

Om du vill skapa en ny partition väljer du **ny** för att öppna dialog rutan **Egenskaper för partition** . Ange partitionstyp och storlek och om det är en startpartition. Om du vill ändra en befintlig partition väljer du den partition som ska ändras och väljer sedan knappen **Egenskaper** . Mer information om hur du konfigurerar hårddiskpartitioner finns i någon av följande artiklar:  

- [UEFI/GPT-baserade hårddiskpartitioner](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [BIOS/MBR-baserade hårddiskpartitioner](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Om du vill ta bort en partition väljer du partitionen och väljer sedan **ta bort**.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Installera program

Det här steget installerar de angivna programmen eller en uppsättning program som definieras av en dynamisk lista med variabler för aktivitetssekvens. När aktivitetssekvensen kör det här steget startar programinstallationen omedelbart utan att vänta på något avsöknings intervall för principer.  

Programmen måste uppfylla följande kriterier:  

- Programmet måste ha en distributions typ **Windows Installer** eller **skript** installations program. Distributions typer för Windows app-paket (. appx-fil) stöds inte.  

- Det måste köras under det lokala system kontot och inte användar kontot.  

- Den får inte samverka med skrivbordet. Programmet måste köras i bakgrunden eller i ett obevakat läge.  

- Det får inte initiera en egen omstart. Programmet måste begära en omstart med hjälp av standard koden för omstart, 3010. Det här beteendet ser till att det här steget hanterar omstarten korrekt. Om programmet returnerar en avslutnings kod på 3010 startar aktivitetssekvensen om datorn. Efter omstarten fortsätter aktivitetssekvensen automatiskt.  

> [!Note]
> Om programmet [kontrollerar att körbara filer körs](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), kommer aktivitetssekvensen inte att kunna installera den. Om du inte konfigurerar det här steget för att fortsätta med felet Miss lyckas hela aktivitetssekvensen.

När det här steget körs kontrollerar programmet tillämpligheten för krav reglerna och identifierings metoden på dess distributions typer. Baserat på resultatet av den här kontrollen installerar programmet den tillämpliga distributionstypen. Om en distributions typ innehåller beroenden, utvärderas den beroende distributions typen och installeras som en del av det här steget. Program beroenden stöds inte för fristående media.  

> [!NOTE]  
> För att installera ett program som ersätter ett annat program måste innehållsfilerna för det ersatta programmet vara tillgängligt. Annars Miss lyckas det här steget i aktivitetssekvensen. Exempel: Microsoft Visio 2010 är installerat på en klient eller är avbildat. När steget **installera program** installerar microsoft Visio 2013 måste innehållsfilerna för microsoft Visio 2010 (det ersatta programmet) vara tillgängliga på en distributions plats. Om Microsoft Visio inte är installerat på en klient eller avbildning, installerar aktivitetssekvensen Microsoft Visio 2013 utan att söka efter Microsoft Visio 2010-innehållsfilerna.  
>
> Om du drar tillbaka en ersatt app och den nya appen refereras till i en aktivitetssekvens, kan aktivitetssekvensen inte starta.
Det här beteendet är avsiktligt: aktivitetssekvensen kräver alla app-referenser.<!-- SCCMDocs 1711 -->  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **program vara**och sedan **installera program**.

### <a name="variables-for-install-application"></a>Variabler för att installera program

Använd följande variabler för aktivitetssekvens i det här steget:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Om klienten inte kan hämta listan över hanterings platser från plats tjänster använder du **SMSTSMPListRequestTimeoutEnabled** och **SMSTSMPListRequestTimeout** . Dessa variabler anger hur många millisekunder en aktivitetssekvens ska vänta innan den gör ett nytt försök att installera ett program. Mer information finns i [variabler för aktivitetssekvens](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Cmdlets för installation av program

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps)
- [New-CMTSStepInstallApplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps)
- [Remove-CMTSStepInstallApplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps)
- [Set-CMTSStepInstallApplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps)

### <a name="properties-for-install-application"></a>Egenskaper för installera program

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="install-the-following-applications"></a>Installera följande program

Aktivitetssekvensen installerar dessa program i angiven ordning.  

Configuration Manager filtrerar bort alla inaktiverade program eller program med följande inställningar:  

- Endast när en användare är inloggad  
- Kör med användarrättigheter  

Dessa program visas inte i dialog rutan **Välj program att installera** .

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Installera program enligt dynamisk variabellista

Aktivitetssekvensen installerar program med hjälp av det här bas variabel namnet. Bas variabel namnet är en uppsättning variabler för aktivitetssekvenser som definierats för en samling eller en dator. Dessa variabler anger de program som aktivitetssekvensen installerar för samlingen eller datorn. Varje variabelnamn består av dess grundläggande namn plus ett numeriskt suffix som börjar på 01. Varje variabels värde måste innehålla namnet på programmet och inget annat.  

För att aktivitetssekvensen ska installera program med hjälp av en dynamisk variabel lista aktiverar du följande inställning på fliken **Allmänt** i program **egenskaperna**: **Tillåt att det här programmet installeras från aktivitetssekvensen installera program, i stället för att distribuera manuellt**.  

> [!NOTE]  
> Du kan inte installera program med hjälp av en dynamisk variabel lista för distributioner med fristående media.  

Om du till exempel vill installera ett enda program med hjälp av en aktivitetssekvens som kallas AA01, anger du följande variabel:  

|Variabelnamn|Variabelvärde|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Om du vill installera två program, anger du följande variabler:  

|Variabelnamn|Variabelvärde|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Följande villkor påverkar de program som installeras av aktivitetssekvensen:  

- Om värdet för en variabel inte innehåller någon annan information än namnet på programmet. Aktivitetssekvensen installerar inte programmet och aktivitetssekvensen fortsätter.  

- Om aktivitetssekvensen inte hittar någon variabel med det angivna bas namnet och "01"-suffixet, installerar inte aktivitetssekvensen några program.  

> [!Important]  
> Dessa värden är Skift läges känsliga. Till exempel är "installera" inte detsamma som "installera". Om du behöver ändra värdet kan inte redigeraren för aktivitetssekvens identifiera en ändring av ärendet. Gör en annan redigering samtidigt, till exempel genom att ändra beskrivningen av steg.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Fortsätt med andra program i listan om ett program inte kan installeras, 

Den här inställningen anger att steget fortsätter när en enskild programinstallation Miss lyckas. Om du anger den här inställningen fortsätter aktivitetssekvensen oavsett eventuella installations fel. Om du inte anger den här inställningen och installationen Miss lyckas avslutas steget omedelbart.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Rensa program innehåll från cache efter installation

<!--4485675-->
Från och med version 1906 tar du bort appens innehåll från klientens cacheminne när steget har körts. Det här beteendet är fördelaktigt på enheter med små hård diskar eller när du installerar massor av stora appar i följd.


### <a name="options-for-install-application"></a>Alternativ för att installera program

> [!NOTE]  
> När du väljer **Fortsätt vid fel** på fliken **alternativ** i det här steget, fortsätter aktivitetssekvensen när ett program inte kan installeras. När du inte aktiverar det här alternativet Miss lyckas aktivitetssekvensen och installerar inte återstående program.  

Förutom standard alternativen konfigurerar du följande ytterligare inställningar på fliken **alternativ** i det här steget i aktivitetssekvensen:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Gör om det här steget om datorn startar om från början

Om en av program installationerna startar om datorn från en oväntad omstart, gör du om det här steget. Steget aktiverar den här inställningen som standard med två återförsök. Du kan ange mellan en och fem återförsök.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Installera paket

Använd det här steget för att installera ett program varu paket som en del av aktivitetssekvensen. När det här steget körs startar installationen omedelbart utan att vänta på något avsöknings intervall för principer.  

Paketet måste uppfylla följande kriterier:  

- Den måste köras under det lokala system kontot och inte ett användar konto.  

- Den bör inte samverka med Skriv bordet. Programmet måste köras i bakgrunden eller i ett obevakat läge.  

- Det får inte initiera en egen omstart. Program varan måste begära en omstart med hjälp av standard koden för omstart, 3010. Det här beteendet ser till att aktivitetssekvensen korrekt hanterar omstarten. Om program varan returnerar en 3010-slutkod startar aktivitetssekvensen om datorn. Efter omstarten fortsätter aktivitetssekvensen automatiskt.  

Program som använder alternativet **kör ett annat program först** för att installera ett beroende program stöds inte när du distribuerar ett operativ system. Om du aktiverar paket alternativet **kör ett annat program först**och det beroende programmet redan körs på mål datorn, körs det beroende programmet och aktivitetssekvensen fortsätter. Men om det beroende programmet inte redan har körts på mål datorn, Miss lyckas steget i aktivitetssekvensen.  

> [!NOTE]  
> Den centrala administrations platsen har inte de nödvändiga klient konfigurations principer som krävs för att aktivera program distributions agenten under aktivitetssekvensen. När du skapar fristående medier för en aktivitetssekvens på den centrala administrationsplatsen och aktivitetssekvensen innefattar ett **Installera paket**-steg kan följande fel visas i CreateTsMedia.log-filen:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> För fristående media som innefattar steget **installera paket** skapar du fristående media på en primär plats som har program distributions agenten aktive rad. Du kan också lägga till steget **Kör kommando rad** efter steget **Installera Windows och ConfigMgr** och före det första **installera paket** -steget. Steget **Kör kommando rad** kör ett WMIC-kommando för att aktivera program distributions agenten före det första **installera paket** -steget. Använd följande kommando i steget **Kör kommando rad** :  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Mer information om hur du skapar fristående medier finns i [skapa fristående media](../deploy-use/create-stand-alone-media.md).  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **program vara**och sedan **installera paket**.

### <a name="variables-for-install-package"></a>Variabler för installations paket

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Cmdlets för installations paket

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps)
- [New-CMTSStepInstallSoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps)
- [Remove-CMTSStepInstallSoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps)
- [Set-CMTSStepInstallSoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps)

> [!TIP]
> Använd för cachelagring av innehåll för att ladda ned ett tillämpligt uppgraderings paket för operativ system innan en användare installerar aktivitetssekvensen. Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Egenskaper för installations paket

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="install-a-single-software-package"></a>Installera ett enda programpaket

Den här inställningen anger ett Configuration Manager program varu paket. Steget väntar tills installationen är klar.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Installera programvarupaket enligt dynamiska variabellista

Aktivitetssekvensen installerar paket med hjälp av det här bas variabel namnet. Bas variabel namnet är en uppsättning variabler för aktivitetssekvenser som definierats för en samling eller en dator. Dessa variabler anger de paket som aktivitetssekvensen installerar för samlingen eller datorn. Varje variabelnamn består av dess grundläggande namn plus ett numeriskt suffix som börjar på 001. Varje variabels värde måste innehålla ett paket-ID och namnet på programvaran avgränsat med ett kolon.  

För aktivitetssekvensen för att installera program vara med hjälp av en dynamisk variabel lista aktiverar du följande inställning på fliken **Avancerat** i paket **egenskaperna**: Tillåt att **det här programmet installeras från aktivitetssekvensen installera paket utan att distribueras**.  

> [!NOTE]  
> Du kan inte installera program varu paket med en dynamisk variabel lista för distributioner med fristående media.  

Du kan exempelvis ange följande variabel om du vill installera ett enda programpaket med hjälp av en aktivitetsekvensvariabel med namnet AA001:  

|Variabelnamn|Variabelvärde|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Om du vill installera tre programvarupaket, anger du följande variabler:  

|Variabelnamn|Variabelvärde|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

Följande villkor påverkar de paket som installeras av aktivitetssekvensen:  

- Om du inte skapar värdet för en variabel i rätt format, eller om det inte anger ett giltigt paket-ID och-namn, så Miss lyckas installationen av program varan.  

- Om paket-ID: t innehåller gemener, Miss lyckas program varu installationen.  

- Om aktivitetssekvensen inte hittar någon variabel med det angivna bas namnet och "001"-suffixet, installeras inga paket med aktivitetssekvensen. Aktivitetssekvensen fortsätter.  

> [!Important]  
> Dessa värden är Skift läges känsliga. Till exempel är "installera" inte detsamma som "installera". Om du behöver ändra värdet kan inte redigeraren för aktivitetssekvens identifiera en ändring av ärendet. Gör en annan redigering samtidigt, till exempel genom att ändra beskrivningen av steg.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Om installationen av ett programpaket misslyckas, fortsätter installationen av andra paket i listan

Den här inställningen anger att steget fortsätter om en enskild programpaketinstallation misslyckas. Om du anger den här inställningen fortsätter aktivitetssekvensen oavsett eventuella installations fel. Om du inte anger den här inställningen och installationen Miss lyckas avslutas steget omedelbart.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Installera program uppdateringar

Använd det här steget för att installera program uppdateringar på mål datorn. Mål datorn utvärderas inte för tillämpliga program uppdateringar förrän det här steget körs. Vid detta tillfälle utvärderas mål datorn för program uppdateringar som andra Configuration Manager-klienter. För det här steget för att installera program uppdateringar måste du först distribuera uppdateringarna till en samling som mål datorn är medlem i.  

> [!IMPORTANT]  
> Installera den senaste versionen av Windows Update Agent för bästa prestanda.  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **program vara**och välja **installera program uppdateringar**.

### <a name="variables-for-install-software-updates"></a>Variabler för att installera program uppdateringar

Använd följande variabler för aktivitetssekvens i det här steget:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Om klienten inte kan hämta listan över hanterings platser från plats tjänster använder du variablerna **SMSTSMPListRequestTimeoutEnabled** och **SMSTSMPListRequestTimeout** . Dessa variabler anger hur många millisekunder en aktivitetssekvens ska vänta innan den gör ett nytt försök att installera ett program eller en program uppdatering. Mer information finns i [variabler för aktivitetssekvens](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Cmdletar för att installera program uppdateringar

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps)
- [New-CMTSStepInstallUpdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps)
- [Remove-CMTSStepInstallUpdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps)
- [Set-CMTSStepInstallUpdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps)

Mer information om rekommendationer och ett diagram diagram med tekniskt flöde för det här steget finns i [installera program uppdateringar](install-software-updates.md).

### <a name="properties-for-install-software-updates"></a>Egenskaper för att installera program uppdateringar

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Krävs för installationen - Endast obligatoriska programuppdateringar

Välj det här alternativet om du vill installera alla obligatoriska program uppdateringar med tids gränser för administratörs installation.  

#### <a name="available-for-installation---all-software-updates"></a>Tillgängligt vid installation - Alla programuppdateringar

Välj det här alternativet för att installera alla tillgängliga program uppdateringar. Distribuera först dessa uppdateringar till en samling som datorn är medlem i. Aktivitetssekvensen installerar alla tillgängliga program uppdateringar på mål datorerna.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Utvärdera programuppdateringar från cachelagrade sökresultat

Som standard använder det här steget cachelagrade genomsöknings resultat från Windows Update agenten. Inaktivera det här alternativet om du vill instruera Windows Update Agent att ladda ned den senaste katalogen från program uppdaterings platsen. Aktivera det här alternativet när du använder en aktivitetssekvens för att [avbilda och skapa en operativ system avbildning](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Ett stort antal program uppdateringar är förmodligen i det här scenariot.

Många av de här uppdateringarna har beroenden. Installera till exempel uppdatering ABC innan uppdatering XYZ visas. När du inaktiverar den här inställningen och distribuerar aktivitetssekvensen till många klienter ansluter alla till program uppdaterings platsen på samma gång. Detta leder till prestanda problem under processen och nedladdningen av uppdaterings katalogen.

I de flesta fall använder du standardinställningen för att använda cachelagrade genomsöknings resultat.

Variabeln **SMSTSSoftwareUpdateScanTimeout** styr tids gränsen för genomsökning av program uppdateringar under det här steget. Standardvärdet är 60 minuter. Mer information finns i [variabler för aktivitetssekvens](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Alternativ för att installera program uppdateringar

Förutom standard alternativen konfigurerar du följande ytterligare inställningar på fliken **alternativ** i det här steget i aktivitetssekvensen:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Gör om det här steget om datorn startar om från början

Om en av uppdateringarna startar om datorn, gör om det här steget. Steget aktiverar den här inställningen som standard med två återförsök. Du kan ange mellan en och fem återförsök.  

> [!NOTE]  
> Konfigurera variabeln **SMSTSWaitForSecondReboot** för att ange hur många sekunder som aktivitetssekvensen pausas efter att datorn har startats om i det här scenariot. Mer information finns i [variabler för aktivitetssekvens](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Anslut till domän eller arbets grupp

Använd det här steget för att lägga till mål datorn i en arbets grupp eller domän.  

> [!NOTE]
> När en Azure Active Directory (Azure AD)-ansluten klient kör en aktivitetssekvens för operativ Systems distribution kommer klienten i det nya operativ systemet inte att ansluta automatiskt till Azure AD. Även om den inte är Azure AD-ansluten, hanteras klienten fortfarande.

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **Allmänt**och välj **Anslut domän eller arbets grupp**.

### <a name="variables-for-join-domain-or-workgroup"></a>Variabler för Anslut till domän eller arbets grupp

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Cmdletar för Anslut till domän eller arbets grupp

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps)

### <a name="properties-for-join-domain-or-workgroup"></a>Egenskaper för Anslut till domän eller arbets grupp

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="join-a-workgroup"></a>Anslut till en arbetsgrupp

Välj det här alternativet för att ansluta måldatorn till den angivna arbetsgruppen. Om datorn för närvarande är medlem i en domän väljer du det här alternativet för att starta om datorn.  

#### <a name="join-a-domain"></a>Ansluta till en domän

Välj det här alternativet för att ansluta måldatorn till den angivna domänen.  

Du kan också ange eller bläddra efter en organisationsenhet i den angivna domänen att ansluta datorn till. Om datorn för närvarande är medlem i en annan domän eller en arbets grupp innebär det här alternativet att datorn startas om. Om datorn redan är medlem i en annan ORGANISATIONSENHET, eftersom Active Directory Domain Services inte tillåter ändring av ORGANISATIONSENHETen via den här metoden, ignorerar Installationsprogrammet för Windows den här inställningen.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Ange det konto som har behörighet att ansluta till domänen

Välj **Ange** för att ange användar namn och lösen ord för ett konto som har behörighet att ansluta till domänen. Ange kontot i formatet:  `Domain\account` . Mer information om konto för aktivitetssekvens domän anslutning finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> Förbered ConfigMgr-klient för avbildning

Använd det här steget för att ta bort eller konfigurera den Configuration Manager klienten på referens datorn. Den här åtgärden förbereder datorn för avbildning som en del av avbildnings processen.

Det här steget tar bort Configuration Manager-klienten helt och hållet, i stället för att bara ta bort viktig information. När aktivitetssekvensen distribuerar den insamlade OS-avbildningen installeras en ny Configuration Manager-klient varje gång.  

> [!Note]  
> Motorn för aktivitetssekvenser tar bara bort klienten när en aktivitetssekvens för att **bygga och avbilda en referens operativ Systems avbildning** . Motorn för aktivitetssekvenser tar inte bort klienten under andra avbildnings metoder, till exempel avbildnings medier eller en anpassad aktivitetssekvens.  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, välja **avbildningar**och välja **Förbered ConfigMgr-klient för avbildning**.

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Cmdletar för att förbereda ConfigMgr-klienten för avbildning

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Förbered Windows för avbildning

Använd det här steget för att ange Sysprep-alternativ när du fångar en OS-avbildning på referens datorn. Det här steget Kör Sysprep och startar sedan om datorn i Windows PE-startavbildningen som anges för aktivitetssekvensen. Den här åtgärden Miss lyckas om referens datorn är ansluten till en domän.  

Det här steget körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, välja **bilder**och välja **Förbered Windows för avbildning**.

### <a name="variables-for-prepare-windows-for-capture"></a>Variabler för att förbereda Windows för avbildning

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Cmdletar för att förbereda Windows för avbildning

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps)

### <a name="properties-for-prepare-windows-for-capture"></a>Egenskaper för att förbereda Windows för avbildning

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Automatiskt skapa drivrutinslista för lagringsenheter 

Välj det här alternativet om du vill att Sysprep automatiskt ska skapa en lista över drivrutiner för lagringsenheter från referensdatorn. Det här alternativet aktiverar alternativet Skapa drivrutinslista för lagringsenheter i sysprep.inf-filen på referensdatorn. Mer information om den här inställningen finns i Sysprep-dokumentationen.  

#### <a name="do-not-reset-activation-flag"></a>Återställ inte aktiveringsflaggan

Välj det här alternativet för att förhindra att Sysprep återställer produktaktiveringsflaggan.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Stäng datorn när den här åtgärden har körts

<!--SCCMDocs-pr issue 2695-->
Det här alternativet instruerar Sysprep att stänga av datorn i stället för dess standard beteende för omstart.

Aktivitetssekvensen [Windows autopilot för befintliga enheter](../../../autopilot/existing-devices.md) använder det här steget med det här alternativet.

- Lämna det här alternativet om du vill att aktivitetssekvensen ska uppdatera enheten och sedan omedelbart starta OOBE för autopilot.  

- Aktivera det här alternativet om du vill stänga av enheten efter avbildningen. Sedan kan du leverera enheten till en användare, som startar OOBE med autopilot när de aktiverar den för första gången.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> Företablera BitLocker

Använd det här steget för att aktivera BitLocker på en enhet i Windows PE. Som standard krypteras bara det disk utrymme som används, så krypterings tiderna är mycket snabbare. Du tillämpar alternativ för nyckel hantering genom att använda steget [Aktivera BitLocker](#BKMK_EnableBitLocker) efter att operativ systemet har installerats.

> [!IMPORTANT]
> För etablering av BitLocker krävs att datorn har stöd för och aktiverade Trusted Platform Module (TPM).

Det här steget körs bara i Windows PE. Den körs inte i det fullständiga operativ systemet.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **diskar**och sedan **Företablera BitLocker**.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Cmdlets för företablering av BitLocker

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps)

### <a name="properties-for-pre-provision-bitlocker"></a>Egenskaper för Företablera BitLocker

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Använd BitLocker på den angivna enheten

Ange den enhet du vill aktivera BitLocker för. BitLocker krypterar bara det använda utrymmet på enheten.  

#### <a name="disk-encryption-mode"></a>Disk krypterings läge

<!--6995601-->
Från och med version 2006 väljer du någon av följande krypteringsalgoritmer:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Som standard fortsätter steget att använda standard krypterings metoden för operativ system versionen. Om steget körs på en version av Windows som inte stöder den angivna algoritmen, går den tillbaka till standard operativ systemet. I detta fall skickar aktivitetssekvensen status meddelande 11911.

#### <a name="use-full-disk-encryption"></a>Använd fullständig disk kryptering

<!--SCCMDocs-pr issue 2671-->
Som standard krypterar det här steget bara använt utrymme på enheten. Detta är standard beteendet rekommenderas eftersom det är snabbare och mer effektivt. Om din organisation kräver kryptering av hela enheten under installationen aktiverar du det här alternativet. Installationsprogrammet för Windows väntar på att hela enheten ska krypteras, vilket tar lång tid, särskilt på stora enheter.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Hoppa över det här steget för datorer som inte har TPM, eller där TPM inte är aktiverat

Välj det här alternativet om du vill hoppa över enhets kryptering på en dator som inte innehåller en eller aktiverat TPM som stöds. Använd till exempel det här alternativet när du distribuerar ett operativ system till en virtuell dator. Som standard är den här inställningen aktive rad för steget för **Företablera BitLocker** . Steget kan inte utföras på en enhet utan TPM eller TPM som inte initieras. Från och med version 2006, om enheten inte har en fungerande TPM, loggar aktivitetssekvensen en varning till Smsts. log och skickar status meddelandet 11912.



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Frisläpp tillstånds lager

Använd det här steget för att meddela platsen för tillståndsmigrering att avbildningen eller återställnings åtgärden har slutförts. Använd det här steget tillsammans med **begär tillstånds lager**, **avbilda användar tillstånd**och **återställa användar tillstånds** steg. Du kan använda de här stegen för att migrera användar tillstånds data med en plats för tillståndsmigrering och User State Migration Tool (USMT).  

Mer information om hur du hanterar användar tillstånd när du distribuerar operativ system finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

Om du använder steget **begär tillstånds lager** för att begära åtkomst till en plats för tillståndsmigrering för att *avbilda* användar tillstånd, meddelar det här steget platsen för tillståndsmigrering att insamlings processen har slutförts. Platsen för tillståndsmigrering anger sedan de användar tillstånds data som är tillgängliga för återställning. Platsen för tillståndsmigrering anger åtkomst kontroll behörigheter för användar tillstånds data så att endast återställnings datorn har skrivskyddad åtkomst.  

Om du använder steget **begär tillstånds lager** för att begära åtkomst till en plats för tillståndsmigrering för att *återställa* användar tillstånd, meddelar det här steget platsen för tillståndsmigrering att återställnings processen är klar. Platsen för tillståndsmigrering aktiverar sedan dess konfigurerade inställningar för datakvarhållning.  

> [!IMPORTANT]  
> Ange alternativet **Fortsätt vid fel** för alla steg mellan de steg som krävs för **tillstånds lagret för begäran** och **publicerings tillstånd** . Varje **begäran om tillstånds lager** måste ha ett matchande **publicerings tillstånds lager** steg.  

Det här steget körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **användar tillstånd**och välj **Frisläpp tillstånds lager**.

### <a name="variables-for-release-state-store"></a>Variabler för publicerings tillstånds lager

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Cmdletar för publicerings tillstånds lager

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps)

### <a name="properties-for-release-state-store"></a>Egenskaper för publicerings tillstånds lager

Det här steget kräver inte några inställningar på fliken **Egenskaper** .



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Begär tillstånds lager

Använd det här steget för att begära åtkomst till en plats för tillståndsmigrering när status fångas eller återställs.  

Mer information om hur du hanterar användar tillstånd när du distribuerar operativ system finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

Använd det här steget tillsammans med **publicerings tillstånds lagret**, **avbilda användar tillstånd**och **återställa användar tillstånds** steg. Du kan använda de här stegen för att migrera dator tillstånd med hjälp av en plats för tillståndsmigrering och User State Migration Tool (USMT).  

> [!NOTE]  
> När du skapar en ny plats för tillståndsmigrering, är lagring av användar tillstånd inte tillgängligt i upp till en timme. Du kan påskynda tillgänglighet genom att justera alla egenskaps inställningar på platsen för tillståndsmigrering för att utlösa en plats kontroll fil uppdatering.  

Det här steget körs i det fullständiga operativ systemet och i Windows PE för offline USMT.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **användar tillstånd**och sedan **begär tillstånds lager**.

### <a name="variables-for-request-state-store"></a>Variabler för lagring av begär tillstånd

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Cmdletar för begär tillstånds lager

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps)

### <a name="properties-for-request-state-store"></a>Egenskaper för lagring av begär tillstånd

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="capture-state-from-the-computer"></a>Avbilda tillstånd från datorn.

Hitta en plats för tillståndsmigrering som uppfyller de minimi krav som kon figurer ATS i inställningarna för plats för tillståndsmigrering. Till exempel **maximalt antal klienter** och **minsta mängd ledigt disk utrymme**. Det här alternativet garanterar inte att tillräckligt med utrymme är tillgängligt vid tidpunkten för tillståndsmigrering. Det här alternativet begär åtkomst till platsen för tillståndsmigrering för att samla in användar tillstånd och inställningar från en dator.  

Om Configuration Manager-platsen har flera aktiva tillstånds flyttnings punkter hittar det här steget en plats för tillståndsmigrering med tillgängligt disk utrymme. Aktivitetssekvensen frågar hanterings platsen efter en lista över tillståndsmigrering och utvärderar sedan varje gång den hittar en som uppfyller minimi kraven.  

#### <a name="restore-state-from-another-computer"></a>Återställ tillstånd från en annan dator

Begär åtkomst till en plats för tillståndsmigrering för att återställa tidigare insamlade användar tillstånd och inställningar till en måldator.  

Om det finns flera platser för tillståndsmigrering hittar det här steget platsen för tillståndsmigrering som har statusen för mål datorn.  

#### <a name="number-of-retries"></a>Antal återförsök

Det antal gånger som det här steget försöker hitta en lämplig plats för tillståndsmigrering innan den avbryts.  

#### <a name="retry-delay-in-seconds"></a>Fördröjning av försök (i sekunder)

Tid i sekunder som aktivitetssekvenssteget ska vänta innan ett nytt försök görs.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Om dator kontot inte kan ansluta till ett tillstånds lager, använder du nätverks åtkomst kontot

Om aktivitetssekvensen inte kan komma åt platsen för tillståndsmigrering med hjälp av dator kontot, använder den nätverks åtkomst kontots autentiseringsuppgifter för att ansluta. Det här alternativet är mindre säkert eftersom andra datorer kan använda nätverks åtkomst kontot för att komma åt det lagrade läget. Det här alternativet kan vara nödvändigt om mål datorn inte är domänansluten.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Starta om datorn

Använd det här steget för att starta om datorn som kör aktivitetssekvensen. Efter omstarten fortsätter datorn automatiskt med nästa steg i aktivitetssekvensen.  

Det här steget kan köras antingen i hela operativ systemet eller Windows PE.

Lägg till det här steget i redigeraren för aktivitetssekvens genom att välja **Lägg till**, Välj **Allmänt**och **sedan starta om datorn**.

### <a name="variables-for-restart-computer"></a>Variabler för omstart av dator

Använd följande variabler för aktivitetssekvens i det här steget:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Cmdletar för omstart av dator

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps)

### <a name="properties-for-restart-computer"></a>Egenskaper för omstart av dator

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>Startavbildningen som tilldelas till den här aktivitetssekvensen

Välj det här alternativet om du vill att mål datorn ska använda den Start avbildning som är tilldelad i aktivitetssekvensen. Aktivitetssekvensen använder start avbildningen för att köra efterföljande steg i Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>Installerat standardoperativsystem

Välj det här alternativet om du vill att mål datorn ska starta om i det installerade operativ systemet.  

#### <a name="notify-the-user-before-restarting"></a>Meddela användaren innan du startar om

Välj det här alternativet om du vill visa ett meddelande för användaren innan mål datorn startas om. Steget väljer det här alternativet som standard.  

#### <a name="notification-message"></a>Aviseringsmeddelande

Ange ett meddelande som ska visas för användaren innan mål datorn startas om.  

#### <a name="message-display-time-out"></a>Tidsgräns för meddelande

Ange hur lång tid i sekunder innan mål datorn startar om. Standardvärdet är 60 sekunder.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Återställ användar tillstånd

Använd det här steget för att starta User State Migration Tool (USMT) för att återställa användar tillstånd och inställningar till mål datorn. Du använder det här steget tillsammans med steget **avbilda användar tillstånd** .  

Mer information om hur du hanterar användar tillstånd när du distribuerar operativ system finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

Använd det här steget med lagrings stegen **begär tillstånds lager** och **publicerings tillstånd** för att spara eller återställa tillstånds inställningarna med en plats för tillståndsmigrering. Med det här alternativet dekrypteras ständigt tillstånds arkivet i USMT med hjälp av en krypterings nyckel som Configuration Manager genererar och hanterar.  

Steget **Återställ användar tillstånd** ger kontroll över en begränsad del av de oftast använda USMT-alternativen. Ange ytterligare kommando rads alternativ med **aktivitetssekvensvariabeln OSDMigrateAdditionalRestoreOptions** -variabeln.  

> [!IMPORTANT]  
> Om du använder det här steget för ett syfte som inte är relaterat till ett operativ system distributions scenario lägger du till steget [starta om datorn](#BKMK_RestartComputer) direkt efter steget **Återställ användar tillstånd** .  

Det här steget körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **användar tillstånd**och välj **Återställ användar tillstånd**.

### <a name="variables-for-restore-user-state"></a>Variabler för återställning av användar tillstånd

Använd följande variabler för aktivitetssekvens i det här steget:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Cmdletar för återställning av användar tillstånd

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps)

### <a name="properties-for-restore-user-state"></a>Egenskaper för återställning av användar tillstånd

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="user-state-migration-tool-package"></a>USMT-paket

Ange det paket som innehåller den version av USMT som ska användas för det här steget. Det här paketet kräver inte något program. När steget körs använder aktivitetssekvensen den version av USMT i det angivna paketet. Ange ett paket som innehåller 32-bitars-eller 64-bitars versionen av USMT. Arkitekturen i USMT beror på arkitekturen hos det operativ system som aktivitetssekvensen återställer tillstånd till.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Återställ alla avbildade användarprofiler med standardalternativ

Återställer avbildade användarprofiler med standardalternativ. Om du vill anpassa de alternativ som USMT återställer väljer du **anpassa avbildning av användar profil**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Anpassa hur användarprofiler återställs

Gör att du kan anpassa de filer du vill återställa till måldatorn. Välj **filer** för att ange KONFIGURATIONSFILERNA i USMT-paketet som du vill använda för att återställa användar profilerna. Om du vill lägga till en konfigurations fil anger du namnet på filen i rutan **fil namn** och väljer sedan **Lägg till**. I fönstret filer visas de konfigurationsfiler som används i USMT. XML-filen du anger definierar vilken användar fil i USMT som återställs.  

#### <a name="restore-local-computer-user-profiles"></a>Återställa användarprofiler på den lokala datorn

Återställer användar profilerna på den lokala datorn. De här profilerna är inte för domän användare. Tilldela nya lösen ord till de återställda lokala användar kontona. USMT kan inte migrera de ursprungliga lösen orden. Ange det nya lösenordet i rutan **Lösenord** och bekräfta lösenordet i rutan **Bekräfta lösenord**.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Fortsätt om vissa filer inte kan avbildas

Fortsätter att återställa användar tillstånd och inställningar även om USMT inte kan återställa vissa filer. Steget aktiverar det här alternativet som standard. Om du inaktiverar det här alternativet och USMT påträffar fel vid återställning av filer, Miss lyckas det här steget omedelbart. USMT återställer inte alla filer.

#### <a name="enable-verbose-logging"></a>Aktivera utförlig loggning

Aktivera det här alternativet för att skapa mer detaljerad information i loggfilen. Vid återställning av status genererar aktivitetssekvensen som standard **LoadState. log** i mappen aktivitetssekvens `%WinDir%\ccm\logs` .  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Kör kommando rad

Använd det här steget för att köra den angivna kommando raden.  

Kommandot som körs måste uppfylla följande kriterier:  

- Den bör inte samverka med Skriv bordet. Kommandot måste köras tyst eller i obevakat läge.  

- Det får inte initiera en egen omstart. Kommandot måste begära en omstart med hjälp av standard koden för omstart, 3010. Det här beteendet ser till att aktivitetssekvensen korrekt hanterar omstarten. Om kommandot returnerar en avslutnings kod på 3010, startar aktivitetssekvensen om datorn. Efter omstarten fortsätter aktivitetssekvensen automatiskt.

Det här steget kan köras i fullständigt operativ system eller Windows PE.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **Allmänt**och välj **Kör kommando rad**.

### <a name="variables-for-run-command-line"></a>Variabler för körning av kommando rad

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (från och med version 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (från och med version 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Cmdletar för körning av kommando rad

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps)

### <a name="properties-for-run-command-line"></a>Egenskaper för körning av kommando rad

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="command-line"></a>Kommandorad

Anger den kommando rad som aktivitetssekvensen körs på. Det här fältet är obligatoriskt. Inkludera fil namns tillägg, till exempel. vbs och. exe. Ta med alla nödvändiga installationsfiler och kommando rads alternativ.  

Om du inte anger fil namns tillägget Configuration Manager försöker. com,. exe och. bat. Om fil namnet har ett tillägg som inte är av körbar typ försöker Configuration Manager använda en lokal Association. Om kommando raden till exempel är readme.gif, Configuration Manager startar det program som anges på mål datorn för att öppna. gif-filer.  

Exempel:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> För att köra utan problem, föregå kommando rads åtgärder med kommandot **cmd.exe/c** . Exempel på dessa åtgärder är kommandon för omdirigering av utdata, rör och kopiering.  

#### <a name="output-to-task-sequence-variable"></a>Utdata till aktivitetssekvens-variabel

<!--user story 4977616/bug 4798352-->

Från och med version 1910 sparar du kommandots utdata till en anpassad aktivitetssekvens-variabel.

> [!Note]  
> Configuration Manager begränsar de här utdata till de sista 1000 tecknen.

#### <a name="disable-64-bit-file-system-redirection"></a>Inaktivera omdirigering av filsystem i 64-bitars system

Som standard använder 64-bitars operativ system omdirigeringen av WOW64-filsystem för att köra kommando rader. Detta är att du hittar 32-bitars versioner av operativ systemets körbara filer och bibliotek på rätt sätt. Välj det här alternativet om du vill inaktivera användningen av WOW64-fil systemets omdirigerare. Windows kör kommandot med inbyggda 64-bitars versioner av operativ systemets körbara filer och bibliotek. Det här alternativet har ingen påverkan när du kör på ett 32-bitars operativ system.  

#### <a name="start-in"></a>Starta i

Anger mappen för programmets körbara filer, upp till 127 tecken. Den här mappen kan vara en absolut sökväg på måldatorn eller en sökväg i förhållande till den distributionsplatsmapp som innehåller paketet. Det här fältet är valfritt.  

Exempel:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Knappen **Bläddra** bläddrar i den lokala datorn efter filer och mappar. Allt du väljer måste också finnas på mål datorn. Det måste finnas på samma plats och med samma fil-och mappnamn.  

#### <a name="package"></a>Paket

När du anger filer eller program på kommando raden som inte redan finns på mål datorn väljer du det här alternativet för att ange det Configuration Manager paket som innehåller de filer som krävs. Paketet kräver inget program. Om de angivna filerna finns på mål datorn, krävs inte det här alternativet.  

#### <a name="time-out"></a>Timeout

Anger ett värde som representerar hur länge Configuration Manager tillåter att kommando raden körs. Värdet kan vara mellan en minut och 999 minuter. Standardvärdet är 15 minuter. Det här alternativet är inaktiverat som standard.  

> [!IMPORTANT]  
> Det här steget Miss lyckas om du anger ett värde som inte tillåter tillräckligt med tid för att det angivna kommandot ska slutföras. Det gick inte att utföra hela aktivitetssekvensen beroende på steg-eller grupp villkor. Om timeout går ut Configuration Manager avslutar kommando rads processen.  

#### <a name="run-this-step-as-the-following-account"></a>Kör det här steget som följande konto

Anger att kommando raden körs som ett annat Windows-användarkonto än det lokala system kontot.  

> [!NOTE]  
> Om du vill köra enkla skript eller kommandon med ett annat konto när du har installerat operativ systemet lägger du först till kontot på datorn. Dessutom kan du behöva återställa Windows-användargrupper för att köra mer avancerade program, till exempel en Windows Installer.  

#### <a name="account"></a>Konto

Anger det Windows-användarkonto som det här steget använder för att köra kommando raden. Kommando raden körs med behörigheterna för det angivna kontot. Välj **Ange** för att ange det lokala användar-eller domän kontot. Mer information om kör som-kontot för aktivitetssekvens finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Om det här steget anger ett användar konto och körs i Windows PE, Miss lyckas åtgärden. Du kan inte ansluta Windows PE till en domän. Filen **Smsts. log** registrerar felet.  

### <a name="options-for-run-command-line"></a>Alternativ för körning av kommando rad

Förutom standard alternativen konfigurerar du följande ytterligare inställningar på fliken **alternativ** i det här steget i aktivitetssekvensen:  

#### <a name="success-codes"></a>Lyckade koder

Inkludera andra slut koder från skriptet som steget ska utvärdera som lyckat.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Kör PowerShell-skript

Använd det här steget för att köra det angivna Windows PowerShell-skriptet.  

Skriptet måste uppfylla följande kriterier:  

- Den bör inte samverka med Skriv bordet. Skriptet måste köras tyst eller i obevakat läge.  

- Det får inte initiera en egen omstart. Sscript måste begära en omstart med hjälp av standard koden för omstart, 3010. Det här beteendet ser till att aktivitetssekvensen korrekt hanterar omstarten. Om skriptet returnerar en 3010-slutkod, startar aktivitetssekvensen om datorn. Efter omstarten fortsätter aktivitetssekvensen automatiskt.

Det här steget kan köras i fullständigt operativ system eller Windows PE. Om du vill köra det här steget i Windows PE aktiverar du PowerShell i Start avbildningen. Aktivera WinPE-PowerShell-komponenten från fliken **valfria komponenter** i egenskaperna för start avbildningen. Mer information om hur du ändrar en start avbildning finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

> [!NOTE]  
> PowerShell är inte aktiverat som standard i Windows Embedded-operativsystem.  

> [!WARNING]
> Vissa program mot skadlig kod kan oavsiktligt utlösa händelser mot steget Configuration Manager kör PowerShell-skript. Vi rekommenderar att du undantar%windir%\temp\smstspowershellscripts så att program varan mot skadlig kod tillåter att skripten kan köras utan störningar.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **Allmänt**och sedan **kör PowerShell-skript**.

### <a name="variables-for-run-powershell-script"></a>Variabler för körning av PowerShell-skript

Använd följande variabler för aktivitetssekvens i det här steget:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (från och med version 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (från och med version 2002)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Cmdletar för körning av PowerShell-skript

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps)

> [!Note]  
> Använd signerade PowerShell-skript i Unicode-format. ANSI-format, som är standard, fungerar inte med det här steget.

### <a name="properties-for-run-powershell-script"></a>Egenskaper för kör PowerShell-skript

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="package"></a>Paket

Ange det Configuration Manager-paket som innehåller PowerShell-skriptet. Ett paket kan innehålla flera PowerShell-skript.  

#### <a name="script-name"></a>Skriptets namn

Anger namnet på PowerShell-skriptet som ska köras. Det här fältet är obligatoriskt.  

#### <a name="enter-a-powershell-script"></a>Ange ett PowerShell-skript

<!-- 3556028 -->
Från och med version 1902 anger du Windows PowerShell-kod direkt i det här steget. Med den här funktionen kan du köra PowerShell-kommandon under en aktivitetssekvens utan att först skapa och distribuera ett paket med skriptet.

När du lägger till eller redigerar ett skript, innehåller PowerShell-skript fönstret följande åtgärder:  

- Redigera skriptet direkt  

- Öppna ett befintligt skript från en fil  

- Bläddra till ett befintligt godkänt [skript](../../apps/deploy-use/create-deploy-scripts.md) i Configuration Manager

> [!Important]  
> Om du vill dra nytta av den nya Configuration Manager-funktionen kan du, när du har uppdaterat platsen, även uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

#### <a name="parameters"></a>Parametrar

Anger de parametrar som skickas till PowerShell-skriptet. Dessa parametrar är samma som PowerShell-skript parametrarna på kommando raden.  

Ange de parametrar som används av skriptet, inte för Windows PowerShell-kommandoraden.  
Följande exempel innehåller giltiga parametrar:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

Följande exempel innehåller ogiltiga parametrar. De första två objekten är kommando rads parametrar för Windows PowerShell (**-nologo** -och **-ExecutionPolicy unrestricted**). Skriptet använder inte parametrarna.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Använd enkla citat tecken () runt värdet om ett parameter värde innehåller ett specialtecken `'` . Om du använder dubbla citat tecken ( `"` ) kan det leda till att aktivitetssekvensen felaktigt bearbetar parametern.

Exempel: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

Från och med version 2002 ställer du in den här egenskapen till en variabel.<!-- 5690481 --> Om du till exempel anger `%MyScriptVariable%` När aktivitetssekvensen kör skriptet, läggs värdet för den här anpassade variabeln till i PowerShell-kommandoraden.

#### <a name="powershell-execution-policy"></a>PowerShell-körningsprincip

Bestäm vilka PowerShell-skript (om det finns) som du tillåter att ska köras på datorn. Välj någo av följande körningsprincip:  

- **AllSigned**: kör bara skript signerade av en betrodd utgivare  

- **Odefinierad**: definiera inte någon körnings princip  

- **Kringgå**: Läs in alla konfigurationsfiler och kör alla skript. Om du hämtar ett osignerat skript från Internet, behöver Windows PowerShell inte ange behörighet innan skriptet körs.  

> [!IMPORTANT]  
> PowerShell 1,0 har inte stöd för odefinierade och kringgå körnings principer.  

#### <a name="output-to-task-sequence-variable"></a>Utdata till aktivitetssekvens-variabel

<!-- 3556028 -->
Från och med version 1902 sparar du skriptets utdata i en anpassad aktivitetssekvens-variabel.

> [!Note]  
> Från och med version 1910 begränsar Configuration Manager utdata till de sista 1000 tecknen.

Ett exempel på hur du använder den här steg egenskapen finns i [så här ställer du in variabler](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Starta i

<!-- 3556028 -->
Från och med version 1902 anger du startmappen för skriptet, upp till 127 tecken. Den här mappen kan vara en absolut sökväg på måldatorn eller en sökväg i förhållande till den distributionsplatsmapp som innehåller paketet. Det här fältet är valfritt.  

> [!NOTE]  
> Knappen **Bläddra** bläddrar i den lokala datorn efter filer och mappar. Allt du väljer måste också finnas på mål datorn. Det måste finnas på samma plats och med samma fil-och mappnamn.  

#### <a name="time-out"></a>Timeout

<!-- 3556028 -->
Från och med version 1902 anger du ett värde som representerar hur länge Configuration Manager tillåter att PowerShell-skriptet körs. Värdet kan vara mellan en minut och 999 minuter. Standardvärdet är 15 minuter. Det här alternativet är inaktiverat som standard.  

> [!IMPORTANT]  
> Det här steget Miss lyckas om du anger ett värde som inte tillåter tillräckligt med tid för att det angivna skriptet ska kunna slutföras. Det gick inte att utföra hela aktivitetssekvensen beroende på steg-eller grupp villkor. Om timeout går ut, avslutar Configuration Manager PowerShell-processen.  

#### <a name="run-this-step-as-the-following-account"></a>Kör det här steget som följande konto

<!-- 3556028 -->
Från och med version 1902 anger du att PowerShell-skriptet körs som ett annat Windows-användarkonto än det lokala system kontot.  

> [!NOTE]  
> Om du vill köra enkla skript eller kommandon med ett annat konto när du har installerat operativ systemet lägger du först till kontot på datorn. Dessutom kan du behöva återställa Windows-användargrupper för att köra mer komplexa åtgärder.  

#### <a name="account"></a>Konto

<!-- 3556028 -->
Från och med version 1902 anger du det Windows-användarkonto som används i det här steget för att köra PowerShell-skriptet. Det angivna kontot måste vara en lokal administratör på systemet och skriptet körs med behörigheterna för det här kontot. Välj **Ange** för att ange det lokala användar-eller domän kontot. Mer information om kör som-kontot för aktivitetssekvens finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Om det här steget anger ett användar konto och körs i Windows PE, Miss lyckas åtgärden. Du kan inte ansluta Windows PE till en domän. Filen **Smsts. log** registrerar felet.  

### <a name="options-for-run-powershell-script"></a>Alternativ för att köra PowerShell-skript

Förutom standard alternativen konfigurerar du följande ytterligare inställningar på fliken **alternativ** i det här steget i aktivitetssekvensen:  

#### <a name="success-codes"></a>Lyckade koder

<!-- 3556028 -->
Från och med version 1902, inkludera andra slut koder från skriptet som steget ska utvärdera som lyckat.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Kör aktivitetssekvens

> [!Note]  
> Configuration Manager aktiverar den här funktionen som standard i version 1910. I version 1906 eller tidigare aktiverar Configuration Manager inte den här valfria funktionen som standard. Aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

Det här steget Kör en annan aktivitetssekvens. Det skapar en överordnad-underordnad relation mellan aktivitetssekvenser. Med underordnade aktivitetssekvenser kan du skapa fler modulära och återanvändbara aktivitetssekvenser.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **Allmänt**och väljer **Kör aktivitetssekvens**.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Specifikationer och begränsningar för att köra aktivitetssekvens

Tänk på följande när du lägger till en underordnad aktivitetssekvens till en aktivitetssekvens:  

- De överordnade och underordnade aktivitetssekvenser kombineras effektivt till en enda princip som klienten kör.  

- Miljön är global. Om den överordnade aktivitetssekvensen anger en variabel och sedan den underordnade aktivitetssekvensen ändrar variabeln, behåller den det senaste värdet. Om den underordnade aktivitetssekvensen skapar en ny variabel, är den tillgänglig för resten av den överordnade aktivitetssekvensen.  

- Status meddelanden skickas per normal för en åtgärd för en aktivitetssekvens.  

- Aktivitetssekvensen skriver poster till filen **Smsts. log** med nya logg poster som gör den tydlig när en underordnad aktivitetssekvens startar.  

<!--the following points are from SCCMdocs issue #1079-->

- Du kan inte välja en aktivitetssekvens med en start avbildnings referens. För alla distributioner som kräver en start avbildning anger du den i den överordnade aktivitetssekvensen.  

- Om en underordnad aktivitetssekvens har inaktiverats Miss lyckas distributionen. Du kan inte använda alternativet **Fortsätt vid fel** för att undvika den här begränsningen.  

- Om en underordnad aktivitetssekvens innehåller steg som betraktas som *hög påverkan*, identifierar Software Center inte det och visar aviseringen med hög effekt. Ändra egenskaperna för den överordnade aktivitetssekvensen på fliken Användar meddelande för att ange att **Detta är en aktivitetssekvens med hög effekt**.  

- Om en underordnad aktivitetssekvens har en paket referens som saknas, identifierar den överordnade aktivitetssekvensen inte det här läget. Om du redigerar den överordnade aktivitetssekvensen, identifierar den eventuella referenser som saknas i underordnade aktivitetssekvenser när du gör ändringar i den överordnade ordningen.  

### <a name="cmdlets-for-run-task-sequence"></a>Cmdletar för att köra aktivitetssekvensen

Från och med version 1906, hantera det här steget med följande PowerShell-cmdletar:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruntasksequence?view=sccm-ps)
- [New-CMTSStepRunTaskSequence](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruntasksequence?view=sccm-ps)
- [Remove-CMTSStepRunTaskSequence](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruntasksequence?view=sccm-ps)
- [Set-CMTSStepRunTaskSequence](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruntasksequence?view=sccm-ps)

Mer information finns i [versions anmärkningar för 1906 – nya cmdletar](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Egenskaper för att köra aktivitetssekvens

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="select-task-sequence-to-run"></a>Välj aktivitetssekvens som ska köras

Välj **Bläddra** för att välja den underordnade aktivitetssekvensen. Dialog rutan **Välj en aktivitetssekvens** visar inte den överordnade aktivitetssekvensen.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Ange dynamiska variabler

Använd det här steget för att utföra följande åtgärder:  

1. Samla in information från datorn och dess miljö. Ange sedan angivna variabler för aktivitetssekvens med informationen.  

2. Utvärdera definierade regler. Ange variabler för aktivitetssekvens baserat på de regler som utvärderas till sant.  

Det här steget kan köras antingen i hela operativ systemet eller Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **Allmänt**och välj sedan **Ange dynamiska variabler**.

### <a name="variables-for-set-dynamic-variables"></a>Variabler för att ange dynamiska variabler

Aktivitetssekvensen ställer automatiskt in följande variabler för skrivskyddade aktivitetssekvenser:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Cmdletar för att ange dynamiska variabler

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps)
- [New-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Remove-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps)
- [Set-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps)

### <a name="properties-for-set-dynamic-variables"></a>Egenskaper för Ange dynamiska variabler

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="dynamic-rules-and-variables"></a>Dynamiska regler och variabler

Lägg till en regel för att ange en dynamisk variabel som ska användas i aktivitetssekvensen. Ange sedan ett värde för varje variabel som anges i regeln. Lägg också till en eller flera variabler utan att lägga till en regel. När du lägger till en regel väljer du bland följande kategorier:  

- **Dator**: utvärdera värden för maskin varu till gångs tag gen, UUID, serie nummer eller Mac-adress. Ange flera värden vid behov. Om något värde är sant utvärderas regeln som sant. Följande regel utvärderas exempelvis som sant om enhetens serie nummer är 5892087 och MAC-adressen är 22 – A4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Plats**: utvärdera värden för standard-Nätverksgatewayen  

- **Märke och modell**: utvärdera värden för datorns märke och modell. Både märke och modell måste utvärderas till sant för regeln ska utvärderas till sant.

    Ange en asterisk ( `*` ) och frågetecken ( `?` ) som jokertecken. Asterisken matchar flera tecken och frågetecknet matchar ett enskilt tecken. Strängen matchar till exempel `DELL*900?` både `DELL-ABC-9001` och `DELL9009` .  

- **Variabel för aktivitetssekvens**: Lägg till en variabel för aktivitetssekvens, villkor och värde som ska utvärderas. Regeln returnerar sant när värdet för variabeln uppfyller de angivna villkoren.  

    Ange en eller flera variabler som ska anges för en regel som utvärderas till true, eller ange variabler utan att använda en regel. Välj en befintlig variabel eller skapa en anpassad variabel.  

  - **Befintliga variabler för aktivitetssekvens**: Välj en eller flera variabler i en lista med befintliga variabler för aktivitetssekvens. Det går inte att välja mat ris variabler.  

  - **Variabler för anpassad**aktivitetssekvens: definiera en anpassad aktivitetssekvens. Du kan även ange en befintlig aktivitetssekvensvariabel. Den här inställningen är användbar för att ange en befintlig variabel mat ris, till exempel **OSDAdapter**, eftersom variabla matriser inte finns i listan över befintliga variabler för aktivitetssekvens.  

När du har valt variablerna för en regel anger du ett värde för varje variabel. Variabeln har angetts till det angivna värdet när regeln utvärderas till sant. För varje variabel kan du välja **Visa inte det här värdet** för att dölja värdet för variabeln. Som standard döljer vissa befintliga variabler värden, t. ex. **aktivitetssekvensvariabeln OSDCaptureAccountPassword** -variabeln.  

> [!IMPORTANT]  
> När du importerar en aktivitetssekvens med steget **Ange dynamiska variabler** tar Configuration Manager bort alla variabel värden som marker ATS som **Visa inte det här värdet**. När du har importerat aktivitetssekvensen anger du värdet för den dynamiska variabeln igen.

Om du använder alternativet **Visa inte det här värdet visas inte**värdet för variabeln i redigeraren för aktivitetssekvens. Logg filen för aktivitetssekvensen (**Smsts. log**) eller fel sökaren för aktivitetssekvensen visar inte variabelvärdet. Variabeln kan fortfarande användas av aktivitetssekvensen när den körs. Om du inte längre vill att dessa variabler ska vara dolda tar du bort dem först. Definiera sedan om variablerna utan att välja alternativet att dölja dem.  

> [!WARNING]  
> Om du inkluderar variabler i kommando raden **Kör kommando rads** steg, visar logg filen för aktivitetssekvensen den fullständiga kommando raden inklusive variabel värden. För att förhindra att potentiellt känsliga data visas i logg filen ställer du in variabeln **OSDDoNotLogCommand** till `TRUE` .


## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Ange variabel för aktivitetssekvens

Använd det här steget för att ange ett värde för en variabel som används med aktivitetssekvensen.  

Det här steget kan köras antingen i hela operativ systemet eller Windows PE.

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **Allmänt**och välj **ange variabel för aktivitetssekvens**.

### <a name="variables-for-set-task-sequence-variable"></a>Variabler för att ange variabeln aktivitetssekvens

Aktivitetssekvensvariabler läses av aktivitetssekvensåtgärderna och bestämmer beteendet för dessa åtgärder. Mer information om de olika variablerna för aktivitetssekvens och hur du använder dem finns i följande artiklar:  

- [Använda aktivitetssekvensvariabler](using-task-sequence-variables.md)  
- [Aktivitetssekvensvariabler](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Cmdletar för att ange variabeln aktivitetssekvens

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps)

### <a name="properties-for-set-task-sequence-variable"></a>Egenskaper för ange aktivitetssekvens-variabel

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="task-sequence-variable"></a>Aktivitetssekvensvariabel

Ange namnet på en inbyggd eller åtgärds variabel i en aktivitetssekvens eller ange ett eget användardefinierat variabel namn.  

#### <a name="do-not-display-this-value"></a>Visa inte det här värdet

<!--1358330-->
Aktivera det här alternativet om du vill maskera känsliga data som lagras i variabler för aktivitetssekvens. Till exempel när du anger ett lösen ord.

> [!NOTE]
> Aktivera det här alternativet och ange värdet för variabeln aktivitetssekvens. Annars anges inte variabelvärdet som du planerar, vilket kan orsaka oväntade beteenden när aktivitetssekvensen körs.<!--SCCMdocs issue #800-->

Om du använder alternativet **Visa inte det här värdet visas inte**värdet för variabeln i redigeraren för aktivitetssekvens. Logg filen för aktivitetssekvensen (**Smsts. log**) eller fel sökaren för aktivitetssekvensen visar inte variabelvärdet. Variabeln kan fortfarande användas av aktivitetssekvensen när den körs. Om du inte längre vill att den här variabeln ska vara dold tar du bort den först. Definiera sedan om variabeln utan att välja alternativet att dölja den.

> [!WARNING]
> Om du inkluderar variabler i kommando raden **Kör kommando rads** steg, visar logg filen för aktivitetssekvensen den fullständiga kommando raden inklusive variabel värden. För att förhindra att potentiellt känsliga data visas i logg filen ställer du in variabeln **OSDDoNotLogCommand** till `TRUE` .<!-- 6963278 -->

#### <a name="value"></a>Värde  

Aktivitetssekvensen ställer in variabeln till det här värdet. Ange den här variabeln för aktivitetssekvensen till värdet för en annan aktivitetssekvens-variabel med syntaxen `%varname%` .  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Installera Windows och ConfigMgr

Använd det här steget för att utföra över gången från Windows PE till det nya operativ systemet. Det här steget i aktivitetssekvensen är en obligatorisk del av alla OS-distributioner. Den installerar Configuration Manager klienten i det nya operativ systemet och förbereder att aktivitetssekvensen ska fortsätta köras i det nya operativ systemet.  

Det här steget ansvarar för över gången till aktivitetssekvensen från Windows PE till det fullständiga operativ systemet. Steget körs både i Windows PE och det fullständiga operativ systemet på grund av den här över gången. Men eftersom över gången startar i Windows PE kan det bara läggas till i Windows PE-delen av aktivitetssekvensen.  

Det här steget ersätter Sysprep. inf-eller unattend.xml Directory-variabler, till exempel `%WINDIR%` och `%ProgramFiles%` , med installations katalogen för Windows PE `X:\Windows` . Aktivitetssekvensen ignorerar variabler som anges genom att använda de här miljövariablerna.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, Välj **avbildningar**och välj sedan **Installera Windows och ConfigMgr**.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Beteenden för installations programmet för Windows och ConfigMgr

Det här steget utför följande åtgärder:  

#### <a name="preliminaries-windows-pe"></a>Förberedelser: Windows PE  

1. Ersätt variabler för aktivitetssekvens i unattend.xml-filen.  

2. Ladda ned paketet som innehåller Configuration Manager-klienten. Lägg till paketet i den distribuerade avbildningen.  

#### <a name="set-up-windows"></a>Konfigurera Windows  

- Avbildningsbaserad installation  

    1. Inaktivera Configuration Manager-klienten i avbildningen, om den finns. Du kan med andra ord inaktivera Autostart för Configuration Manager-klienttjänsten.  

    2. Uppdatera registret i den distribuerade avbildningen för att starta det distribuerade operativ systemet med samma enhets beteckning som referens datorn.  

    3. Starta om till det distribuerade operativ systemet.  

    4. Windows Mini-installation körs med hjälp av den tidigare angivna Sysprep. inf-eller unattend.xml svarsfil som har all slut användar interaktion under tryckning. Om du använder steget **tillämpa nätverks inställningar** för att ansluta till en domän finns den informationen i svars filen. Windows-miniinstallationsprogrammet ansluter datorn till domänen.  

- Setup.exe-baserad installation. Kör Setup.exe som följer den vanliga Windows-installationsprocessen:  

    1. Kopiera uppgraderings paketet för operativ systemet som anges i steget **tillämpa operativ system** på hård disken.  

    2. Starta om till det nyligen distribuerade operativ systemet.  

    3. Windows Mini-installation körs med hjälp av den tidigare angivna Sysprep. inf-eller unattend.xml svarsfil som har alla inställningar för användar gränssnitt ignorerade. Om du använder steget  **tillämpa nätverks inställningar** för att ansluta till en domän finns den informationen i svars filen. Windows-miniinstallationsprogrammet ansluter datorn till domänen.  

#### <a name="set-up-the-configuration-manager-client"></a>Konfigurera Configuration Manager-klienten  

1. När Windows-miniinstallationen har slutförts återupptas aktivitetssekvensen med hjälp av setupcomplete.cmd. Mer information finns i [köra ett skript när installationen är klar (Setupcomplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. Aktivera eller inaktivera det lokala administratörs kontot, baserat på det alternativ som valts i steget **Använd Windows-inställningar** .  

3. Installera Configuration Manager-klienten med hjälp av det tidigare hämtade paketet och installations egenskaperna som anges i det här steget. Klienten installeras i "etablerings läge". Det här läget förhindrar att klienten bearbetar nya princip begär anden tills aktivitetssekvensen har slutförts. Mer information finns i [etablerings läge](provisioning-mode.md).  

4. Vänta tills klienten är fullt fungerande.  

#### <a name="the-step-completes"></a>Steget har slutförts

Aktivitetssekvensen fortsätter att köra nästa steg.  

> [!Note]  
> Grup principen i Windows bearbetar vanligt vis inte förrän aktivitetssekvensen har slutförts. Det här beteendet är konsekvent i olika versioner av Windows. Andra anpassade åtgärder under aktivitetssekvensen kan utlösa utvärdering av grup princip. Mer information om åtgärds ordningen finns i [köra ett skript när installationen är klar (Setupcomplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Variabler för att installera Windows och ConfigMgr

Använd följande variabler för aktivitetssekvens i det här steget:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Cmdlets för installation av Windows och ConfigMgr

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps)

### <a name="properties-for-setup-windows-and-configmgr"></a>Egenskaper för installation av Windows och ConfigMgr

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="client-package"></a>Klientpaketet

Välj **Bläddra**och välj sedan det Configuration Manager klient installations paket som ska användas med det här steget.  

#### <a name="use-pre-production-client-package-when-available"></a>Använd klientpaket för förproduktion om ett är tillgängligt

Om det finns ett för produktions klient paket tillgängligt, och datorn är medlem i pilot samlingen, använder aktivitetssekvensen det här paketet i stället för produktions klient paketet. För produktions klienten är en nyare version för testning i produktions miljön. Välj **Bläddra**och välj sedan det klient installations paket för för produktion som ska användas med det här steget.  

#### <a name="installation-properties"></a>Installationsegenskaper

Steget aktivitetssekvens anger automatiskt platstilldelning och standard konfigurationen. Använd det här fältet för att ange ytterligare installations egenskaper som ska användas när du installerar-klienten. Om du vill ange flera installationsegenskaper avgränsar du dem med ett blanksteg.  

Ange kommando rads alternativ som ska användas vid klient installation. Ange till exempel `/skipprereq: silverlight.exe` för att informera CCMSetup.exe om att inte installera de nödvändiga komponenterna för Microsoft Silverlight. Mer information om tillgängliga kommando rads alternativ för CCMSetup.exe finns i [om klient installations egenskaper](../../core/clients/deploy/about-client-installation-properties.md).  

När du kör en aktivitetssekvens för operativ system distribution på en Internetbaserad klient, som antingen är Azure AD-ansluten eller använder tokenbaserad autentisering, måste du ange egenskapen [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) i steget **Installera Windows och ConfigMgr** . Till exempel `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### <a name="options-for-setup-windows-and-configmgr"></a>Alternativ för installation av Windows och ConfigMgr

> [!NOTE]  
> Aktivera inte **Fortsätt vid fel** på fliken **alternativ** . Om det uppstår ett fel under det här steget Miss lyckas aktivitetssekvensen oavsett om du aktiverar den här inställningen eller inte.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Uppgradera operativ system

Använd det här steget för att uppgradera en äldre version av Windows till en nyare version av Windows 10.  

Detta steg i aktivitetssekvensen körs bara i det fullständiga operativ systemet. Den körs inte i Windows PE.  

Om du vill lägga till det här steget i redigeraren för aktivitetssekvens väljer du **Lägg till**, väljer **avbildningar**och sedan **Uppgradera operativ system**.

> [!TIP]
> Från och med Windows 10, version 1709, innehåller Media flera versioner. När du konfigurerar en aktivitetssekvens för att använda ett uppgraderings paket för operativ system eller en operativ system avbildning måste du välja en [version som stöds](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).  
>
> Använd för cachelagring av innehåll för att ladda ned ett tillämpligt uppgraderings paket för operativ system innan en användare installerar aktivitetssekvensen. Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>Variabler för uppgradering av OS

Använd följande variabler för aktivitetssekvens i det här steget:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Cmdletar för uppgradering av OS

Hantera det här steget med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps)

### <a name="properties-for-upgrade-os"></a>Egenskaper för uppgradering av OS

På fliken **Egenskaper** för det här steget konfigurerar du de inställningar som beskrivs i det här avsnittet.  

#### <a name="upgrade-package"></a>Uppgraderingspaket

Välj det här alternativet för att ange uppgraderings paketet för Windows 10-operativsystem som ska användas för uppgraderingen.  

#### <a name="source-path"></a>Källsökväg

Anger en lokal sökväg eller en nätverks Sök väg till Windows 10-mediet som Installationsprogrammet för Windows använder. Den här inställningen motsvarar kommando rads alternativet Installationsprogrammet för Windows `/InstallFrom` .

Du kan också ange en variabel, till exempel `%MyContentPath%` eller `%DPC01%` . När du använder en variabel för käll Sök vägen anger du dess värde tidigare i aktivitetssekvensen. Använd till exempel steget [Ladda ned paket innehåll](#BKMK_DownloadPackageContent) för att ange en variabel för platsen för operativ system uppgraderings paketet. Använd sedan variabeln för käll Sök vägen för det här steget.  

#### <a name="edition"></a>Utgåva

Ange versionen i OS-mediet som ska användas för uppgraderingen.  

#### <a name="product-key"></a>Produktnyckel

Ange produkt nyckeln som ska användas för uppgraderings processen.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Ange följande drivrutinsinnehåll i Windows-installationsprogrammet under uppgradering

Lägg till driv rutiner på mål datorn under uppgraderings processen. Drivrutinerna måste vara kompatibla med Windows 10. Den här inställningen motsvarar kommando rads alternativet Installationsprogrammet för Windows `/InstallDriver` . Mer information finns i [installationsprogrammet för Windows kommando rads alternativ](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Ange ett av följande alternativ:  

- **Driv rutins paket**: Välj **Bläddra** och välj ett befintligt driv rutins paket i listan.

- **Mellanlagrat innehåll**: Välj det här alternativet för att ange platsen för driv Rutinens innehåll. Du kan ange en lokal mapp, en nätverkssökväg eller en aktivitetssekvensvariabel. När du använder en variabel för käll Sök vägen anger du dess värde tidigare i aktivitetssekvensen. Du kan till exempel använda steget [Ladda ned paket innehåll](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

> [!TIP]
> Om du vill ha dynamiskt innehåll för flera typer av maskin vara:
>
> - Använd flera instanser av det här steget med villkor för maskin varu typer och separat driv rutins innehåll.
>
> - Använd flera instanser av steget [Ladda ned paket innehåll](task-sequence-steps.md#BKMK_DownloadPackageContent) . Placera innehållet på en gemensam plats och Använd sedan alternativet för **mellanlagrat innehåll** . Fördelen med den här metoden är att aktivitetssekvensen har ett enda **uppgraderings operativ system** steg.

#### <a name="time-out-minutes"></a>Tidsgräns (minuter)

Ange antalet minuter innan Configuration Manager inte det här steget. Det här alternativet är användbart om Installationsprogrammet för Windows stoppar bearbetningen men inte avslutas.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Utför kompatibilitetskontroll i Windows-installationsprogrammet utan att starta uppgraderingen

Utför Installationsprogrammet för Windows kompatibilitetskontroll utan att starta uppgraderings processen. Den här inställningen motsvarar kommando rads alternativet Installationsprogrammet för Windows `/Compat ScanOnly` . Distribuera hela operativ Systems uppgraderings paketet med det här alternativet.

<!--SCCMDocs-pr issue 2812-->
När du aktiverar det här alternativet sätter det här steget inte Configuration Manager klienten i etablerings läge. Installationsprogrammet för Windows körs tyst i bakgrunden och klienten fortsätter att fungera som vanligt. Mer information finns i [etablerings läge](provisioning-mode.md).

Installationsprogrammet returnerar en slutkod efter kontrollen. Följande tabell innehåller några av de vanligaste slut koderna:  

|Slutkod|Information|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Inga kompatibilitetsproblem ("lyckades").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Kompatibilitetsproblem med åtgärder.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Valt alternativ för migrering är inte tillgängligt. Till exempel en uppgradering från Enterprise till Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Inte tillämpligt för Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Det finns inte tillräckligt med ledigt diskutrymme.|  

Mer information om den här parametern finns i [installationsprogrammet för Windows kommando rads alternativ](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorera alla kompatibilitetsmeddelanden som kan avfärdas

Anger att installationen Slutför installationen och ignorerar eventuella kompatibilitetsmeddelanden avfärdas. Den här inställningen motsvarar kommando rads alternativet Installationsprogrammet för Windows `/Compat IgnoreWarning` .  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Uppdatera installationsprogrammet för Windows dynamiskt med Windows Update

Aktivera installations programmet för att utföra dynamiska uppdaterings åtgärder, till exempel Sök, ladda ned och installera uppdateringar. Den här inställningen motsvarar kommando rads alternativet Installationsprogrammet för Windows `/DynamicUpdate` . Den här inställningen är inte kompatibel med Configuration Manager program uppdateringar. Aktivera det här alternativet när du hanterar uppdateringar med fristående Windows Server Update Services (WSUS) eller Windows Update för företag.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Åsidosätt principen och Använd standard Microsoft Update

Åsidosätt tillfälligt den lokala principen i real tid för att köra dynamiska uppdaterings åtgärder. Datorn hämtar uppdateringar från Windows Update.