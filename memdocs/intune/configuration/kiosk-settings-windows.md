---
title: Kioskinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera dina enheter som kör Windows 10 (eller senare) med helskärmsläget för en app eller flera appar, anpassa startmenyn, lägg till appar, visa aktivitetsfältet och konfigurera en webbläsare i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae89a939e35f68f55d2e63e7495a9b743cc0fa34
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791771"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Inställningar för enheter med Windows 10 (och senare) som ska köras med helskärmsläge i Intune

På enheter som kör Windows 10 (och senare) kan du konfigurera att enheterna körs i helskärmsläge för en enskild app eller helskärmsläge för flera appar.

Den här artikeln beskriver de olika inställningar som du kan styra på enheter med Windows 10 och senare. I din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar till att konfigurera att dina enheter med Windows 10 (och senare) körs i helskärmsläge.

Som Intune-administratör kan du skapa och tilldela dessa inställningar till dina enheter.

Mer information om Windows helskärmsfunktion i Intune finns i [Konfigurera inställningar för helskärmsläge](kiosk-settings.md).

## <a name="before-you-begin"></a>Innan du börjar

- [Skapa profilen](kiosk-settings.md#create-the-profile).

- Den här helskärmsprofilen är direkt kopplad till den profil för enhetsbegränsningar som du skapar med [Microsoft Edge-helskärmsinställningarna](device-restrictions-windows-10.md#microsoft-edge-browser). Sammanfattningsvis:

  1. Skapa den här helskärmsprofilen för att köra enheten i helskärmsläge.
  2. Skapa [profilen för enhetsbegränsningar](device-restrictions-windows-10.md#microsoft-edge-browser) och konfigurera specifika funktioner och inställningar som tillåts i Microsoft Edge.

- Se till att alla filer, skript och genvägar finns på det lokala systemet. Mer information, inklusive andra Windows-krav, finns i [Anpassa och exportera Start-layout](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Var noga med att tilldela den här helskärmsprofilen till samma enheter som din [Microsoft Edge-profil](device-restrictions-windows-10.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>En app, helskärmsläge

Kör endast en app på enheten.

- **Välj ett helskärmsläge**: Välj **En app, helskärmsläge**.

- **Typ av användarinloggning**: Välj den kontotyp som kör appen. Alternativen är:

  - **Automatisk inloggning (Windows 10 version 1803 och senare)** : Använd på kioskenheter i offentliga miljöer som inte kräver att användaren loggar in, ungefär som ett gästkonto. Den här inställningen använder [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Lokalt användarkonto**: Ange det lokala användarkontot (för enheten). Det konto som du anger loggar in i helskärmsläget.

- **Programtyp**: Välj programtypen. Alternativen är:

  - **Lägg till Microsoft Edge-webbläsare**: Välj **Microsoft Edge-webbläsare** och välj **helskärmslägestyp för Microsoft Edge**:

    - **Digital/interaktiv signering**: Öppnar en URL i helskärmsläge och visar endast innehållet på den webbplatsen. Mer information om den här funktionen finns i [Konfigurera digital signering](https://docs.microsoft.com/windows/configuration/setup-digital-signage).
    - **Offentlig surfning (InPrivate)** : Kör en begränsad version av Microsoft Edge med flera flikar. Användare kan surfa offentligt eller avsluta sin webbläsarsession.

    Mer information om dessa alternativ finns i [Distribuera Microsoft Edge-helskärmsläge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Den här inställningen aktiverar Microsoft Edge-webbläsaren på enheten. För att konfigurera Microsoft Edge-specifika inställningar skapar du en profil för enhetsbegränsningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10** som plattform > **Enhetsbegränsningar** > **Microsoft Edge-webbläsare**). [Microsoft Edge-webbläsare](device-restrictions-windows-10.md#microsoft-edge-browser) visar och beskriver de tillgängliga inställningarna.

  - **Lägg till Kiosk Browser**: Välj **Kiosk Browser-inställningar**. Dessa inställningar definierar hur en webbläsare visas på kioskenheten. Se till att du får [Kiosk Browser-appen](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) från Store och lägg till den i Intune som en [Klientapp](../apps/apps-add.md). Tilldela sedan appen till enheter i helskärmsläge.

    Ange följande inställningar:

    - **Webbadress till standardhemsida**: Ange vilken standardwebbadress som ska visas när webbläsaren öppnas i helskärmläge eller när webbläsaren startas om. Ange till exempel `http://bing.com` eller `http://www.contoso.com`.

    - **Startknapp**: **Visa** eller **dölj** knappen på startsidan i webbläsaren på kioskenheten. Standardinställningen är att knappen inte visas.

    - **Navigeringsknappar**: **Visa** eller **dölj** framåt- och bakåtknappen. Som standard visas inte navigeringsknapparna.

    - **Avsluta session-knapp**: **Visa** eller **dölj** knappen för att avsluta session. När det här visas väljer användaren knappen så uppmanar appen om att avsluta sessionen. När du bekräftar rensar webbläsaren alla webbdata (cookies, cache och så vidare) och öppnar sedan den webbadress som är standard. Standardinställningen är att knappen inte visas.

    - **Uppdatera webbläsaren efter inaktivitetstid**: Ange efter hur lång tid av inaktivitet (1–1 440 minuter) som webbläsaren i helskärmsläge ska starta om i återställt tillstånd. Hur inaktivitetstiden är antalet minuter sedan den senaste interaktionen från en användare. Värdet är tomt som standard, vilket innebär att det inte finns någon tidsgräns för inaktivitet.

    - **Tillåtna webbplatser**: Använd den här inställningen för att tillåta att vissa webbplatser öppnas. Med andra ord kan du använda denna funktion till att begränsa eller förhindra webbplatser på enheten. Du kan till exempel tillåta att alla webbplatser på `http://contoso.com` öppnas. Som standard tillåts alla webbplatser.

      Ladda upp en fil som innehåller en lista med tillåtna webbplatser på separata rader om du vill tillåta specifika webbplatser. Om du inte lägger till någon fil tillåts alla webbplatser. Som standard tillåter Intune alla webbplatsens underdomäner. Tänk dig att du anger domänen `sharepoint.com`. Intune tillåter automatiskt alla underdomäner som `contoso.sharepoint.com`, `my.sharepoint.com` och så vidare. Ange inte jokertecken som en asterisk (`*`).

      Exempelfilen bör likna följande lista:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Helskärmsenheter med Windows 10 som har automatisk inloggning aktiverad och använder Microsoft Kiosk Browser måste använda en offline-licens från Microsoft Store för företag. Detta krav beror på att automatisk inloggning använder ett lokalt användarkonto utan autentiseringsuppgifter för Azure Active Directory. Det går därför inte att utvärdera onlinelicenser. Mer information finns i [Distribuera offlineappar](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Lägg till Store-app**: Välj **Lägg till en Store-app** och välj en app i listan.

    Har du inte några appar i listan? Lägg till några med hjälp av anvisningarna i [Klientappar](../apps/apps-add.md).

- **Ange underhållsperiod för omstart av appar**: För vissa appar krävs en omstart för att slutföra installationen av appen eller eventuella uppdateringar. **Kräv** skapar en underhållsperiod. Om appen måste startas om startas den om under den här perioden.

  Ange även:

  - **Starttid för underhållsperiod**: Välj datumet och tiden på dagen då du vill börja kontrollera om det finns programuppdateringar som kräver omstart på klienter. Standardstarttiden är midnatt, eller noll minuter. Om värdet lämnas tomt startas appar om vid en oplanerad tidpunkt tre dagar efter att en appuppdatering har installerats.

  - **Upprepning av underhållsperiod**: Standardvärdet är varje dag. Välj hur ofta underhållsperioder för appuppdateringar ska äga rum. Rekommendationen är **Varje dag** så att du undviker oplanerade omstarter av appar.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Helskärmsläge för flera appar

Appar i det här läget är tillgängliga på startmenyn. De här apparna är de enda appar som användaren kan öppna. Om en app har ett beroende på en annan app måste båda inkluderas i listan över tillåtna appar. Till exempel har Internet Explorer 64-bitars ett beroende på Internet Explorer 32-bitars, så du måste tillåta både "C:\Program Files\internet explorer\iexplore.exe" och "C:\Program Files (x86)\Internet Explorer\iexplore.exe". 

- **Välj ett helskärmsläge**: Välj **Helskärmsläge för flera appar**.

- **Rikta in enheter med Windows 10 i S-läge**:
  - **Ja**: Tillåter Store-appar och AUMID-appar i helskärmsprofilen. Win32-appar utesluts.
  - **Nej**: Tillåter Store-appar, Win32-appar och AUMID-appar i kioskprofilen. Den här helskärmsprofilen distribueras inte till enheter i S-läge.

- **Typ av användarinloggning**: Välj den kontotyp som kör dina appar. Alternativen är:

  - **Automatisk inloggning (Windows 10 version 1803 och senare)** : Använd på kioskenheter i offentliga miljöer som inte kräver att användaren loggar in, ungefär som ett gästkonto. Den här inställningen använder [AssignedAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Lokalt användarkonto**: **Lägg till** det lokala användarkontot (för enheten). Det konto som du anger loggar in i helskärmsläget.
  - **Azure AD-användare eller -grupp (Windows 10 version 1803 och senare)** : Välj **Lägg till** och välj Azure AD-användare eller -grupper i listan. Du kan välja flera användare och grupper. Välj **OK** för att spara ändringarna.
  - **HoloLens-besökare**: Besökarkontot är ett gästkonto som inte kräver autentiseringsuppgifter eller autentisering, enligt beskrivningen i [begrepp om delat PC-läge](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Webbläsare och program**: Lägg till appar som ska köras på kioskenheten. Kom ihåg att du kan lägga till flera appar.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Lägg till webbläsare eller appar i helskärmsprofilen för flera appar i Microsoft Intune.":::  

  - **Webbläsare**

    - **Lägg till Microsoft Edge**: Microsoft Edge läggs till i apprutnätet, och alla program kan köras på den här helskärmsenheten. Välj **typen av helskärmsläge för Microsoft Edge**:

      - **Normalt läge (fullständig version av Microsoft Edge)** : Kör en fullständig version av Microsoft Edge med alla webbläsarens funktioner. Användardata och tillstånd sparas mellan sessioner.
      - **Offentlig surfning (InPrivate)** : Kör en version av Microsoft Edge InPrivate med flera flikar och en anpassad upplevelse för helskärmsenheter som körs i helskärmsläge.

      Mer information om dessa alternativ finns i [Distribuera Microsoft Edge-helskärmsläge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Den här inställningen aktiverar Microsoft Edge-webbläsaren på enheten. För att konfigurera Microsoft Edge-specifika inställningar skapar du en profil för enhetsbegränsningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > >**Windows 10** som plattform > **Enhetsbegränsningar** >  **Microsoft Edge-webbläsare**). [Microsoft Edge-webbläsare](device-restrictions-windows-10.md#microsoft-edge-browser) visar och beskriver de tillgängliga inställningarna.

    - **Lägg till Kiosk Browser**: Dessa inställningar definierar hur en webbläsare visas på kioskenheten. Kontrollera att du har distribuerat en webbläsarapp till kioskenheterna via [Klientappar](../apps/apps-add.md).

      Ange följande inställningar:

      - **Webbadress till standardhemsida**: Ange vilken standardwebbadress som ska visas när webbläsaren öppnas i helskärmläge eller när webbläsaren startas om. Ange till exempel `http://bing.com` eller `http://www.contoso.com`.

      - **Startknapp**: **Visa** eller **dölj** knappen på startsidan i webbläsaren på kioskenheten. Standardinställningen är att knappen inte visas.

      - **Navigeringsknappar**: **Visa** eller **dölj** framåt- och bakåtknappen. Som standard visas inte navigeringsknapparna.

      - **Avsluta session-knapp**: **Visa** eller **dölj** knappen för att avsluta session. När det här visas väljer användaren knappen så uppmanar appen om att avsluta sessionen. När du bekräftar rensar webbläsaren alla webbdata (cookies, cache och så vidare) och öppnar sedan den webbadress som är standard. Standardinställningen är att knappen inte visas.

      - **Uppdatera webbläsaren efter inaktivitetstid**: Ange hur lång inaktivitetstiden (1–1 440 minuter) ska vara innan kioskenhetens webbläsare startar om med ny status. Hur inaktivitetstiden är antalet minuter sedan den senaste interaktionen från en användare. Värdet är tomt som standard, vilket innebär att det inte finns någon tidsgräns för inaktivitet.

      - **Tillåtna webbplatser**: Använd den här inställningen för att tillåta att vissa webbplatser öppnas. Med andra ord kan du använda denna funktion till att begränsa eller förhindra webbplatser på enheten. Du kan till exempel tillåta att alla webbplatser på `contoso.com*` öppnas. Som standard tillåts alla webbplatser.

        Ladda upp en .csv-fil som innehåller en lista med tillåtna webbplatser om du vill tillåta specifika webbplatser. Om du inte lägger till någon .csv-fil tillåts alla webbplatser.

      > [!NOTE]
      > Helskärmsenheter med Windows 10 som har automatisk inloggning aktiverad och använder Microsoft Kiosk Browser måste använda en offline-licens från Microsoft Store för företag. Detta krav beror på att automatisk inloggning använder ett lokalt användarkonto utan autentiseringsuppgifter för Azure Active Directory. Det går därför inte att utvärdera onlinelicenser. Mer information finns i [Distribuera offlineappar](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Program**

    - **Lägg till Store-app**: Lägg till en app från Microsoft Store för företag. Om du inte har några appar i listan kan du hämta appar och [lägga till dem i Intune](../apps/store-apps-windows.md). Du kan till exempel lägga till Kiosk Browser, Excel, OneNote etc.

    - **Lägg till Win32-App**: En Win32-app är en traditionell skrivbordsapp, till exempel Visual Studio Code eller Google Chrome. Ange följande egenskaper:

      - **Programnamn**: Obligatoriskt. Ange ett namn på programmet.
      - **Lokal sökväg till körbar app-fil**: Obligatoriskt. Ange sökvägen till den körbara filen, till exempel `C:\Program Files (x86)\Microsoft VS Code\Code.exe` eller `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **Win32-appens ID för programanvändarmodellen (AUMID)** : Ange ID för programanvändarmodellen (AUMID) för Win32-appen. Den här inställningen avgör panelens startlayout på skrivbordet. Se [Get-StartApps](https://docs.microsoft.com/powershell/module/startlayout/get-startapps?view=win10-ps) för hur du hämtar detta ID.

    - **Lägg till via AUMID**: Använd det här alternativet för att lägga till inkorgens Windows-appar, till exempel Anteckningar eller Kalkylatorn. Ange följande egenskaper:

      - **Programnamn**: Obligatoriskt. Ange ett namn på programmet.
      - **ID för programanvändarmodell (AUMID)** : Obligatoriskt. Ange appens programanvändarmodell-ID (AUMID) för Windows-appen. Information om hur du hittar detta ID finns i [Hitta programanvändarmodell-ID för en installerad app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **Autostart**: Valfritt. När du har lagt till appar och webbläsare väljer du en app eller webbläsare som ska öppnas automatiskt när användaren loggar in. Du kan bara starta en app eller webbläsare automatiskt.
    - **Panelstorlek**: Obligatoriskt. När du har lagt till dina appar väljer du en liten, medelstor, bred eller stor storlek för appanelen.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Starta appen eller webbläsaren automatiskt och välj panelstorlek i en helskärmsprofil för flera appar i Microsoft Intune.":::

  > [!TIP]
  > När du har lagt till alla appar kan du ändra visningsordning genom att klicka och dra apparna i listan.  

- **Använd alternativ startlayout**: Välj **Ja** för att ange en XML-fil som beskriver hur apparna ska visas på Start-menyn, inklusive apparnas inbördes ordning. Använd det här alternativet om du behöver anpassa mer på startmenyn. [Anpassa och exportera Start-layout](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout) innehåller en del vägledning och XML-exempel.

- **Aktivitetsfältet**: Välj om du vill **visa** eller **dölja** aktivitetsfältet. Standardinställningen är att aktivitetsfältet inte visas. Ikoner som exempelvis Wi-Fi-ikonen visas, men inställningarna kan inte ändras av slutanvändarna.

- **Tillåt åtkomst till mappen Hämtade filer**: Välj **Ja** för att tillåta användarna att komma åt mappen Hämtade filer i Utforskaren. Som standard är åtkomst till mappen Hämtade filer inaktiverad. Den här funktionen används vanligtvis för att ge slutanvändare möjligheten att komma åt objekt som laddats ned från en webbläsare.

- **Ange underhållsperiod för omstart av appar**: För vissa appar krävs en omstart för att slutföra installationen av appen eller eventuella uppdateringar. **Kräv** skapar en underhållsperiod. Om apparna måste startas om startas de om under den här perioden.

  Ange även:

  - **Starttid för underhållsperiod**: Välj datumet och tiden på dagen då du vill börja kontrollera om det finns programuppdateringar som kräver omstart på klienter. Standardstarttiden är midnatt, eller noll minuter. Om värdet lämnas tomt startas appar om vid en oplanerad tidpunkt tre dagar efter att en appuppdatering har installerats.

  - **Upprepning av underhållsperiod**: Standardvärdet är varje dag. Välj hur ofta underhållsperioder för appuppdateringar ska äga rum. Rekommendationen är **Varje dag** så att du undviker oplanerade omstarter av appar.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa helskärmsprofiler för [Android](device-restrictions-android.md#kiosk)-, [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)- och [Windows Holographic for Business](kiosk-settings-holographic.md)-enheter.

Det finns även information om hur man kan [konfigurera helskärmsläge för enskild app](https://docs.microsoft.com/windows/configuration/kiosk-single-app) eller [konfigurera helskärmsläge för flera appar](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps) i Windows-vägledningen.
