---
title: 'Anpassa startavbildningar '
titleSuffix: Configuration Manager
description: Lär dig flera sätt att använda Configuration Manager eller kommando rads verktyget DISM (Deployment Image Servicing and Management) för att anpassa en start avbildning.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc679ec7e73e9d43902ad70e09fb2a01c95eed65
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906890"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Anpassa Start avbildningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Varje version av Configuration Manager har stöd för en speciell version av Windows ADK (Assessment and Deployment Kit). Du kan underhålla eller anpassa start avbildningar från Configuration Manager-konsolen när de baseras på en Windows PE-version från den version av Windows ADK som stöds. Andra startavbildningar måste du anpassa med någon annan metod, till exempel genom att använda kommandoradsverktyget DISM (Deployment Image Servicing and Management) som ingår i Windows AIK och Windows ADK.  

 Följande innehåller den version av Windows ADK som stöds, den Windows PE-version som start avbildningen är baserad på och som kan anpassas i Configuration Manager-konsolen och de Windows PE-versioner som start avbildningen baseras på och som du kan anpassa med DISM och sedan lägga till avbildningen i Configuration Manager.  

- **Windows ADK-version**  

   Windows ADK för Windows 10  

- **Windows PE-versioner för start avbildningar som går att anpassa från Configuration Manager-konsolen**  

   Windows PE 10  

- **Windows PE-versioner som stöds för start avbildningar som inte kan anpassas från Configuration Manager-konsolen**  

   Windows PE 3.1<sup>1</sup> och Windows PE 5  

   <sup>1</sup> du kan bara lägga till en start avbildning som ska Configuration Manager när den är baserad på Windows PE 3,1. Installera tillägget Windows AIK för Windows 7 SP1 för att uppgradera Windows AIK för Windows 7 (baserat på Windows PE 3) med tillägget Windows AIK för Windows 7 SP1 (baserat på Windows PE 3.1). Du kan ladda ned tillägget Windows AIK för Windows 7 SP1 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

   Om du till exempel har Configuration Manager kan du anpassa start avbildningar från Windows ADK för Windows 10 (baserat på Windows PE 10) från Configuration Manager-konsolen. Även om det finns stöd för startavbildningar baserade på Windows PE 5 måste du anpassa dem från en annan dator och använda den DISM-version som är installerad med Windows ADK för Windows 8. Sedan kan du lägga till Start avbildningen i Configuration Manager-konsolen.  

  Procedurerna i det här avsnittet visar hur du lägger till valfria komponenter som krävs av Configuration Manager i Start avbildningen med hjälp av följande Windows PE-paket:  

- **WinPE-WMI**: Lägger till stöd för Windows Management Instrumentation (WMI).  

- **WinPE-skript**: Lägger till stöd för Windows Script Host (WSH).  

- **WinPE-WDS-Tools**: Installerar Windows Deployment Services-verktyg.  

  Det finns andra Windows PE-paket som du också kan lägga till. Mer information om valfria komponenter som du kan lägga till i Start avbildningen finns i [WinPE: lägga till paket (alternativ referens för valfria komponenter)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

> [!NOTE]
>När du startar i WinPE från en anpassad startavbildning som innehåller verktyg som du har lagt till kan du öppna en kommandotolk från WinPE och ange filnamnet i verktyget för att köra den. Platsen för dessa verktyg läggs automatiskt till i variabeln Path. Kommando tolken kan bara läggas till om inställningen **Aktivera kommando stöd (endast testning)** är markerad på fliken **anpassning** i Start avbildningens egenskaper.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Anpassa en startavbildning som använder Windows PE 5  
 Om du vill du anpassa en startavbildning som använder Windows PE 5 måste du installera Windows ADK och använda kommandoradsverktyget DISM för att montera startavbildningen, lägga till valfria komponenter och drivrutiner och sedan spara ändringarna. Använd följande procedur för att anpassa startavbildningen.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Så här anpassar du en startavbildning som använder Windows PE 5  

1. Installera Windows ADK på en dator som inte har någon annan version av Windows AIK eller Windows ADK, och som inte har några Configuration Manager-komponenter installerade.  

2. Ladda ned Windows ADK för Windows 8.1 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39982).  

3. Kopiera start avbildningen (wimpe. wim) från Windows ADK-installationsmappen (till exempel <*installations Sök väg*> \Windows Kits \\ < *version*> \Assessment och Deployment Kit\Windows Preinstallation Environment \\ < *x86 eller amd64* > \\ < *locale*>) till en målmapp på den dator som du vill anpassa start avbildningen från. I den här proceduren är C:\WinPEWAIK målmappens namn.  

4. Använd DISM för att montera startavbildningen i en lokal Windows PE-mapp. Ange till exempel följande kommandorad:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Där C:\WinPEWAIK är den mapp som innehåller startavbildningen och där C:\WinPEMount är den monterade mappen.  

   > [!NOTE]
   >  Mer information finns i referens för [DISM (Deployment Image Servicing and Management)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. När du har monterat startavbildningen använder du DISM för att lägga till valfria komponenter i startavbildningen. I Windows PE 5 finns de valfria 64-bitarskomponenterna i <*Installationssökväg*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

   > [!NOTE]
   >  I den här proceduren används följande plats för de valfria komponenterna: C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Du kanske använder någon annan sökväg, beroende på vilken version och vilka installationsalternativ du väljer för Windows ADK.  

    Installera valfria komponenter genom att skriva följande:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WMI_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-Scripting** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WDS-Tools_** *<locale\>* **.cab"**  

    Där C:\WinPEMount är den monterade mappen och locale är språkvarianten för komponenterna. Till exempel skulle du skriva följande för språkvarianten **en-us**:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Mer information om valfria komponenter som du kan lägga till i Start avbildningen finns i referens för [valfria Windows PE-komponenter](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

6. Använd DISM om drivrutiner måste läggas till i startavbildningen. Skriv följande om du måste lägga till drivrutiner i startavbildningen:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

    Där C:\WinPEMount är den monterade mappen.  

7. Demontera startavbildningsfilen och spara ändringarna genom att skriva följande:  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Där C:\WinPEMount är den monterade mappen.  

8. Lägg till den uppdaterade start avbildningen i Configuration Manager för att göra den tillgänglig för användning i aktivitetssekvenser. Importera den uppdaterade startavbildningen genom att utföra följande steg:  

   1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

   2. I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

   3. På fliken **Start** går du till gruppen **Skapa** och klickar på **Lägg till startavbildning** för att starta guiden för att lägga till en startavbildning.  

   4. På sidan **Datakälla** anger du följande alternativ och klickar sedan på **Nästa**.  

      - I rutan **Sökväg** anger du sökvägen till den uppdaterade startavbildningsfilen. Den angivna sökvägen måste vara en giltig nätverkssökväg i UNC-format. Exempel: **\\\\<** <em>Server namn</em> **>\\<** <em>WinPEWAIK resurs</em> **> \Winpe.wim**.  

      - Välj startavbildningen i den nedrullningsbara listan **Startavbildningsfil**. Om WIM-filen innehåller flera startavbildningar visas var och en i listan.  

   5. På sidan **Allmänt** anger du följande alternativ och klickar sedan på **Nästa**.  

      -   I rutan **Namn** anger du ett unikt namn på startavbildningen.  

      -   I rutan **Version** anger du ett versionsnummer för startavbildningen.  

      -   I rutan **Kommentar** beskriver du kort hur startavbildningen ska användas.  

   6. Slutför guiden.  

9. Du kan aktivera ett kommandogränssnitt (shell) i startavbildningen för att felsöka det i Windows PE. Aktivera ett shell för kommandon genom att utföra följande steg.  

   1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

   2. I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

   3. Leta reda på den nya startavbildningen i listan och identifiera avbildningens paket-ID. Paket-ID:t visas i kolumnen **Avbildnings-ID** för startavbildningen.  

   4. Öppna Testprogram för Windows Management Instrumentation genom att skriva **wbemtest** i en kommandotolk.  

   5. Skriv **\\\\<** <em>SMS-providerns dator</em> **> \root\sms\ Site_<** <em>platskod</em> **>** i **namn område**och klicka sedan på **Anslut**.  

   6. Klicka på **Öppna instans**, skriv **sms_bootimagepackage.packageID="<packageID\>"** och klicka sedan på **OK**. Som paket-ID anger du det värde som du identifierade i steg 3.  

   7. Klicka på **Uppdatera objekt** och sedan på **Aktivera LabShell** i rutan **Egenskaper**.  

   8. Klicka på **Redigera egenskap**, ändra värdet till **SANT**, och klicka på **Spara egenskap**.  

   9. Klicka på **Spara objekt**, och avsluta Testare för Windows Management Instrumentation.  

10. Du måste distribuera startavbildningen till distributionsplatser, till distributionsplatsgrupper eller till samlingar som är associerade till distributionsplatsgrupper, innan du kan använda startavbildningen i en aktivitetssekvens. Anpassa startavbildningen genom att utföra följande steg.  

    1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

    2.  I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

    3.  Klicka på den startavbildning som identifierades i steg 3.  

    4.  På fliken **Start** går du till gruppen **Distribution** och klickar på **Uppdatera distributionsplatser**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Anpassa en startavbildning som använder Windows PE 3.1  
 Om du vill anpassa en startavbildning som använder WinPE 3.1 måste du installera Windows AIK och Windows AIK-tillägget för Windows 7 SP1, och använda kommandoradsverktyget DISM för att montera startavbildningen, lägga till valfria komponenter och drivrutiner och sedan spara ändringarna. Använd följande procedur för att anpassa startavbildningen.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Så här anpassar du en startavbildning som använder Windows PE 3.1  

1. Installera Windows AIK på en dator som inte har någon annan version av Windows AIK eller Windows ADK, och som inte har några Configuration Manager-komponenter installerade. Hämta Windows AIK från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5753).  

2. Installera tillägget Windows AIK för Windows 7 med SP1 på datorn från steg 1. Ladda ned tillägget Windows AIK för Windows 7 SP1 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

3. Kopiera startavbildningen (wimpe.wim) från Windows ADK-installationsmappen (till exempel <** Installationssökväg\\>\Windows AIK\Tools\PETools\amd64\) till en mapp på den dator som ska användas för att anpassa startavbildningen. I den här proceduren används mappnamnet C:\WinPEWAIK.  

4. Använd DISM för att montera startavbildningen i en lokal Windows PE-mapp. Ange till exempel följande kommandorad:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Där C:\WinPEWAIK är den mapp som innehåller startavbildningen och där C:\WinPEMount är den monterade mappen.  

   > [!NOTE]
   > Mer information finns i referens för [DISM (Deployment Image Servicing and Management)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. När du har monterat startavbildningen använder du DISM för att lägga till valfria komponenter i startavbildningen. I till exempel Windows PE 3.1 finns de valfria komponenterna i <*Installationssökväg*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

   > [!NOTE]
   >  I den här proceduren används följande plats för de valfria komponenterna: C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Du kanske använder någon annan sökväg, beroende på vilken version och vilka installationsalternativ du väljer för Windows AIK.  

    Installera valfria komponenter genom att skriva följande:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<locale\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<locale\>* **.cab"**  

    Där C:\WinPEMount är den monterade mappen och locale är språkvarianten för komponenterna. Till exempel skulle du skriva följande för språkvarianten **en-us**:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Mer information om de olika paket som du kan lägga till i Start avbildningen finns i [lägga till ett paket i en Windows PE-avbildning](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd799312(v=ws.10)).

6. Använd DISM om drivrutiner måste läggas till i startavbildningen. Skriv följande om du måste lägga till drivrutiner i startavbildningen:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

    Där C:\WinPEMount är den monterade mappen.  

7. Demontera startavbildningsfilen och spara ändringarna genom att skriva följande:  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Där C:\WinPEMount är den monterade mappen.  

8. Lägg till den uppdaterade start avbildningen i Configuration Manager för att göra den tillgänglig för användning i aktivitetssekvenser. Importera den uppdaterade startavbildningen genom att utföra följande steg:  

   1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

   2. I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

   3. På fliken **Start** går du till gruppen **Skapa** och klickar på **Lägg till startavbildning** för att starta guiden för att lägga till en startavbildning.  

   4. På sidan **Datakälla** anger du följande alternativ och klickar sedan på **Nästa**.  

      - I rutan **Sökväg** anger du sökvägen till den uppdaterade startavbildningsfilen. Den angivna sökvägen måste vara en giltig nätverkssökväg i UNC-format. Exempel: **\\\\<** <em>Server namn</em> **>\\<** <em>WinPEWAIK resurs</em> **> \Winpe.wim**.  

      - Välj startavbildningen i den nedrullningsbara listan **Startavbildningsfil**. Om WIM-filen innehåller flera startavbildningar visas var och en i listan.  

   5. På sidan **Allmänt** anger du följande alternativ och klickar sedan på **Nästa**.  

      -   I rutan **Namn** anger du ett unikt namn på startavbildningen.  

      -   I rutan **Version** anger du ett versionsnummer för startavbildningen.  

      -   I rutan **Kommentar** beskriver du kort hur startavbildningen ska användas.  

   6. Slutför guiden.  

9. Du kan aktivera ett kommandogränssnitt (shell) i startavbildningen för att felsöka det i Windows PE. Aktivera ett shell för kommandon genom att utföra följande steg.  

   1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

   2. I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

   3. Leta reda på den nya startavbildningen i listan och identifiera avbildningens paket-ID. Paket-ID:t visas i kolumnen **Avbildnings-ID** för startavbildningen.  

   4. Öppna Testprogram för Windows Management Instrumentation genom att skriva **wbemtest** i en kommandotolk.  

   5. Skriv **\\\\<** <em>SMS-providerns dator</em> **> \root\sms\ Site_<** <em>platskod</em> **>** i **namn område**och klicka sedan på **Anslut**.  

   6. Klicka på **Öppna instans**, skriv **sms_bootimagepackage.packageID="<packageID\>"** och klicka sedan på **OK**. Som paket-ID anger du det värde som du identifierade i steg 3.  

   7. Klicka på **Uppdatera objekt** och sedan på **Aktivera LabShell** i rutan **Egenskaper**.  

   8. Klicka på **Redigera egenskap**, ändra värdet till **SANT**, och klicka på **Spara egenskap**.  

   9. Klicka på **Spara objekt**, och avsluta Testare för Windows Management Instrumentation.  

10. Du måste distribuera startavbildningen till distributionsplatser, till distributionsplatsgrupper eller till samlingar som är associerade till distributionsplatsgrupper, innan du kan använda startavbildningen i en aktivitetssekvens. Anpassa startavbildningen genom att utföra följande steg.  

    1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

    2.  I arbetsytan **Programbibliotek** expanderar du **Operativsystem** och klickar sedan på **Startavbildningar**.  

    3.  Klicka på den startavbildning som identifierades i steg 3.  

    4.  På fliken **Start** går du till gruppen **Distribution** och klickar på **Uppdatera distributionsplatser**.  
