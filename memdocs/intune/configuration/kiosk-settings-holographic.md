---
title: Helskärmsinställningar för Windows Holographic for Business i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera helskärmsläget i dina Windows Holographic for Business-enheter för en app eller för flera appar, anpassa startmenyn, lägg till appar, visa aktivitetsfältet och konfigurera en webbläsare i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d54e02c7bb88354ec59a9a8ce780ff559377466
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556106"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Enhetsinställningar i Windows Holographic for Business för att köra helskärmsläge i Intune

På Windows Holographic for Business-enheter kan du konfigurera enheterna att köra i helskärmsläge för en enskild app eller helskärmsläge för flera appar. Vissa funktioner stöds inte i Windows Holographic for Business.

Den här artikeln visar och beskriver de olika inställningar som du kan styra på Windows Holographic for Business-enheter. I din MDM-lösning (hantering av mobilenheter) använder du inställningarna till att konfigurera att dina Windows Holographic for Business-enheter körs i helskärmsläge.

Som Intune-administratör kan du skapa och tilldela dessa inställningar till dina enheter.

Mer information om Windows helskärmsfunktion i Intune finns i [Konfigurera inställningar för helskärmsläge](kiosk-settings.md).

## <a name="before-you-begin"></a>Innan du börjar

- [Skapa en enhetskonfigurationsprofil för Windows 10-helskärmsläge](kiosk-settings.md#create-the-profile).

  När du skapar en enhetskonfigurationsprofil för Windows 10-helskärmsläge finns det fler inställningar än vad som anges i den här artikeln. Inställningarna i den här artikeln stöds på Windows Holographic for Business-enheter.

- Den här helskärmsprofilen är direkt kopplad till den profil för enhetsbegränsningar som du skapar med [Microsoft Edge-helskärmsinställningarna](device-restrictions-windows-holographic.md#microsoft-edge-browser). Sammanfattningsvis:

  1. Skapa den här helskärmsprofilen för att köra enheten i helskärmsläge.
  2. Skapa [profilen för enhetsbegränsningar](device-restrictions-windows-holographic.md#microsoft-edge-browser) och konfigurera specifika funktioner och inställningar som tillåts i Microsoft Edge.

> [!IMPORTANT]
> Var noga med att tilldela den här helskärmsprofilen till samma enheter som din [Microsoft Edge-profil](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>En app, helskärmsläge

Kör endast en app på enheten. Appen startas när användaren loggar in. Det här läget gör också att användaren inte kan öppna nya appar eller ändra appen som körs.

- **Typ av användarinloggning**: Välj den kontotyp som kör appen. Alternativen är:

  - **Automatisk inloggning (Windows 10 version 1803 och senare)** : Stöds inte i Windows Holographic for Business.
  - **Lokalt användarkonto**: Ange det lokala användarkontot (för enheten). Du kan också ange Microsoft-konto (MSA) som är associerat med helskärmslägesappen. Det konto som du anger loggar in i helskärmsläget.

    För helskärmslägen i offentliga miljöer ska du använda en användartyp med lägsta möjliga behörighet.

- **Programtyp**: Välj **Lägg till Store-app**.

  - **App som ska köras i helskärmsläge**: Välj en app i listan.

    Har du inte några appar i listan? Lägg till några med hjälp av anvisningarna i [Klientappar](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Helskärmsläge för flera appar

Appar i det här läget är tillgängliga på startmenyn. De här apparna är de enda appar som användaren kan öppna. Om en app har ett beroende på en annan app måste båda inkluderas i listan över tillåtna appar.

- **Rikta in enheter med Windows 10 i S-läge**: Välj **Nej**. S-läge stöds inte i Windows Holographic for Business.

- **Typ av användarinloggning**: Lägg till ett eller flera användarkonton som kan använda de appar som du lägger till. Alternativen är:

  - **Automatisk inloggning (Windows 10 version 1803 och senare)** : Stöds inte i Windows Holographic for Business.
  - **Lokala användarkonton**: **Lägg till** det lokala användarkontot (för enheten). Det konto som du anger loggar in i helskärmsläget.
  - **Azure AD-användare eller -grupp (Windows 10, version 1803 och senare)** : Kräver autentiseringsuppgifter för inloggning på enheten. Välj **Lägg till** för att välja Azure AD-användare eller grupper i listan. Du kan välja flera användare och grupper. Välj **OK** för att spara ändringarna.
  - **HoloLens-besökare**: Besökarkontot är ett gästkonto som inte kräver autentiseringsuppgifter eller autentisering, enligt beskrivningen i [begrepp om delat PC-läge](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Webbläsare och program**: Lägg till appar som ska köras på kioskenheten. Kom ihåg att du kan lägga till flera appar.

  - **Webbläsare**
    - **Lägg till Microsoft Edge**: Microsoft Edge läggs till i apprutnätet, och alla program kan köras på den här helskärmsenheten. Välj typen av helskärmsläge för Microsoft Edge:

      - **Normalt läge (fullständig version av Microsoft Edge)** : Kör en fullständig version av Microsoft Edge med alla webbläsarens funktioner. Användardata och tillstånd sparas mellan sessioner.
      - **Offentlig surfning (InPrivate)** : Kör en version av Microsoft Edge InPrivate med flera flikar och en anpassad upplevelse för helskärmsenheter som körs i helskärmsläge.

      Mer information om dessa alternativ finns i [Distribuera Microsoft Edge-helskärmsläge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Den här inställningen aktiverar Microsoft Edge-webbläsaren på enheten. För att konfigurera Microsoft Edge-specifika inställningar skapar du en profil för enhetsbegränsningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10** som plattform > **Enhetsbegränsningar** > **Microsoft Edge-webbläsare**). [Microsoft Edge-webbläsare](device-restrictions-windows-holographic.md#microsoft-edge-browser) visar och beskriver de tillgängliga inställningarna för Holographic for Business.

    - **Lägg till Kiosk Browser**: Stöds inte i Windows Holographic for Business.

  - **Program**
    - **Lägg till Store-app**: Välj en befintlig app som du har lagt till eller distribuerat till Intune som [klientappar](../apps/apps-add.md), inklusive LOB-appar. Om du inte har några appar i lista, stöder Intune många [apptyper](../apps/apps-add.md) som du kan [lägga till i Intune](../apps/store-apps-windows.md).
    - **Lägg till Win32-app**: Stöds inte i Windows Holographic for Business.
    - **Lägg till via AUMID**: Använd det här alternativet för att lägga till inkorgens Windows-appar, till exempel Anteckningar eller Kalkylatorn. Ange följande egenskaper:

      - **Programnamn**: Obligatoriskt. Ange ett namn på programmet.
      - **ID för programanvändarmodell (AUMID)** : Obligatoriskt. Ange appens programanvändarmodell-ID (AUMID) för Windows-appen. Information om hur du hittar detta ID finns i [Hitta programanvändarmodell-ID för en installerad app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **Autostart**: Valfritt. När du har lagt till appar och webbläsare väljer du en app eller webbläsare som ska öppnas automatiskt när användaren loggar in. Du kan bara starta en app eller webbläsare automatiskt.
    - **Panelstorlek**: Obligatoriskt. När du har lagt till dina appar väljer du en liten, medelstor, bred eller stor storlek för appanelen.

- **Använd alternativ startlayout**: Välj **Ja** för att ange en XML-fil som beskriver hur apparna ska visas på Start-menyn, inklusive apparnas inbördes ordning. Använd det här alternativet om du behöver anpassa mer på startmenyn. [Anpassa och exportera Start-layout](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) ger viss vägledning och innehåller en specifik XML-fil för Windows Holographic for Business-enheter.

- **Aktivitetsfältet**: Stöds inte i Windows Holographic for Business.
- **Tillåt åtkomst till mappen Hämtade filer**: Stöds inte i Windows Holographic for Business.
- **Ange underhållsperiod för omstart av appar**: Stöds inte i Windows Holographic for Business.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa helskärmsprofiler för enheter som kör [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) samt [Windows 10 och senare](kiosk-settings-windows.md).
