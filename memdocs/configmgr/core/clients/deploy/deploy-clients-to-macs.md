---
title: Distribuera Mac-klienter
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar klienter till Mac-datorer i Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713445"
---
# <a name="how-to-deploy-clients-to-macs"></a>Distribuera klienter på Mac-datorer

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver hur du distribuerar och underhåller Configuration Manager-klienten på Mac-datorer. Information om vad du måste konfigurera innan du distribuerar klienter till Mac-datorer finns i [förbereda för distribution av klient program vara till Mac](prepare-to-deploy-mac-clients.md)-datorer.

När du installerar en ny klient för Mac-datorer kan du även behöva installera Configuration Manager uppdateringar för att avspegla den nya klient informationen i Configuration Manager-konsolen.

I de här procedurerna har du två alternativ för att installera klient certifikat. Läs mer om klient certifikat för Mac i [förbereda för att distribuera klient program vara till Mac](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Använd Configuration Manager-registrering med [verktyget CMEnroll](#bkmk_enroll). Registrerings processen har inte stöd för automatisk certifikat förnyelse. Omregistrera Mac-datorn innan det installerade certifikatet upphör att gälla.    

- [Använd en certifikatbegäran och en installations metod som är oberoende av Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Om du vill distribuera klienten till enheter som kör macOS Sierra, konfigurerar du på rätt sätt **ämnes namnet** för hanterings plats certifikatet. Använd till exempel FQDN för hanterings plats servern.



## <a name="configure-client-settings"></a>Konfigurera klientinställningar  

Använd [standard klient inställningarna](about-client-settings.md) om du vill konfigurera registrering för Mac-datorer. Du kan inte använda anpassade klient inställningar. För att begära och installera certifikatet kräver Configuration Manager-klienten för Mac Standard klient inställningarna.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Välj noden **klient inställningar** och välj sedan **standard klient inställningar**.  

2. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

3. Välj avsnittet **registrering** och konfigurera sedan följande inställningar:  

    1. **Tillåt att användare registrerar mobila enheter och Mac-datorer**: **Ja**  

    2. **Registrerings profil:** Välj **Ange profil**.  

4. I dialog rutan **registrerings profil för mobil enhet** väljer du **skapa**.  

5. I dialog rutan **skapa registrerings profil** anger du ett namn för den här registrerings profilen. Konfigurera sedan **hanterings plats koden**. Välj den Configuration Manager primära plats som innehåller hanterings platserna för dessa Mac-datorer.  

    > [!NOTE]  
    >  Om du inte kan välja platsen kontrollerar du att du konfigurerar minst en hanterings plats på platsen för att stödja mobila enheter.  

6. Välj **Lägg till**.  

7. I fönstret **Lägg till certifikat utfärdare för mobila enheter** väljer du den certifikat utfärdares server som utfärdar certifikat till Mac-datorer.  

8. I dialog rutan **skapa registrerings profil** väljer du den certifikatmall för Mac-datorn som du skapade tidigare.  

9. Välj **OK** för att stänga dialog rutan **registrerings profil** och sedan dialog rutan inställningar för **standard klient** .  

    > [!TIP]  
    > Om du vill ändra klient princip intervallet använder du **avsöknings intervall för klient princip** i klient inställnings gruppen klient **princip** .  

Nästa gången som enheterna laddar ned klient principen, Configuration Manager tillämpar dessa inställningar för alla användare. Information om hur du startar princip hämtning för en enskild klient finns i [Starta princip hämtning för en Configuration Manager-klient](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Förutom registrerings klient inställningarna kontrollerar du att du har konfigurerat följande klient enhets inställningar:  

- **Maskin varu inventering**: Aktivera och konfigurera den här funktionen om du vill samla in maskin varu inventering från Mac-och Windows-klientdatorer. Mer information finns i [så här utökar du maskin varu inventering](../manage/inventory/extend-hardware-inventory.md).  

- **Kompatibilitetsinställningar: Aktivera**och konfigurera den här funktionen om du vill utvärdera och reparera inställningar på Mac-och Windows-klientdatorer. Mer information finns i [Planera för och konfigurera kompatibilitetsinställningar](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

Mer information finns i [så här konfigurerar du klient inställningar](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a>Ladda ned klienten för macOS

1. Hämta macOS-klientens fil paket, [Microsoft Endpoint Configuration Manager-MacOS-klienten (64-bitars)](https://www.microsoft.com/download/details.aspx?id=100850). Spara **ConfigmgrMacClient. msi** på en dator som kör Windows. Den här filen finns inte på installations mediet för Configuration Manager.  

2. Kör installations programmet på Windows-datorn. Extrahera Mac-klientprogrammet, **Macclient. dmg**, till en mapp på den lokala disken. Standard Sök vägen är `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Kopiera filen **Macclient. dmg** till en mapp på Mac-datorn.  

4. På Mac-datorn kör du **Macclient. dmg** för att extrahera filerna till en mapp på den lokala disken.  

5. I mappen kontrollerar du att den innehåller följande filer: 

    - **CCMSetup**: installerar Configuration Manager-klienten på Mac-datorerna med **CMClient. pkg**  

    - **CMDiagnostics**: samlar in diagnostikinformation som är relaterade till Configuration Manager-klienten på Mac-datorerna  

    - **CMUninstall**: avinstallerar klienten från Mac-datorer  

    - **CMAppUtil**: konverterar Apple-programpaket till ett format som du kan distribuera som ett Configuration Manager program  

    - **CMEnroll**: begär och installerar klient certifikatet för en Mac-dator så att du sedan kan installera Configuration Manager-klienten  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a>Registrera Mac-klienten  

Registrera enskilda klienter med [guiden registrering av Mac-dator](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Om du vill automatisera registreringen för många klienter använder du [verktyget CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrera klienten med guiden registrering av Mac-dator  

1. När du har installerat-klienten öppnas guiden dator registrering. Om du vill starta guiden manuellt väljer du **Registrera** på sidan **Configuration Manager** inställningar.  

2. Ange följande information på den andra sidan i guiden:  

   - **Användar namn**: användar namnet kan ha följande format:  

     - `domain\name`. Exempelvis: `contoso\mnorth`  

     - `user@domain`. Exempelvis: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  När du använder en e-postadress för att fylla i fältet **användar namn** fyller Configuration Manager automatiskt i fältet **Server namn** . Den använder standard namnet på proxyservern för registrerings platsen och domän namnet för e-postadressen. Om namnen inte matchar namnet på proxyservern för registrerings platsen, korrigerar du **Server namnet** under registreringen.  

       Användar namnet och motsvarande lösen ord måste matcha ett Active Directory-användarkonto som har **Läs** -och **registrerings** behörigheter på Mac-klientens certifikatmall.  

   - **Server namn**: namnet på proxyservern för registrerings platsen.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Klient-och certifikat automatisering med CMEnroll  

Använd den här proceduren för att automatisera klient installationen och begära och registrera klient certifikat med verktyget CMEnroll. Om du vill köra verktyget måste du ha ett Active Directory användar konto.

1. På Mac-datorn navigerar du till den mapp där du extraherade innehållet i filen **Macclient. dmg** .  

2. Ange följande kommando:`sudo ./ccmsetup`  

3. Vänta tills meddelandet **Installationen har slutförts** visas. Även om installations programmet visar ett meddelande som du måste starta om nu, ska du inte starta om och fortsätta till nästa steg.  

4. I mappen **verktyg** på Mac-datorn skriver du följande kommando:`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    När klienten har installerats öppnas guiden Registrering av Mac-dator. Här får du hjälp att registrera Mac-datorn. Mer information finns i [Registrera klienten med hjälp av guiden registrering av Mac-dator](#bkmk_enroll).  

     Exempel: om proxyservern för registrerings platsen heter **server02.contoso.com**, och du beviljar **contoso\mnorth** -behörigheter för Mac-klientens certifikatmall, skriver du följande kommando:`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Om användar namnet innehåller något av följande tecken Miss lyckas registreringen: `<>"+=,`. Använd ett out-of-band-certifikat med ett användar namn som inte innehåller dessa tecken.  
    >  
    > Skript för installations stegen för en mer sömlös användar upplevelse. Användarna behöver sedan bara ange sitt användar namn och lösen ord.  

5. Ange lösen ordet för det Active Directory användar kontot. När du anger det här kommandot uppmanas du att ange två lösen ord. Det första lösen ordet är för superanvändarens konto för att köra kommandot. Den andra frågan avser Active Directory-användarkontot. Uppmaningarna ser identiska ut, så se till att du anger dem i korrekt ordning.  

6. Vänta tills meddelandet **Registreringen har genomförts** visas.  

7. Om du vill begränsa det registrerade certifikatet till Configuration Manager, öppnar du ett terminalfönster på Mac-datorn och gör följande ändringar:  

    1. Ange kommandot`sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Välj **system** **i avsnittet nyckel ringar i** fönstret **nyckel rings åtkomst** . Välj sedan **nycklar**i avsnittet **kategori** .  

    3. Expandera nycklarna om du vill visa klientcertifikaten. Hitta certifikatet med en privat nyckel som du har installerat och öppna nyckeln.  

    4. På fliken **Access Control** väljer du **Bekräfta innan du tillåter åtkomst**.  

    5. Bläddra till **/Library/Application Support/Microsoft/CCM**, Välj **ccmclient**och välj sedan **Lägg till**.  

    6. Välj **Spara ändringar** och Stäng dialog rutan **nyckel hanterare** .  

8. Starta om Mac-datorn.  

Kontrol lera att klient installationen har slutförts genom att öppna **Configuration Manager** objekt i **Systeminställningar** på Mac-datorn. Uppdatera och Visa även samlingen **alla system** i Configuration Manager-konsolen. Bekräfta att Mac-datorn visas i den här samlingen som en hanterad klient.  

> [!TIP]  
> Du kan felsöka Mac-klienten med hjälp av **CMDiagnostics** -verktyget som ingår i Mac-klientcertifikatet. Använd den för att samla in följande diagnostikinformation:  
>   
> - En lista med processer som körs  
> - Version av Mac OS X-operativsystemet  
> - Mac OS X krasch rapporter som är relaterade till Configuration Manager-klienten, inklusive **CCM\*. krasch** och **Systeminställningar. krasch**.  
> - STRUKTURLISTE-filen och egenskaps list filen (. plist) som skapats av Configuration Manager-klient installationen.  
> - Innehållet i mappen **/Library/Application Support/Microsoft/CCM/logs**.  
>   
> Informationen som samlas in av CmDiagnostics läggs till i en zip-fil som sparas på datorns skriv bord och har namnet`cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a>Hantera certifikat utanför Configuration Manager

Du kan använda en certifikatbegäran och en installations metod som är oberoende av Configuration Manager. Använd samma allmänna process, men inkludera följande ytterligare steg: 

- När du installerar Configuration Manager-klienten använder du kommando rads alternativen **MP** och **SubjectName** . Ange följande kommando: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Certifikatets ämnes namn är Skift läges känsligt, så skriv det exakt som det visas i certifikat informationen.  

     Exempel: hanterings platsens Internet-FQDN är **server03.contoso.com**. Mac-klientcertifikatet har FQDN för **mac12.contoso.com** som ett eget namn i certifikatets ämne. Använd följande kommando:`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Om du har fler än ett certifikat som innehåller samma ämnes värde anger du det serie nummer för certifikat som ska användas för den Configuration Manager klienten. Ange följande kommando: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Exempelvis: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Förnya Mac-klientcertifikatet  

Den här proceduren tar bort SMSID. Configuration Manager-klienten för Mac kräver ett nytt ID för att använda ett nytt eller förnyat certifikat.  

> [!IMPORTANT]  
> När du har ersatt-SMSID när du tar bort den gamla resursen i Configuration Manager-konsolen tar du även bort alla lagrade klient historik. Till exempel maskin varu inventerings historik för den klienten.  


1. Skapa och fyll i en enhets samling för de Mac-datorer som måste förnya dator certifikaten.  

2. I arbetsytan **Tillgångar och efterlevnad** startar du **guiden Skapa konfigurationsobjekt**.  

3. På sidan **Allmänt** i guiden anger du följande information:  

    - **Namn**: **ta bort SMSID för Mac**  

    - **Typ**: **Mac OS X**  

4. På sidan **plattformar som stöds** väljer du alla Mac OS X-versioner.  

5. På sidan **Inställningar** väljer du **Nytt**. I fönstret **Skapa inställning** anger du följande information:  

    - **Namn**: **ta bort SMSID för Mac**  

    - **Inställnings typ**: **skript**  

    - **Datatyp**: **sträng**  

6. I fönstret **Skapa inställning** , för **identifierings skript**, väljer du **Lägg till skript**. Den här åtgärden anger ett skript för att identifiera Mac-datorer som kon figurer ATS med en SMSID.  

7. I fönstret **Redigera identifierings skript** anger du följande kommando skript:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Stäng fönstret **Redigera identifierings skript** genom att klicka på **OK** .  

9. Välj **Lägg till skript**i fönstret **Skapa inställning** för **reparations skript (valfritt)**. Den här åtgärden anger ett skript som tar bort SMSID när det hittas på Mac-datorer.  

10. I fönstret **skapa reparations skript** anger du följande kommando skript:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Stäng fönstret **skapa reparations skript** genom att klicka på **OK** .  

12. På sidan **regler för efterlevnad** väljer du **nytt**. Ange följande information i fönstret **Skapa regel** :  

    - **Namn**: **ta bort SMSID för Mac**  

    - **Vald inställning**: Välj **Bläddra** och välj det identifierings skript som du angav tidigare.  

    - I **följande värde** fält: **domän/default-paret (com. Microsoft. ccmclient, SMSID) finns inte**.  

    - Aktivera alternativet att **köra det angivna reparations skriptet när den här inställningen är inkompatibel**.  

13. Slutför guiden.  

14. Skapa en konfigurations bas linje som innehåller detta konfigurations objekt. Distribuera bas linjen till mål samlingen.  

     Mer information finns i [så här skapar du konfigurations bas linjer](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. När du har installerat ett nytt certifikat på Mac-datorer där SMSID har tagits bort kör du följande kommando för att konfigurera klienten att använda det nya certifikatet:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Se även

[Förbered att distribuera klienter på Mac-datorer](prepare-to-deploy-mac-clients.md)

[Underhåll Mac-klienter](../manage/maintain-mac-clients.md)
