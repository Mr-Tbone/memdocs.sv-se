---
title: Lägga till och tilldela MTD-appar i Microsoft Intune
titleSuffix: Microsoft Intune
description: Använda Intune för att lägga till MTD-program, Microsoft Authenticator-app och iOS-konfigurationsprincip i Azure-portalen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b487b9f921e40df8730fab235a2ec2c0d3f0f788
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910867"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Lägg till och tilldela MTD-appar med Intune

Du kan använda Intune för att lägga till och distribuera MTD-apparna (Mobile Threat Defense) så att slutanvändarna får ett meddelande när ett hot har identifierats i deras mobila enheter och anvisningar för att åtgärda hoten.

> [!NOTE]
> Den här artikeln gäller alla Mobile Threat Defense-partner.

## <a name="before-you-begin"></a>Innan du börjar

Utför följande steg i Intune. Kontrollera att du vet hur man gör för att:

- [Lägga till en app i Intune](../apps/apps-add.md).
- [Lägga till en konfigurationsprincip för iOS-appar i Intune](../apps/app-configuration-policies-use-ios.md).
- [Tilldela en app med Intune](../apps/apps-deploy.md).

> [!TIP]
> Intune-företagsportalen fungerar som broker på Android-enheter så att användare kan få sina identiteter kontrollerade av Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Konfigurera Microsoft Authenticator för iOS

För iOS-enheter krävs [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) så att användarnas identiteter kan kontrolleras av Azure AD. Dessutom behövs en konfigurationsprincip för iOS-appar som konfigurerar MTD iOS-appen för användning med Intune.

Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Microsoft Authenticator-apparna](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) när du konfigurerar **appinformation**.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>Konfigurera dina MTD-appar med en appkonfigurationsprincip

För att förenkla användarregistrering använder appar för skydd mot mobila hot på MDM-hanterade enheter appkonfiguration. För ej registrerade enheter är MDM-baserad appkonfiguration inte tillgänglig, se [Lägg till skydd mot mobila hot-appar i enheter som inte registrerats](../protect/mtd-add-apps-unenrolled-devices.md).

### <a name="lookout-for-work-app-configuration-policy"></a>Konfigurationsprincip för Lookout for Work-app

Skapa konfigurationsprincipen för iOS-appar enligt beskrivningen i artikeln om att [använda konfigurationsprincipen för iOS-appar](../apps/app-configuration-policies-use-ios.md).

### <a name="sep-mobile-app-configuration-policy"></a>Konfigurationsprincip för SEP Mobile-app

Använd samma Azure AD-konto som tidigare konfigurerades i [Symantec Endpoint Protection-hanteringskonsolen](https://aad.skycure.com), vilket ska vara samma konto som användes för att logga in på Intune.

- **Ladda ned** konfigurationsprincipsfilen för iOS-appen:
  - Gå till [Symantec Endpoint Protection-hanteringskonsol](https://aad.skycure.com) och logga in med dina administratörsautentiseringsuppgifter.

  - Gå till **Inställningar** och under **Integreringar** väljer du **Intune**. Välj **Val av EMM-integrering**. Välj **Microsoft** och spara sedan ditt val.

  - Klicka på länken **Integrering av installationsfiler** och spara den genererade \*-ZIP-filen. ZIP-filen innehåller filen * **.plist** som används för att skapa iOS-appens konfigurationsprincip i Intune.

  - Se anvisningarna för [användning av Microsoft Intune-appkonfigurationsprinciper för iOS](../apps/app-configuration-policies-use-ios.md) för att lägga till SEP Mobile-konfigurationsprincipen för iOS-appar.

    - Välj **Ange XML-data** som **format för konfigurationsinställningarna**. Kopiera innehållet från filen * **.plist** och klistra in det i konfigurationsprincipens text.

> [!NOTE]
> Om det inte går att hämta filerna, kontakta [Symantec Endpoint Protection Mobile Enterprise Support](https://support.symantec.com/en_US/contact-support.html).

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Konfigurationsprincip för Check Point SandBlast Mobile-app

Se anvisningarna för [användning av Microsoft Intune-appkonfigurationsprinciper för iOS](../apps/app-configuration-policies-use-ios.md) för att lägga till Check Point SandBlast Mobile-konfigurationsprincipen för iOS-appar.

- Välj **Ange XML-data** som **format för konfigurationsinställningarna**. Kopiera följande innehåll och klistra in det i konfigurationsprincipens text.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Konfigurationsprincip för Zimperium-app

Se anvisningarna för att [använda Microsoft Intune-appkonfigurationsprinciper för iOS](../apps/app-configuration-policies-use-ios.md) för att lägga till Zimperium-konfigurationsprincipen för iOS-appar.

- Välj **Ange XML-data** som **format för konfigurationsinställningarna**. Kopiera följande innehåll och klistra in det i konfigurationsprincipens text.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Konfigurationsprincip för Pradeo-appar

Pradeo stöder inte programkonfigurationsprincipen på iOS/iPadOS.  För att istället få en konfigurerad app kan du arbeta med Pradeo för att implementera anpassade IPA- eller APK-filer som är förkonfigurerade med de inställningar som du önskar.

### <a name="better-mobile-app-configuration-policy"></a>Konfigurationsprincip för Better Mobile-appen

Se anvisningarna för [användning av Microsoft Intune-appkonfigurationsprinciper för iOS](../apps/app-configuration-policies-use-ios.md) när du ska lägga till en konfigurationsprincip för Better Mobile iOS-appen.

- Välj **Ange XML-data** som **format för konfigurationsinställningarna**. Kopiera följande innehåll och klistra in det i konfigurationsprincipens text. Ersätt webbadressen `https://client.bmobi.net` med rätt konsoladress.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Konfigurationsprincip för Sophos Mobile-appen

Skapa konfigurationsprincipen för iOS-appar enligt beskrivningen i artikeln om att [använda konfigurationsprincipen för iOS-appar](../apps/app-configuration-policies-use-ios.md). Mer information finns i [Sophos Intercept X för mobila iOS – Tillgängliga hanterade inställningar](https://community.sophos.com/kb/133963) i Sophos kunskapsbas.

### <a name="wandera-app-configuration-policy"></a>Konfigurationsprincip för Wandera-appar

> [!NOTE]
> Vid inledande testning, använd en testgrupp när du tilldelar användare och enheter i avsnittet Tilldelningar i konfigurationsprincipen. 

- **Android**
  - Se anvisningarna för [använda av Microsoft Intune-appkonfigurationsprinciper för Android](../apps/app-configuration-policies-use-android.md) för att lägga till Wandera-konfigurationsprincipen för Android-appar med informationen nedan när du ombeds.

1. I **RADAR Wandera-portalen** klickar du på knappen **Lägg till** under **Konfigurationsinställningar**-formatet.
2. Välj **Aktiveringsprofil-URL** i listan över **Konfigurationsnycklar**. Klicka på **OK**.
3. För **Aktiveringsprofil-URL** väljer du **sträng** från **Värdetyp**-menyn och kopierar **URL för delningsbar länk** från önskad aktiveringsprofil i RADAR.
4. I **Konfigurationsgränssnittet för Intune-administratörskonsolen** väljer du **Inställningar**, definierar **Format för konfigurationsinställningar > Använd Configuration Designer** och klistrar in **URL för delningsbar länk**.  

> [!NOTE] 
> Till skillnad från iOS måste du definiera en unik appkonfigurationsprincip för Android-Enterprise för varje Wandera-aktiveringsprofil. Om du inte behöver flera Wandera-aktiveringsprofiler kan du använda en enda Android-appkonfiguration för alla målenheter. När du skapar aktiveringsprofiler i Wandera måste du välja Azure Active Directory under den associerade användarkonfigurationen för att säkerställa att Wandera kan synkronisera enheten med Intune via UEM Connect.

- **iOS**
  - Se anvisningarna för [använda Microsoft Intune-appkonfigurationsprinciper för iOS](../apps/app-configuration-policies-use-ios.md) för att lägga till Wandera-konfigurationsprincipen med informationen nedan när du ombeds.

1. I **RADAR Wandera-portalen** går du till **Enheter > Aktiveringar** och väljer valfri aktiveringsprofil. Klicka på **Distributionsstrategier > Hanterade enheter > Microsoft Intune** och leta upp **Konfigurationsinställningar för iOS-appen**.  
2. Expandera rutan om du vill visa XML-konfigurationsfilen för iOS-appen och kopiera den till systemets Urklipp.  
3. I **Inställningar för konfigurationsgränssnittet för Intune-administratörskonsolen** definierar du **Format för konfigurationsinställningar > Ange XML-data**. 
4. Klistra in XML-koden i textrutan för appkonfiguration.

> [!NOTE]
> En enda iOS-konfigurationsprincip kan användas på alla enheter som ska etableras med Wandera.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Tilldela appar för skydd mot mobilhot till slutanvändare via Intune

Om du vill installera appen för skydd mot mobilhot på slutanvändarens enhet så kan du följa stegen nedan i Azure Portal. Kontrollera att du vet hur man gör för att:

- [Tilldela appar till grupper med Intune](../apps/apps-deploy.md)

Välj det avsnitt som motsvarar din MTD-provider:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Tilldela Lookout for Work

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Lookout for Work-apparna för Google](https://play.google.com/store/apps/details?id=com.lookout.enterprise) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Lookout for Work-apparna för iOS](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) som **appbutiksadress**.

- **Lookout for Work-app utanför Apple Store**
  - Du måste omsignera iOS-appen Lookout for Work. Lookout distribuerar iOS-appen Lookout for Work utanför iOS App Store. Innan du distribuerar appen måste du signera den på nytt med ditt iOS Enterprise Developer-certifikat.  
  - Detaljerade anvisningar om hur du omsignerar iOS-apparna Lookout for Work finns i [Omsigneringsprocessen för iOS-appen Lookout for Work](https://personal.support.lookout.com/hc/articles/114094038714) på Lookout-webbplatsen.

  - **Aktivera Azure AD-autentisering för användare av Lookout for Work iOS-appen.**

    1. Gå till [Azure-portalen](https://portal.azure.com), logga in med dina autentiseringsuppgifter och gå sedan till appsidan.

    2. Lägg till **Lookout for Work iOS app** (iOS-appen Lookout for Work) som ett **internt klientprogram**.

    3. Ersätt **com.lookout.enterprise.yourcompanyname** med ID:t för kundprogrampaketet som du valde när du registrerade IPA.

    4. Lägg till ytterligare omdirigerings-URI: **&lt;companyportal://code/>** följt av en URL-kodad version av din ursprungliga omdirigerings-URI.

    5. Lägg till **Delegerad behörighet** till din app.

    > [!NOTE]
    > Mer information finns i [configure a native client application with Azure AD](/azure/app-service/configure-authentication-provider-aad#optional-configure-a-native-client-application) (konfigurera ett Native Client-program med Azure AD).

  - **Lägg till IPA-filen för Lookout for Work.**

    - Ladda upp den omsignerade IPA-filen enligt beskrivningen i artikeln [Add iOS LOB apps with Intune](../apps/lob-apps-ios.md) (Lägg till iOS LOB-appar med Intune). Du måste också ange den lägsta versionen av operativsystemet till iOS 8.0 eller senare.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Tilldela Symantec Endpoint Protection Mobile

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till SEP Mobile-apparna](https://play.google.com/store/apps/details?id=com.skycure.skycure) som **appbutiksadress**.  Som **Lägsta operativsystem** väljer du **Android 4.0 (Ice Cream Sandwich)** .

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till SEP Mobile-apparna](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) som **appbutiksadress**.

### <a name="assigning-check-point-sandblast-mobile"></a>Tilldela Check Point SandBlast Mobile

- **Android**  
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Check Point SandBlast-apparna](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Check Point SandBlast-apparna](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) som **appbutiksadress**.  

### <a name="assigning-zimperium"></a>Tilldela Zimperium

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Zimperium-apparna](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Zimperium-apparna](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) som **appbutiksadress**.  
 
### <a name="assigning-pradeo"></a>Tilldela Pradeo

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Pradeo-apparna](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Pradeo-apparna](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) som **appbutiksadress**.

### <a name="assigning-better-mobile"></a>Tilldela Better Mobile

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Active Shield-apparna](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Active Shield-apparna](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) som **appbutiksadress**.

### <a name="assigning-sophos"></a>Tilldela Sophos

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Sophos-apparna](https://play.google.com/store/apps/details?id=com.sophos.smsec) som **appbutiksadress**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Active Shield-apparna](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) som **appbutiksadress**.

### <a name="assigning-wandera"></a>Tilldela Wandera

- **Android**
  - Se anvisningarna för att [lägga till Android Store-appar i Microsoft Intune](../apps/store-apps-android.md). Använd [webbadressen till Wandera Mobile-apparna](https://play.google.com/store/apps/details?id=com.wandera.android) som **appbutiksadress**. Som **Lägsta operativsystem** väljer du **Android 5.0**.

- **iOS**
  - Läs anvisningarna för att [lägga till iOS Store-appar i Microsoft Intune](../apps/store-apps-ios.md). Använd [webbadressen till Wandera Mobile-apparna](https://itunes.apple.com/app/wandera/id605469330) som **appbutiksadress**.

## <a name="next-steps"></a>Nästa steg

- [Konfigurera enhetsefterlevnadsprincipen för MTD](mtd-device-compliance-policy-create.md)