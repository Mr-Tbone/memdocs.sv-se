---
title: Skapa en aktivitetssekvens för en operativsystemuppgradering
titleSuffix: Configuration Manager
description: Använda en aktivitetssekvens för att automatiskt uppgradera från Windows 7 eller senare till Windows 10
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 907c36b6f06bbf4fbbabb9ee1b2df6cadb0acb75
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125465"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Skapa en aktivitetssekvens för att uppgradera ett operativ system i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd aktivitetssekvenser i Configuration Manager för att automatiskt uppgradera ett operativ system på mål datorn. Den här uppgraderingen kan vara från Windows 7 eller senare till Windows 10, eller från Windows Server 2012 eller senare till Windows Server 2016. Skapa en aktivitetssekvens som refererar till uppgraderings paketet för operativ systemet och eventuellt annat innehåll att installera, till exempel program eller program uppdateringar. Aktivitetssekvensen för att uppgradera ett operativ system är en del av [uppgraderings Fönstren till det senaste versions](upgrade-windows-to-the-latest-version.md) scenariot.  


## <a name="prerequisites"></a>Förutsättningar

Innan du skapar aktivitetssekvensen måste följande krav vara på plats:

### <a name="required"></a>Obligatorisk

- [Uppgraderings paketet för operativ systemet](../get-started/manage-operating-system-upgrade-packages.md) måste vara tillgängligt i Configuration Manager-konsolen.  

- När du uppgraderar till Windows Server 2016 väljer du inställningen **ignorera eventuella meddelanden som kan ignoreras** i steget uppgradera operativ system. Annars Miss lyckas uppgraderingen.  

### <a name="required-if-used"></a>Obligatoriskt (om det används)  

- [Program uppdateringar](../../sum/get-started/synchronize-software-updates.md) måste synkroniseras i Configuration Manager-konsolen.  

- [Program](../../apps/deploy-use/create-applications.md) måste läggas till i Configuration Manager-konsolen.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a>Skapa en aktivitetssekvens för att uppgradera ett operativ system  

Om du vill uppgradera operativ systemet på klienter skapar du en aktivitetssekvens och väljer **uppgradera ett operativ system från uppgraderings paket** i guiden skapa aktivitetssekvens. Guiden lägger till aktivitetssekvenser för att uppgradera operativ systemet, tillämpa program uppdateringar och installera program.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan **aktivitetssekvenser**.  

2. Välj **skapa**aktivitetssekvens i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

3. På sidan **skapa en ny aktivitetssekvens** i guiden skapa aktivitetssekvens väljer du **uppgradera ett operativ system från ett uppgraderings paket**och väljer sedan **Nästa**.  

4. På sidan **information om aktivitetssekvens** anger du följande inställningar:  

    - **Namn på aktivitetssekvens**: Ange ett namn på aktivitetssekvensen.  

    - **Beskrivning**: Ange en beskrivning om du vill.  

5. På sidan **Uppgradera operativ systemet Windows** anger du följande inställningar:  

    - **Uppgraderings paket**: Ange det uppgraderings paket som innehåller källfilerna för operativ system uppgradering. Kontrol lera att du har valt rätt uppgraderings paket genom att titta på informationen i fönstret **Egenskaper** . Mer information finns i [hantera OS-uppgraderings paket](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Versions index**: om det finns flera tillgängliga OS Edition-index i paketet väljer du det önskade versions indexet. Som standard väljs det första indexet i guiden.  

    - **Produkt nyckel**: Ange produkt nyckeln för Windows för det operativ system som ska installeras. Ange kodade volym licens nycklar eller standard produkt nycklar. Om du använder en standard produkt nyckel separerar du varje grupp om fem tecken med ett bindestreck ( `-` ). Till exempel: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. När uppgraderingen är för en volym licens version kanske produkt nyckeln inte krävs.  

        > [!Note]  
        > Den här produkt nyckeln kan vara en MAK (Multiple Activation Key) eller en allmän volym licens nyckel (GVLK). En GVLK kallas även för en klient installations nyckel för nyckel hanterings tjänst (KMS). Mer information finns i [Planera för volym aktivering](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). En lista över konfigurations nycklar för KMS-klienter finns i [bilaga a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) i aktiverings guiden för Windows Server.

    - **Ignorera eventuella meddelanden som kan ignoreras**: Välj den här inställningen om du uppgraderar till Windows Server 2016. Om du inte väljer den här inställningen kan aktivitetssekvensen inte slutföras eftersom Installationsprogrammet för Windows väntar på att användaren ska välja **Bekräfta** i en dialog ruta för Windows-appar.  

6. På sidan **Inkludera uppdateringar** anger du om obligatoriska, alla eller inga program uppdateringar ska installeras. Välj sedan **Nästa**. Om du anger att program uppdateringarna ska installeras, installerar Configuration Manager bara de uppdateringar som är riktade mot de samlingar som mål datorn är medlem i.  

7. På sidan **installera program** anger du de program som ska installeras på mål datorn och väljer sedan **Nästa**. Om du väljer fler än ett program anger du även om aktivitetssekvensen ska fortsätta om installationen av ett enskilt program Miss lyckas.  

8. Slutför guiden.  

> [!Important]  
> När aktivitetssekvensen körs på en enhet, skapar Configuration Manager klienten flera skript för att styra hur aktivitetssekvensen fungerar i olika scenarier. När aktivitetssekvensen har slutförts tar klienten inte bort skripten förrän datorn har startats om. Dessa skriptfiler innehåller inte känslig information.  

Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller ytterligare grupper med rekommenderade åtgärder som ska läggas till före och efter uppgraderings processen. Dessa åtgärder är gemensamma för många kunder som har lyckats uppgradera enheter till Windows 10. Mer information finns i rekommenderade steg [i aktivitetssekvensen för att förbereda för uppgradering](#recommended-task-sequence-steps-to-prepare-for-upgrade) och [efter bearbetning](#recommended-task-sequence-steps-for-post-processing).

Från och med version 1806 innehåller den här mallen även en grupp med rekommenderade åtgärder som du kan lägga till om uppgraderings processen Miss lyckas. De här åtgärderna gör det enklare att felsöka. Mer information finns i [rekommenderade instruktioner för aktivitetssekvenser vid haveriation](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Konfigurera innehåll i förcachen

<!--1021244-->
Med funktionen för cachelagring för tillgängliga distributioner av aktivitetssekvenser kan klienterna Ladda ned relevanta OS-uppgraderings paket innehåll innan en användare installerar aktivitetssekvensen.  

Mer information finns i [Konfigurera förinställt innehåll för cache](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Rekommenderade åtgärder för aktivitetssekvenser för att förbereda för uppgradering

Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller ytterligare grupper med rekommenderade åtgärder som ska läggas till före uppgraderings processen. De här åtgärderna i **förbereda för uppgraderings** gruppen är gemensamma för många kunder som lyckas uppgradera enheter till Windows 10. Om du har en befintlig aktivitetssekvens som inte redan har de här åtgärderna kan du manuellt lägga till dem i aktivitetssekvensen i **förberedelse för uppgraderings** gruppen.  

### <a name="battery-checks"></a>Batteri kontroller

Lägg till steg i den här gruppen för att kontrol lera om datorn använder batteri eller kabelansluten ström. Den här åtgärden kräver ett anpassat skript eller verktyg för att utföra den här kontrollen.

#### <a name="battery-check-example"></a>Exempel på batteri kontroll

Använd WbemTest och Anslut till `root\cimv2` namn området. Kör sedan följande fråga:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Om det returnerar några resultat körs enheten på batteri. Annars är enheten ansluten till en kabelansluten ström.  

### <a name="networkwired-connection-checks"></a>Kontroller för nätverks-/kabelanslutna anslutningar

Lägg till steg i den här gruppen för att kontrol lera om datorn är ansluten till ett nätverk och inte använder en trådlös anslutning. Den här åtgärden kräver ett anpassat skript eller verktyg för att utföra den här kontrollen.

#### <a name="network-check-example"></a>Exempel på nätverks kontroll

Använd WbemTest och Anslut till `root\cimv2` namn området. Kör sedan följande fråga:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Om det returnerar några resultat körs enheten på Wi-Fi. Annars är enheten ansluten till tråd bunden nätverks anslutning.

### <a name="remove-incompatible-applications"></a>Ta bort inkompatibla program

Lägg till steg i den här gruppen för att ta bort alla program som inte är kompatibla med den här versionen av Windows 10. Metoden för att avinstallera ett program varierar.  

Om programmet använder Windows Installer kopierar du kommando raden **Avinstallera program** från fliken **program** i egenskaperna för Windows Installer distributions typ för programmet. Lägg sedan till steget **Kör kommando rad** i den här gruppen med kommando raden avinstallera program. Till exempel:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Ta bort inkompatibla driv rutiner

Lägg till steg i den här gruppen för att ta bort alla driv rutiner som inte är kompatibla med den här versionen av Windows 10.  

### <a name="removesuspend-third-party-security"></a>Ta bort/pausa säkerhet från tredje part

Lägg till steg i den här gruppen för att ta bort eller pausa säkerhets program från tredje part, till exempel Antivirus.  

Om du använder ett disk krypterings program från tredje part, anger du dess krypterings driv rutin för Installationsprogrammet för Windows med `/ReflectDrivers` [kommando rads alternativet](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Lägg till [variabel steget Ställ in](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) aktivitetssekvens i aktivitetssekvensen i den här gruppen. Ange variabeln för aktivitetssekvensen till **OSDSetupAdditionalUpgradeOptions**. Ställ in värdet på `/ReflectDrivers` med sökvägen till driv rutinen. Den här [aktivitetssekvensen](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) lägger till installationsprogrammet för Windows kommando raden som används av aktivitetssekvensen. Kontakta program varu leverantören om du behöver ytterligare vägledning om den här processen.  

### <a name="download-package-content-task-sequence-step"></a>Steg i aktivitetssekvens för att ladda ned paket innehåll  

Använd steget [Ladda ned paket innehåll](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) innan du **uppgraderar operativ systemet** i följande scenarier:  

- Du använder en enda uppgraderings aktivitetssekvens för både x86-och x64-plattformar. Inkludera två **innehålls steg för hämtnings paket** i **förberedelse för uppgraderings** gruppen. Ange villkor för varje steg för att identifiera klient arkitekturen. Det här tillståndet gör att steget endast laddar ned rätt uppgraderings paket för operativ systemet. Konfigurera **Ladda ned paketinnehåll**-stegen så att de använder samma variabel och använd variabeln för mediesökvägen i steget **Uppgradera operativsystem**.  

- Om du vill ladda ned relevanta drivrutinspaket dynamiskt använder du två **Ladda ned paketinnehåll**-steg med villkor som identifierar lämplig maskinvarutyp för varje drivrutinspaket. Konfigurera varje steg för **hämtning av paket innehåll** för att använda samma variabel. Använd sedan variabeln för det **mellanlagrade innehålls** värdet i avsnittet driv rutiner i steget **Uppgradera operativ system** .  

    > [!NOTE]  
    > Configuration Manager lägger till ett numeriskt suffix till variabel namnet. Om du till exempel anger `%mycontent%` som en anpassad variabel lagrar klienten allt innehåll som refereras till på den här platsen. När du refererar till variabeln i ett efterföljande steg, till exempel **Uppgradera operativ system**, använder du variabeln med ett numeriskt suffix. I det här exemplet, `%mycontent01%` eller `%mycontent02%` , där numret motsvarar den ordning som steget **Hämta paket innehåll** innehåller, visas det här innehållet.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Rekommenderade steg för aktivitetssekvenser för efter bearbetning

När du har skapat aktivitetssekvensen lägger du till ytterligare steg i **efter bearbetnings** gruppen i aktivitetssekvensen.  

> [!NOTE]  
> Den här aktivitetssekvensen är inte linjär. Det finns villkor för steg som kan påverka resultatet av aktivitetssekvensen. Det här beteendet beror på om den har uppgraderat klient datorn eller om den måste återställa klient datorn till det ursprungliga operativ systemet.  

Standardmallen för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller ytterligare grupper med rekommenderade åtgärder som ska läggas till efter uppgraderings processen. De här åtgärderna i **efter bearbetnings** gruppen är gemensamma för många kunder som lyckas uppgradera enheter till Windows 10. Om du har en befintlig aktivitetssekvens som inte redan har de här åtgärderna kan du manuellt lägga till dem i aktivitetssekvensen i **efter bearbetnings** gruppen.  

### <a name="apply-setup-based-drivers"></a>Använd installationsbaserade driv rutiner

Lägg till steg i den här gruppen för att installera installationsbaserade driv rutiner (. exe) från paket.  

### <a name="installenable-third-party-security"></a>Installera/Aktivera säkerhet från tredje part

Lägg till steg i den här gruppen för att installera eller aktivera säkerhets program från tredje part, till exempel antivirus program.  

### <a name="set-windows-default-apps-and-associations"></a>Ange standard-appar och-associationer för Windows

Lägg till steg i den här gruppen för att ställa in Windows-standardappar och fil associationer.

1. Förbered en referens dator med dina önskade app-associationer.
1. Kör följande kommando rad för att exportera:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Lägg till XML-filen i ett paket.
1. Lägg till steget [Kör kommando rad](../understand/task-sequence-steps.md#BKMK_RunCommandLine) i den här gruppen. Ange det paket som innehåller XML-filen och ange följande kommando rad:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Mer information finns i [Exportera eller importera standard program associationer](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).

### <a name="apply-customizations-and-personalization"></a>Använda anpassningar och anpassning

Lägg till steg i den här gruppen om du vill använda anpassningar av Start-menyn, till exempel ordna program grupper. Mer information finns i [Anpassa Start skärmen](/windows-hardware/manufacture/desktop/customize-the-start-screen).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Valfria steg för aktivitetssekvens för återställning  

Om något går fel med uppgraderings processen när datorn har startats om, Installationsprogrammet för Windows återställa systemet till föregående operativ system. Aktivitetssekvensen fortsätter sedan med alla steg i **återställnings** gruppen. När du har skapat aktivitetssekvensen kan du lägga till valfria steg i den här gruppen vid behov. Du kan till exempel ångra eventuella ändringar som gjorts i systemet i gruppen Förbered för uppgradering, till exempel avinstallera inkompatibel program vara.


## <a name="recommended-task-sequence-steps-on-failure"></a>Rekommenderade åtgärder vid körning av aktivitetssekvensen

<!--1358500-->
Från och med version 1806 innehåller standardmallen för aktivitetssekvenser för Windows 10 uppgradering på plats en grupp för att **köra åtgärder vid ett haveri**. Den här gruppen innehåller rekommenderade åtgärder som du kan lägga till om uppgraderings processen Miss lyckas. De här åtgärderna gör det enklare att felsöka.

### <a name="collect-logs"></a>Samla in loggar

Lägg till steg i den här gruppen om du vill samla in loggar från klienten.  

- En vanlig metod är att kopiera loggfilerna till en nätverks resurs. Använd steget [Anslut till nätverksmapp](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) för att upprätta anslutningen.  

- Om du vill utföra kopierings åtgärden använder du ett anpassat skript eller verktyg med [kommando raden kör](../understand/task-sequence-steps.md#BKMK_RunCommandLine) eller [kör PowerShell-skript](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .  

- Filer som ska samlas in kan innehålla följande loggar:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Mer information om Setupact. log och andra Installationsprogrammet för Windows loggar finns i [installationsprogrammet för Windows loggfiler](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

- Mer information om Configuration Manager klient loggar finns i [Configuration Manager klient loggar](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- Mer information om **_SMSTSLogPath** och andra användbara variabler finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md).  

### <a name="run-diagnostic-tools"></a>Köra diagnostikverktyg

Lägg till steg i den här gruppen om du vill köra ytterligare diagnostiska verktyg. Automatisera de här verktygen för att samla in ytterligare information från systemet direkt efter att det har misslyckats.  

Ett sådant verktyg är Windows- [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Det är ett fristående diagnostikverktyg för att få information om varför en Windows 10-uppgradering misslyckades.  

- [Skapa ett paket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) för verktyget i Configuration Manager.  

- Lägg till steget [Kör kommando rad](../understand/task-sequence-steps.md#BKMK_RunCommandLine) i den här gruppen av aktivitetssekvensen. Använd alternativet **paket** för att referera till verktyget. Följande sträng är ett exempel på en **kommando rad**:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> Använd alltid den senaste versionen av SetupDiag för de senaste funktionerna och korrigeringarna på kända problem. Mer information finns i [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Ytterligare rekommendationer

### <a name="windows-documentation"></a>Windows-dokumentation

Läs igenom Windows-dokumentationen för att [lösa Windows 10-uppgraderings fel](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Den här artikeln innehåller även detaljerad information om uppgraderings processen.  

### <a name="check-minimum-disk-space"></a>Kontrol lera minsta disk utrymme

I steget standard **kontroll beredskap** aktiverar du **minsta ledigt disk utrymme (MB)**. Ange värdet till minst **16384** (16 GB) för ett 32-bitars uppgraderings paket för operativ system, eller **20480** (20 GB) för 64-bitars.  

### <a name="retry-downloading-policy"></a>Försök att ladda ned princip igen

Använd **SMSTSDownloadRetryCount** - [variabeln](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) för att försöka hämta principen igen. Som standard försöker klienten igen två gånger; den här variabeln anges till två (2). Om klienterna inte är på en kabelansluten intranäts nätverks anslutning, kommer ytterligare försök att hjälpa klienten att hämta principer. Om den här variabeln används får ingen negativ sido effekt, förutom fördröjt fel om den inte kan ladda ned princip.<!--501016--> Öka också **SMSTSDownloadRetryDelay** -variabeln från standardvärdet på 15 sekunder.  

### <a name="perform-an-inline-compatibility-assessment"></a>Utföra en intern kompatibilitetskontroll

1. Lägg till ett andra **uppgraderings operativ system** steg tidigt i **förbereda för uppgraderings** gruppen.  

    1. Bedöm namn för *uppgradering*av namn.
    1. Ange samma uppgraderings paket och aktivera sedan alternativet för att **utföra installationsprogrammet för Windows kompatibilitetskontroll utan att starta uppgraderingen**.
    1. Aktivera **Fortsätt vid fel** på fliken Alternativ.  

1. Omedelbart efter det här steget för *uppgraderings utvärdering* lägger du till steget **Kör kommando rad** . Ange följande kommando rad:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

    Det här kommandot gör att kommando tolken avslutas med den angivna slutkod som inte är noll, vilket innebär att aktivitetssekvensen anser ett fel.

1. Lägg till följande villkor på fliken **alternativ** :

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

    Det här tillståndet innebär att aktivitetssekvensen bara kör **kommando rads** steget för körning om retur koden inte är en lyckad kod.

Retur koden `3247440400` är den decimal som motsvarar MOSETUP_E_COMPAT_SCANONLY (0xC1900210), som är en lyckad kompatibilitetskontroll utan problem. Om steget för *uppgraderings utvärdering* lyckas och returnerar `3247440400` , hoppar aktivitetssekvensen över det här steget för att **köra kommando raden** och fortsätter. Om bedömnings steget returnerar någon annan returkod körs det här **körnings kommando rads** steget. Eftersom kommandot avslutas med en returkod som inte är noll, Miss lyckas även aktivitetssekvensen. Logg-och status meddelanden i aktivitetssekvensen innehåller retur koden från Installationsprogrammet för Windows kompatibilitetskontroll. Mer information om **_SMSTSOSUpgradeActionReturnCode**finns i [variabler för aktivitetssekvensen](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

Mer information finns i steget [Uppgradera operativ systemets](../understand/task-sequence-steps.md#BKMK_UpgradeOS) aktivitetssekvens.

### <a name="convert-from-bios-to-uefi"></a>Konvertera från BIOS till UEFI

Om du vill ändra enheten från BIOS till UEFI under den här aktivitetssekvensen, se [konvertera från BIOS till UEFI under en uppgradering på plats](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).  

### <a name="manage-bitlocker"></a>Hantera BitLocker

<!--SCCMDocs issue #494-->
Om du använder BitLocker Disk Encryption inaktive ras som standard Installationsprogrammet för Windows automatiskt under uppgraderingen. Från och med Windows 10 version 1803 innehåller Installationsprogrammet för Windows `/BitLocker` kommando rads parametern för att styra det här beteendet. Om dina säkerhets krav gör att du alltid måste ha en aktiv disk kryptering, använder du **OSDSetupAdditionalUpgradeOptions** - [variabeln](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) i gruppen **Förbered för uppgradering** för att inkludera `/BitLocker TryKeepActive` . Mer information finns i [installationsprogrammet för Windows kommando rads alternativ](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Ta bort standard appar

<!--SCCMDocs issue #526-->
Vissa kunder tar bort standard etablerade appar i Windows 10. Till exempel Bing väder-appen eller Microsoft Harpan-samlingen. I vissa situationer returneras dessa appar efter uppdatering av Windows 10. Mer information finns i [så här håller du appar borttagna från Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Lägg till steget **Kör kommando rad** i aktivitetssekvensen i **förberedelse för uppgraderings** gruppen. Ange en kommando rad som liknar följande exempel:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
