---
title: Konfigurera sidan för registreringsstatus
titleSuffix: Microsoft Intune
description: Konfigurera en hälsningssida för användare som registrerar Windows 10-enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f8991b772f5562538403492735f1f4c2fdc87e8
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093451"
---
# <a name="set-up-the-enrollment-status-page"></a>Konfigurera sidan för registreringsstatus
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
På sidan för registreringsstatus visas etableringsförloppet när en ny enhet har registrerats, samt när nya användare loggar in på enheten.  Det här gör att IT-administratörer kan förhindra (blockera) åtkomst till enheten tills den har etablerats fullständigt, samtidigt som användarna får information om de uppgifter som återstår under etableringsprocessen.

Sidan för registreringsstatus kan användas i etableringsscenarier i [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/) och kan även användas separat från Windows Autopilot inom ramen för standardmiljön i Azure AD Join, samt för alla nya användare som loggar in på enheten första gången.

Du kan skapa flera profiler för sidan för registreringsstatus med olika konfigurationer du anger:

- Visar installationsförloppet
- Blockerar åtkomst tills etableringsprocessen har slutförts
- Tidsgränser
- Tillåtna felsökningsåtgärder

De här profilerna anges i prioritetsordning där den högsta tillämpliga prioritetsnivån används.  Varje sådan profil kan riktas mot grupper som innehåller enheter eller användare.  När du bestämmer vilken profil som ska användas följs följande villkor:

- Profilen med den högsta prioriteten som är riktad mot enheten används först.
- Om det inte finns några profiler riktade mot enheten används profilen med den högsta prioriteten som är riktad mot den aktuella användaren.  (Det här gäller bara i scenarier där det finns en användare. I assisterade och självdistribuerade scenarier kan du endast använda riktade enheter.)
- Om det inte finns några profiler riktade mot specifika grupper används standardprofilen för sidan för registreringsstatus.

## <a name="available-settings"></a>Tillgängliga inställningar

Följande inställningar kan konfigureras för att anpassa beteendet för sidan för registreringsstatus:

<table>
<th align="left">Inställningen<th align="left">Ja<th align="left">Nej
<tr><td>Visa installationsförlopp för appar och profiler<td>Registreringsstatussidan visas.<td>Registreringsstatussidan visas inte.
<tr><td>Blockera enhetsanvändning tills alla appar och profiler är installerade<td>Inställningarna i den här tabellen görs tillgängliga för att anpassa beteendet för sidan registreringsstatus, så att användaren kan åtgärda eventuella installationsproblem.
<td>Sidan registreringsstatus visas utan ytterligare alternativ för att lösa installationsproblem.
<tr><td>Tillåt användare att återställa enheten om installationsfel uppstår<td>Knappen <b>Återställ enheten</b> visas om installationsfel uppstår.<td>Knappen <b>Återställ enheten</b> visas inte om installationsfel uppstår.
<tr><td>Tillåt användare att återställa enheten om installationsfel uppstår<td>Knappen <b>Fortsätt ändå</b> visas om ett installationsfel uppstår.<td>Knappen <b>Fortsätt ändå</b> visas inte om ett installationsfel uppstår.
<tr><td>Visa tidsgränsfel när installationen tar längre tid än det angivna antalet minuter<td colspan="2">Ange antalet minuter som ska förflyta innan installationen slutförs. Ett standardvärde på 60 minuter har angetts.
<tr><td>Visa anpassat meddelande när ett fel uppstår<td>En textruta finns där du kan ange ett anpassat meddelande som ska visas om ett installationsfel inträffar.<td>Standardmeddelandet visas: <br><b>Installationen överskred den angivna tidsgränsen för din organisation. Försök igen eller kontakta din IT-support om du behöver hjälp.<b>
<tr><td>Tillåt användare att samla in loggar om installationsfel<td>Om det finns ett installationsfel visas knappen <b>Samla in loggar</b>. <br>Om användaren klickar på den här knappen uppmanas de att välja en plats där loggfilen ska sparas <b>MDMDiagReport.cab</b><td>Knappen <b>Samla in loggar</b> visas inte om installationsfel uppstår.
<tr><td>Blockera enhetsanvändning tills följande obligatoriska appar har installerats, om de är tilldelade till användaren/enheten<td colspan="2">Välj <b>Alla</b> eller <b>Valda</b>. <br><br>Om <b>Selected</b> väljs visas en knappen <b>Välj appar</b> som låter dig välja vilka appar som måste installeras innan enheten aktiveras.
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>Aktivera standardsidan för registreringsstatus för alla användare

Följ stegen nedan om du vill aktivera sidan för registreringsstatus.
 
1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Windows** > **Windows-registrering** > **Sidan för registreringsstatus**.
2. På bladet **Statussidan för registrering**  väljer du **Standard** > **Inställningar**.
3. Välj **Ja** för **Show app and profile installation progress** (Visa installationsförlopp för appar och profiler).
4. Välj övriga inställningar som du vill aktivera och välj sedan **Spara**.

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>Skapa en profil för registreringsstatussidan och tilldela den till en grupp

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Windows** > **Windows-registrering** > **Sidan för registreringsstatus** > **Skapa profil**.
2. Ange ett **namn** och en **beskrivning**.
3. Välj **Skapa**.
4. Välj den nya profilen i listan **Statussidan för registrering**.
5. Välj **Tilldelningar** > **Välj grupper** > välj de grupper som ska använda den här profilen > **Välj** > **Spara**.
6. Välj **Inställningar** > välj de inställningar som du vill använda för den här profilen > **Spara**.

## <a name="set-the-enrollment-status-page-priority"></a>Ange prioritet för registreringsstatussidan

En enhet eller användare kan tillhöra flera grupper och ha flera riktade profiler för registreringsstatussidan. Om du vill kontrollera vilka profiler som används först kan du ställa in prioriteten för varje profil. De med högre prioritet används först.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Windows** > **Windows-registrering** > **Sidan för registreringsstatus**.
2. Hovra över profilen i listan.
3. Använd de tre lodräta punkterna och dra profilen till önskad plats i listan.

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>Blockera åtkomst till en enhet tills ett visst program har installerats

Du kan ange vilka appar som måste installeras innan sidan för registreringsstatus anses slutförd.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Windows** > **Windows-registrering** > **Sidan för registreringsstatus**.
2. Välj en profil > **Inställningar**.
3. Välj **Ja** för **Show app and profile installation progress** (Visa installationsförlopp för appar och profiler).
4. Välj **Ja** för **Block device use until all apps and profiles are installed** (Blockera enhetsanvändning tills alla appar och profiler är installerade).
5. Välj **Valda** för **Blockera enhetsanvändning tills följande obligatoriska appar har installerats, om de är tilldelade till användaren/enheten**.
6. Välj **Välj appar** > välj apparna > **Välj** > **Spara**.

De appar som ingår i den här listan används av Intune för att filtrera listan som bör betraktas som blockerande.  Den anger inte vilka appar som ska installeras.  Om du till exempel konfigurerar den här listan så att den inkluderar ”app 1”, ”app 2” och ”app 3”, och ”app 3” och ”app 4” är riktade till enheten eller användaren, kommer sidan för registreringsstatus endast att spåra ”app 3”.  ”App 4” kommer fortfarande att installeras, men sidan för registreringsstatus kommer inte att vänta på att den ska slutföras.

Du kan ange högst 100 appar.

## <a name="enrollment-status-page-tracking-information"></a>Spårningsinformation på statussidan för registrering

Det finns tre faser där statussidan spårar information: enhetsförberedelse, enhetskonfiguration och kontokonfiguration.

### <a name="device-preparation"></a>Förberedelse av enheten

När det gäller enhetsförberedelse spårar registreringsstatussidan:

- Trusted Platform Module-nyckelattestering (TPM) (i förekommande fall)
- Anslutningsprocess för Azure Active Directory
- Intune-registrering (MDM)
- Installation av Intune Management-tillägg (används till att installera Win32-appar)

### <a name="device-setup"></a>Enhetskonfiguration

På sidan för registreringsstatus spåras följande installationsobjekt på enheten:

- Säkerhetsprinciper
  - En konfigurationstjänstprovider (CSP) för alla registreringar.
  - De faktiska konfigurationstjänstprovidrar som har konfigurerats av Intune spåras inte här.
- Program
  - Verksamhetskritiska (LoB) MSI-appar per dator.
  - LoB-lagringsappar med installationskontext = Enhet.
  - Offlinelagrings- och LoB-lagringsappar med installationskontext = Enhet.
  - Win32-program (endast Windows 10 version 1903 och senare) 
- Anslutningsprofiler
  - VPN- eller Wi-Fi-profiler som har tilldelats **Alla enheter** eller en enhetsgrupp som enheten som registreras är medlem i, men endast för Autopilot-enheter
- Certifikatprofiler som har tilldelats **Alla enheter** eller en enhetsgrupp som enheten som registreras är medlem i, men endast för Autopilot-enheter

### <a name="account-setup"></a>Kontokonfiguration

För kontokonfiguration spårar statussidan för registrering följande objekt om de har tilldelats till den aktuella användaren:

- Säkerhetsprinciper
  - En konfigurationstjänstprovider (CSP) för alla registreringar.
  - De faktiska konfigurationstjänstprovidrar som har konfigurerats av Intune spåras inte här.
- Program
  - Verksamhetsspecifika MSI-appar per användare som har tilldelats till alla enheter, till alla användare eller till en användargrupp som användaren som registrerar enheten är medlem i.
  - Verksamhetsspecifika MSI-appar per dator som har tilldelats till alla användare eller till en användargrupp som användaren som registrerar enheten är medlem i.
  - Verksamhetsspecifika butiksappar, appar i onlinebutiken och appar i offlinebutiken som tilldelas något av följande objekt:
    - Alla enheter
    - Alla användare
    - En användargrupp där användaren som registrerar enheten är en medlem med installationskontexten Användare.
  - Win32-program (endast Windows 10 version 1903 och senare) 
- Anslutningsprofiler
  - VPN- eller Wi-Fi-profiler som har tilldelats till alla användare eller till en användargrupp som användaren som registrerar enheten är medlem i.
- Certifikat
  - Certifikatprofiler som har tilldelats till alla användare eller till en användargrupp som användaren som registrerar enheten är medlem i.

### <a name="troubleshooting"></a>Felsökning

Här följer några vanliga frågor om felsökning av problem som rör sidan för registreringsstatus.

- Varför har mina program inte installerats och spårats på sidan för registreringsstatus?
  - För att garantera att program installeras och spåras på sidan för registreringsstatus ska du kontrollera att:
      - Apparna är kopplade till en Azure AD-grupp som innehåller enheten (för enhetsinriktade appar) eller användaren (för användarinriktade appar) med hjälp av en ”obligatorisk” tilldelning.  (Enhetsinriktade appar spåras under enhetsfasen av ESP, medan användarinriktade appar spåras under användarfasen av ESP.)
      - Du anger antingen **Blockera enhetsanvändning tills alla appar och profiler är installerade** eller så tar du med appen i listan **Blockera enhetsanvändning tills de nödvändiga apparna är installerade**.
      - Apparna installeras i enhetskontexten och tillämpar inga regler för användarkontexten.

- Varför visas sidan registreringsstatus för distributioner som inte gäller autopilot, till exempel när en användare loggar in för första gången på en registrerad enhet för Configuration Manager-medhantering?  
  - Registreringsstatussidan visar installationsstatus för alla registreringsmetoder, inklusive
      - Autopilot
      - Medhantering med Configuration Manager
      - När en ny användare loggar in på enheten som har tillämpat principen för registreringsstatussidan för första gången
      - n inställningen **Visa endast sidan för enheter som tillhandahålls av OOBE (out-of-box experience)** är aktiverad och principen har ställts in, kommer bara den första användaren som loggar in på enheten att se sidan med registreringsstatus

- Hur kan jag inaktivera registreringsstatussidan om den har konfigurerats på enheten?
  - Registreringsstatussidans princip konfigureras på en enhet när den registreras. Om du vill inaktivera registreringsstatussidan måste du inaktivera områdena användare och status på registreringsstatussidan. Du inaktiverar avsnitten genom att skapa anpassade OMA-URI-inställningar med följande konfigurationer.

      Avaktivera användarregistreringsstatussidan:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Avaktivera enhetsregistreringsstatussidan:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- Hur kan jag samla in loggfiler?
  - Det finns två sätt som loggfiler för registreringsstatussidan kan samlas in på:
      - Ge användarna möjlighet att samla in loggar i ESP-principen. När ett avbrott sker på registreringsstatussidan kan slutanvändaren välja alternativet att **Samla in loggar**. Genom att sätta in en USB-enhet kan loggfilerna kopieras till enheten
      - Öppna en kommandotolk genom att trycka på shift-F10 och ange följande kommandorad för att generera loggfilerna: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>Kända problem

Här följer några kända problem som rör sidan för registreringsstatus.

- Om du inaktiverar ESP-profilen tas inte ESP-principen bort från enheterna och användarna får fortfarande ESP när de loggar in på enheten för första gången. Principen tas inte bort när ESP-profilen är inaktiverad. Du måste distribuera OMA-URI för att inaktivera ESP. Se ovan för instruktioner om hur du inaktiverar ESP med OMA-URI. 
- En omstart under enhetsinstallationen tvingar användaren att ange sina autentiseringsuppgifter innan de övergår till installationsfasen för kontot. Användarautentiseringsuppgifter bevaras inte under omstarten. Låt användaren ange sina autentiseringsuppgifter. Därefter kan registreringsstatussidan fortsätta. 
- Registreringsstatussidan kommer alltid att göra ett avbrott under en registrering av arbets- eller skolkonto på enheter med versioner av Windows 10 som är äldre än 1903. Registreringsstatussidan väntar på att Azure AD-registreringen ska slutföras. Problemet åtgärdas i Windows 10-version 1903 och senare.  
- Hybrid Azure AD-autopilotdistribution med ESP tar längre tid än det avbrott som har definierats i ESP-profilen. I hybriddistributioner av Azure AD-autopilot tar ESP 40 minuter längre än värdet som anges i ESP-profilen. Den här fördröjningen låter det lokala AD-anslutningsprogrammet skapa den nya enhetsposten i Azure AD. 
- Inloggningssidan för Windows är inte ifylld med användarnamnet i användardrivet Autopilot-läge. Om en omstart sker under enhetskonfigurationsfasen i ESP:
  - bevaras inte användarautentiseringsuppgifterna
  - måste användaren ange autentiseringsuppgifterna igen innan de fortsätter från enhetsinstallationsfasen till kontoinstallationsfasen
- ESP har fastnat under en längre tid eller så slutförs aldrig fasen "Identifierar". Intune beräknar ESP-principerna under identifieringsfasen. En enhet kan kanske inte slutföra beräkningen av ESP-principerna om den aktuella användaren inte har en tilldelad Intune-licens.  
- Om du konfigurerar Windows Defender-programreglering kan du bli ombedd att starta om under Autopilot. Konfigurering av Microsoft Defender-programmet (AppLocker CSP) kräver en omstart. När den här principen har konfigurerats kan det leda till att en enhet startas om under autopilot. För närvarande finns det inget sätt att utelämna eller skjuta upp omstarten.
- När DeviceLock-principen (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) är aktiverad som en del av en ESP-profil kan fel på automatisk inloggning med användarskrivbord eller OOBE uppstå oväntat av två orsaker.
  - Om enheten inte har startats om innan du avbröt installationsfasen för ESP-enheten kan användaren uppmanas att ange sina autentiseringsuppgifter för Azure AD. Det här meddelandet visas i stället för en lyckad automatisk inloggning där användaren ser en animation för första inloggningen på Windows.
  - Automatisk inloggning kommer att misslyckas om enheten startades om efter att användaren angav sina inloggningsuppgifter för Azure AD men innan ESP-enhetens konfigurationsfas avslutades. Felet uppstår eftersom ESP-konfigurationsfasen inte slutfördes. Lösningen är att återställa enheten.

## <a name="next-steps"></a>Nästa steg

När du har konfigurerat Windows-registreringssidor kan du gå vidare och lära dig hur du hanterar Windows-enheter. Mer information finns i [Vad är Microsoft Intune-enhetshantering?](../remote-actions/device-management.md)
