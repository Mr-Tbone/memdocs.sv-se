---
title: Windows Autopilot för befintliga enheter
titleSuffix: Configuration Manager
description: Använda en Configuration Manager aktivitetssekvens för att återställa avbildningen och etablera en Windows 7-enhet för Windows autopilot-användarläge
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724211"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot för befintliga enheter
<!--3607717, fka 1358333-->

*Gäller för: Configuration Manager (aktuell gren)*

[Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) gör det möjligt för organisationer att leverera nya, oskyddade Windows 10-enheter direkt till slutanvändaren och definiera det etablerings flöde som användaren går igenom för att få en säker, produktiv Windows 10-enhet. Enheten har registrerats med Windows autopilot-tjänsten, så du kan tilldela den nödvändiga Windows autopilot-profilen. Den här profilen definierar OOBE (out-of-Box Experience) för enheten. 

[Windows autopilot för befintliga enheter](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) finns i Windows 10, version 1809 eller senare. Med den här funktionen kan du återställa avbildningen och etablera en Windows 7-enhet för [Windows autopilot-](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) användarläge med hjälp av en enda, inbyggd Configuration Manager-aktivitetssekvens. 



## <a name="prerequisites"></a>Krav

- Hämta installations mediet för Windows 10 version 1809 eller senare. Skapa sedan en Configuration Manager OS-avbildning. Mer information finns i [hantera OS-avbildningar](../get-started/manage-operating-system-images.md).

- Skapa profiler för Windows autopilot i Microsoft Intune. Mer information finns i [registrera Windows-enheter i Intune med hjälp av Windows autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- En enhet som inte redan har registrerats med Windows autopilot-tjänsten. Om enheten redan har registrerats har den tilldelade profilen företräde. Den autopiloten för profilen för befintliga enheter gäller endast om profilen för online-profilen har uppnåtts.



## <a name="create-the-configuration-file"></a>Skapa konfigurations filen

1. Öppna ett administrativt PowerShell kommando fönster på en Windows-enhet med Internet anslutning och kör följande kommandon:  

    1. Installera nödvändiga moduler och acceptera prompter för att fortsätta  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Logga in på Intune med administratörsautentiseringsuppgifter  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Hämta alla Windows autopilot-profiler som är kopplade till din Intune-klient  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Skapa en konfigurations fil för varje profil. Filerna namnges efter visnings namnet på profilen och sparas på den aktuella användarens skriv bord.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Konfigurations filen får bara innehålla en profil. Varje profil ska ligga inom klammerparenteser `{}`.  

2. Spara en av profilerna till en ANSI-kodad fil med namnet **AutopilotConfigurationFile. JSON**. Spara den på en plats som är lämplig för en Configuration Manager paket källa.  

    > [!Tip]  
    > Om du använder PowerShell-cmdleten **Out-File** för att omdirigera JSON-utdata till en fil använder den Unicode-kodning som standard. Den här cmdleten kan också trunkera långa rader. Använd cmdleten **set-Content** med `-Encoding ASCII` parametern för att ange rätt text kodning.   
    > 
    > Windows Anteckningar använder ANSI-kodning som standard.  

3. Skapa ett Configuration Manager-paket som innehåller den här filen. Det krävs inget program. Mer information finns i [skapa ett paket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Windows kräver att filen heter **AutopilotConfigurationFile. JSON**. Om du vill använda mer än en autopilot-profil skapar du separata Configuration Manager-paket.  



## <a name="create-the-task-sequence"></a>Skapa aktivitetssekvensen

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** . Välj **skapa aktivitetssekvens** i menyfliksområdet.  

2. På sidan **Skapa ny aktivitetssekvens** väljer du alternativet för att **distribuera Windows autopilot för befintliga enheter**.  

3. På sidan **information om aktivitetssekvens** anger du ett namn, eventuellt lägger till en beskrivning och väljer en start avbildning. Mer information om versioner som stöds för start avbildningar finns i [stöd för Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. På sidan **Installera Windows** väljer du Windows 10- **avbildnings paketet**. Konfigurera sedan följande inställningar:  

    - **Avbildnings index**: Välj antingen Enterprise, Education eller Professional, enligt vad som krävs av din organisation  

    - Aktivera alternativet för att **partitionera och formatera mål datorn innan du installerar operativ systemet**  

    - **Konfigurera aktivitetssekvens som ska användas med BitLocker**: om du aktiverar det här alternativet innehåller aktivitetssekvensen de steg som krävs för att aktivera BitLocker  

    - **Produkt nyckel**: om du behöver ange en produkt nyckel för Windows-aktivering anger du den här  

    - Välj ett av följande alternativ för att konfigurera det lokala administratörs kontot i Windows 10:  
        - **Generera slumpmässigt lösen ord för den lokala administratören och inaktivera kontot på alla support plattformar (rekommenderas)**
        - **Aktivera kontot och ange lösenord för den lokala administratören**

5. På sidan **Konfigurera nätverk** väljer du alternativet för att **ansluta till en arbets grupp**. I den här aktivitetssekvensen används Windows system förberedelse verktyget (Sysprep). Om enheten är ansluten till en domän, Miss lyckas Sysprep.  

6. På sidan **installera Configuration Manager** lägger du till nödvändiga installations egenskaper för din miljö.  

    > [!Tip]  
    > Aktivitetssekvensen behöver bara den här informationen om Configuration Manager klient komponenterna behövs under aktivitetssekvensen innan Sysprep körs. Till exempel för att installera program uppdateringar eller program. Om du inte utför dessa åtgärder behövs inte klienten. Den avinstalleras innan aktivitetssekvensen kör Sysprep.  

7. Sidan **Inkludera uppdateringar** väljer som standard alternativet att **inte installera några program uppdateringar**.  

    > [!Tip]  
    > Använd underhåll av offline-avbildning för att hålla avbildningen uppdaterad med de senaste kvalitets uppdateringarna för Windows 10. Mer information finns i [tillämpa program uppdateringar på en operativ system avbildning](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. På sidan **installera program** kan du välja vilka program som ska installeras under aktivitetssekvensen. Microsoft rekommenderar dock att du speglar avbildnings metoden för signaturen med det här scenariot. Använd alla program och konfigurationer från Microsoft Intune eller Configuration Manager samhantering när enheten etablerar med autopilot. Den här processen ger en konsekvent upplevelse mellan användare som tar emot nya enheter och de som använder Windows autopilot för befintliga enheter.  

8. På sidan **system förberedelse** väljer du det paket som innehåller konfigurations filen för autopilot. Som standard startar aktivitetssekvensen om datorn när den har kört Windows Sysprep. Du kan också välja alternativet att **stänga av datorn när aktivitetssekvensen har slutförts**. Med det här alternativet kan du förbereda en enhet och sedan leverera den till en användare för en konsekvent autopilot-upplevelse.  

9. Slutför guiden.  

Om du redigerar aktivitetssekvensen är det liknande som Standardaktivitetssekvensen för att tillämpa en befintlig operativ system avbildning. Den här aktivitetssekvensen innehåller följande ytterligare steg:  

- **Använd Windows autopilot-konfiguration**: det här steget tillämpar konfigurations filen för autopilot från det angivna paketet. Det är inte en ny typ av steg, det är ett **Kör kommando rads** steg för att kopiera filen.  

- **Förbereda Windows för avbildning**: det här steget kör Windows Sysprep och har inställningen att **stänga av datorn när åtgärden har körts**. Mer information finns i [förbereda Windows för avbildning](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

Aktivitetssekvensen Windows autopilot för befintliga enheter resulterar i en enhet som är ansluten till Azure Active Directory (Azure AD). 

> [!NOTE]  
> Med Windows 10 version 1903 och version 1909 har autopilot ett känt problem där Sysprep tar bort filen **AutopilotConfigurationFile. JSON** . Om du använder den här metoden för att distribuera Windows 10 version 1903 eller version 1909 redigerar du den här aktivitetssekvensen och gör följande ändringar:
>
> 1. Inaktivera steget **Förbered Windows för avbildning** .
> 2. När du har inaktiverat steget **Förbered Windows för avbildning** lägger du till ett nytt **kommando rads** steg för körning. Konfigurera den för att köra följande kommando rad:`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Mer information finns i [Windows autopilot – kända problem](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Använd OneDrive för företag- [känd mapp Flytta](https://docs.microsoft.com/onedrive/redirect-known-folders) för att se till att användarens data säkerhets kopie ras före uppgraderingen av Windows 10.



## <a name="next-steps"></a>Nästa steg

Använd Co-Management för att förbättra hanterings funktionerna för dina Windows 10-enheter. Den andra sökvägen till samhantering är genom modern etablering med Windows autopilot. Mer information finns i följande artiklar:

- [Vad är samhantering?](../../comanage/overview.md)
- [Sökvägar till samhantering](../../comanage/quickstart-paths.md)
- [Windows Autopilot med samhantering](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Se även

- [Registrera Windows-enheter i Intune med hjälp av Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)
