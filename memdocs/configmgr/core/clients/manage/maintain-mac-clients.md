---
title: Underhåll Mac-klienter
titleSuffix: Configuration Manager
description: Underhålls aktiviteter för Configuration Manager Mac-klienter.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710652"
---
# <a name="maintain-mac-clients"></a>Underhåll Mac-klienter
*Gäller för: Configuration Manager (aktuell gren)*

Här är procedurer för att avinstallera Mac-klienter och för att förnya sina certifikat.

##  <a name="uninstalling-the-mac-client"></a> Uninstalling the Mac client  

1.  På en Mac-dator öppnar du ett terminalfönster och navigerar till mappen som innehåller **Macclient. dmg**.  

2.  Navigera till mappen Verktyg och ange följande kommandorad:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  Egenskapen **-c** instruerar klient avinstallationen att även ta bort klient krasch loggar och loggfiler. Vi rekommenderar detta för att undvika förvirring om du senare installerar om klienten.  

3.  Om det behövs tar du bort det certifikat för klientautentisering som Configuration Manager använde eller återkallar det. CMUnistall tar inte bort/återkallar inte det här certifikatet.  

##  <a name="renewing-the-mac-client-certificate"></a>Förnya Mac-klientcertifikatet  
 Om du vill förnya Mac-klientcertifikatet kan du använda någon av följande metoder.  

-   [Guiden Förnya certifikat](#renew-certificate-wizard)  

-   [Förnya certifikat manuellt](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Guiden Förnya certifikat  

1. Konfigurera följande värden som *strängar* i filen ccmclient. plist som styr när guiden Förnya certifikat öppnas:  

   - **RenewalPeriod1** – anger den första förnyelse period i sekunder som användare kan förnya certifikatet. Standardvärdet är 3 888 000 sekunder (45 dagar). Konfigurera inte ett värde som är mindre än 300, eftersom perioden återgår till standardvärdet. 

   - **RenewalPeriod2** – anger den andra förnyelse period i sekunder som användare kan förnya certifikatet. Standardvärdet är 259 200 sekunder (3 dagar). Om det här värdet har kon figurer ATS och är större än eller lika med 300 sekunder och är mindre än eller lika med **RenewalPeriod1**, används värdet. Om **RenewalPeriod1** är högre än tre dagar används ett värde på tre dagar för **RenewalPeriod2**.  Om **RenewalPeriod1** är lägre än tre dagar ställs **RenewalPeriod2** in på samma värde som **RenewalPeriod1**.  

   - **RenewalReminderInterval1** – anger i sekunder hur ofta guiden Förnya certifikat ska visas för användare under den första förnyelse perioden. Standardvärdet är 86 400 sekunder (1 dag). Om **RenewalReminderInterval1** är högre än 300 sekunder och lägre än det värde som har konfigurerats för **RenewalPeriod1**används det konfigurerade värdet. I annat fall används standardvärdet på 1 dag.  

   - **RenewalReminderInterval2** – anger i sekunder hur ofta guiden Förnya certifikat ska visas för användare under den andra förnyelse perioden. Standardvärdet är 28 800 sekunder (8 timmar). Om **RenewalReminderInterval2** är högre än 300 sekunder, lägre än eller lika med **RenewalReminderInterval1** och lägre än eller lika med **RenewalPeriod2**, används det konfigurerade värdet. Annars används ett värde på 8 timmar.  

     **Exempel:** Om värdena lämnas som standardvärden öppnas guiden var 24:e timme i 45 dagar innan certifikatet upphör att gälla.  Inom 3 dagar från det att certifikatet upphör att gälla öppnas guiden var 8:e timme.  

     **Exempel:** Använd följande kommandorad, eller ett skript, för att ställa in den första förnyelseperioden på 20 dagar.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. När guiden Förnya certifikat öppnas kommer fälten **användar namn** och **Server namn** normalt att fyllas i och användaren kan bara ange ett lösen ord för att förnya certifikatet.  

   > [!NOTE]  
   >  Om guiden inte öppnas, eller om du råkar stänga guiden av misstag, klickar du på **Förnya** från inställningssidan till **Configuration Manager** för att öppna guiden.  

###  <a name="renew-certificate-manually"></a>Förnya certifikat manuellt  
 En typisk giltighetsperiod för Mac-klientcertifikatet är ett år. Configuration Manager förnyar inte automatiskt det användar certifikat som det begär under registreringen, så du måste använda följande procedur för att förnya certifikatet manuellt.  

> [!IMPORTANT]  
>  Om certifikatet upphör att gälla måste du avinstallera, installera om och sedan omregistrera Mac-klienten.  

 Den här proceduren tar bort SMSID, vilket krävs för att begära ett nytt certifikat för samma Mac-dator. När du tar bort och ersätter klientens SMSID tas alla lagrade klient historik, till exempel lager, bort när du tar bort klienten från Configuration Manager-konsolen.  

1.  Skapa och fyll i en enhets samling för de Mac-datorer som måste förnya användar certifikaten.  

    > [!WARNING]  
    >  Configuration Manager övervakar inte giltighets perioden för det certifikat som det registrerar för Mac-datorer. Du måste övervaka detta oberoende av Configuration Manager för att identifiera de Mac-datorer som ska läggas till i den här samlingen.  

2.  I arbetsytan **Tillgångar och efterlevnad** startar du **guiden Skapa konfigurationsobjekt**.  

3.  På sidan **Allmänt** anger du följande information:  

    -   **Namn:Ta bort SMSID för Mac**  

    -   **Typ:Mac OS X**  

4.  På sidan **plattformar som stöds** ser du till att alla Mac OS X-versioner är markerade.  

5.  På sidan **Inställningar** väljer du **nytt** och anger följande information i dialog rutan **Skapa inställning** :  

    -   **Namn:Ta bort SMSID för Mac**  

    -   **Inställningstyp:Skript**  

    -   **Datatyp:Sträng**  

6.  I dialog rutan **Skapa inställning** för **identifierings skript**väljer du **Lägg till skript** för att ange ett skript som identifierar Mac-datorer med en SMSID konfigurerad.  

7.  I dialogrutan **Redigera identifieringsskript** anger du följande kommandoskript:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Klicka på **OK** för att stänga dialog rutan **Redigera identifierings skript** .  

9. I dialog rutan **Skapa inställning** för **reparations skript (valfritt)** väljer du **Lägg till skript** för att ange ett skript som tar bort SMSID när det hittas på Mac-datorer.  

10. I dialogrutan **Skapa reparationsskript** anger du följande kommandoskript:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Klicka på **OK** för att stänga dialog rutan **skapa reparations skript** .  

12. På sidan **Kompatibilitetsregler** i guiden klickar du på **Nytt**och sedan anger du följande information i dialogrutan **Skapa regel** :  

    -   **Namn:Ta bort SMSID för Mac**  

    -   **Vald inställning:** Välj **Bläddra** och välj det identifierings skript som du angav tidigare.  

    -   I fältet **följande värden** anger du **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Aktivera alternativet **Kör det angivna reparationsskriptet när den här inställningen är inkompatibel**.  

13. Slutför guiden Skapa konfigurationsobjekt  

14. Skapa en konfigurations bas linje som innehåller konfigurationsobjektet som du precis har skapat och distribuera den till enhets samlingen som du skapade i steg 1.  

     Mer information om hur du skapar och distribuerar konfigurations bas linjer finns i [så här skapar du konfigurations bas linjer](../../../compliance/deploy-use/create-configuration-baselines.md) och [hur du distribuerar konfigurations bas linjer](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. På de Mac-datorer där SMSID har tagits bort kör du följande kommando om du vill installera ett nytt certifikat:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     När du uppmanas till det uppger du lösenordet till det överordnande användarkontot för att köra kommandot och sedan lösenordet till Active Directory-användarkontot.  

16. Om du vill begränsa det registrerade certifikatet till Configuration Manager, öppnar du ett terminalfönster på Mac-datorn och gör följande ändringar:  

    a.  Ange kommandot`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  I dialog rutan **nyckel hanterare** , i avsnittet nyckel **ringar** , väljer du **system**och väljer sedan **nycklar**i avsnittet **kategori** .  

    c.  Expandera nycklarna om du vill visa klientcertifikaten. När du har identifierat certifikatet med en privat nyckel som du just har installerat, dubbelklickar du på nyckeln.  

    d.  På fliken **Access Control** väljer du **Bekräfta innan du tillåter åtkomst**.  

    e.  Bläddra till **/Library/Application Support/Microsoft/CCM**, Välj **ccmclient**och välj sedan **Lägg till**.  

    f.  Välj **Spara ändringar** och Stäng dialog rutan **nyckel hanterare** .  

17. Starta om Mac-datorn.  

