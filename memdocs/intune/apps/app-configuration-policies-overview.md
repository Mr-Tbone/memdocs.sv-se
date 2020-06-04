---
title: Appkonfigurationsprinciper för Microsoft Intune
titleSuffix: ''
description: Läs om hur du använder appkonfigurationsprinciper på en iOS/iPadOS- eller Android-enhet i Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 834B4557-80A9-48C0-A72C-C98F6AF79708
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e99922c920966f4f0bb1037b5fc74799cfca7c5
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988780"
---
# <a name="app-configuration-policies-for-microsoft-intune"></a>Appkonfigurationsprinciper för Microsoft Intune

Appkonfigurationsprinciper kan hjälpa dig att förhindra problem med konfiguration av appar eftersom du kan tilldela konfigurationsinställningar till en princip som tilldelas till slutanvändare innan de kör appen. Inställningarna anges sedan automatiskt när appen konfigureras på slutanvändarnas enheter, och slutanvändarna behöver då inte vidta några åtgärder. Konfigurationsinställningarna är unika för varje app. 

Du kan skapa och använda appkonfigurationsprinciper för att ge konfigurationsinställningar för både iOS/iPadOS-appar och Android-appar. Med dessa konfigurationsinställningar kan en app anpassas med hjälp av konfiguration och hantering av appar. Inställningarna för konfigurationsprincipen används när appen söker efter inställningarna, oftast första gången appen körs. 

Till exempel kan en appkonfigurationsinställning kräva att du anger några av de följande uppgifterna:

- Ett anpassat portnummer
- Språkinställningar
- Säkerhetsinställningar
- Anpassade inställningar, t.ex. en företagslogotyp

Om slutanvändarna skulle ange inställningarna i stället kan de göra detta felaktigt. Appkonfigurationsprinciper kan bidra till enhetlighet i ett företag och minska samtal till supporten från slutanvändare som försöker konfigurera inställningar på egen hand. Med hjälp av appkonfigurationsprinciper kan införandet av nya appar bli enklare och snabbare.

De tillgängliga konfigurationsparametrarna bestäms slutligen av appens utvecklare. Dokumentation från programleverantören bör granskas i syfte att kontrollera om en app stöder konfiguration och vilka konfigurationer som är tillgängliga. För vissa program fyller Intune i de tillgängliga konfigurationsinställningarna. 

> [!NOTE]
> I den hanterade Google Play Store markeras appar som stöder konfiguration därefter:
> 
> ![Skärmbild av en konfigurerad app](./media/app-configuration-policies-overview/configured-app.png)
>
> Du ser bara appar från [hanterad Google Play Store](https://play.google.com/work), inte [Google Play Store](https://play.google.com/store/apps), när du använder hanterade enheter som registreringstyp för Android-enheter. Hanterad Google Play Store, som även kallas Android for Work (AfW) och Android Enterprise, är de appar i arbetsprofilen som innehåller de appversioner som stöder appkonfiguration.

Du kan tilldela en appkonfigurationsprincip till en grupp med slutanvändare och enheter med hjälp av en kombination av [tilldelningar som inkluderar och exkluderar](apps-inc-exl-assignments.md). När du lägger till en appkonfigurationsprincip kan du ange tilldelningar för den. När du anger tilldelningar för principen kan du välja att inkludera och exkludera de [grupper](../fundamentals/groups-add.md) av slutanvändare som principen gäller för. När du väljer att inkludera en eller flera grupper kan du välja att utse specifika grupper att inkludera eller välja inbyggda grupper. Inbyggda grupper innefattar **Alla användare**, **Alla enheter** samt **Alla användare + alla enheter**.

Du har två alternativ vad gäller användning av appkonfigurationsprinciper med Intune:
- **Hanterade enheter** – enheten hanteras av Intune som MDM-leverantör (hantering av mobila enheter). Appen måste vara utformad för att stödja appkonfigurationen.
- **Hanterade appar** – en app som har utvecklats för att integrera Intune App SDK. Detta kallas hantering av mobilprogram utan registrering ([MAM-WE](app-management.md#mobile-application-management-mam-basics)). Du kan även omsluta en app för att implementera och stödja Intune App SDK. Mer information om omslutning av en app finns i [Förbereda verksamhetsspecifika appar för appskyddsprinciper](../developer/apps-prepare-mobile-application-management.md).

    > [!NOTE]
    > Intune-hanterade appar checkar in med ett intervall på 30 minuter för status för Intune-appkonfigurationsprincip när de distribueras tillsammans med en Intune-appskyddsprincip. Om en Intune-appskyddsprincip inte är tilldelad till användaren är incheckningsintervallet för Intune-appkonfigurationsprincip angett till 720 minuter.

## <a name="apps-that-support-app-configuration"></a>Appar som stöder appkonfiguration

### <a name="managed-devices"></a>Hanterade enheter
Du kan använda appkonfigurationsprinciper för appar som stöder det. För att stödja appkonfiguration i Intune måste appar ha skrivits för att stödja användningen av appkonfigurationer enligt definitionen från operativsystemet. Kontakta appleverantören för information om vilka appkonfigurationsnycklar som stöds.

### <a name="managed-apps"></a>Hanterade appar
Du kan förbereda dina verksamhetsspecifika appar genom att antingen integrera [Intune App SDK](../developer/app-sdk.md) i appen eller genom att omsluta appen när den har utvecklats med hjälp av [Intune-verktyget för omslutning av appar](../developer/apps-prepare-mobile-application-management.md). Intune App SDK syftar till att minimera den mängd kodändringar i programmet som apputvecklare behöver göra. Mer information finns i [Översikt över Intune App SDK](../developer/app-sdk.md). En jämförelse mellan Intune App SDK och Intune-verktyget för omslutning av appar finns i [Förbereda verksamhetsspecifika appar för appskyddsprinciper](../developer/apps-prepare-mobile-application-management.md#feature-comparison).

Val av **Hanterade appar** som **Enhetsregistreringstyp** syftar specifikt på appar som konfigureras av Intune-konfigurationsprinciper på en enhet som inte är registrerad i enhetshantering, medan **Hanterade enheter** gäller för appar som distribueras via MDM-kanalen och därmed hanteras av Intune. Välj lämpligt alternativ baserat på dessa beskrivningar. 

![Enhetsregistreringstyp](./media/app-configuration-policies-overview/device-enrollment-type.png)

> [!NOTE]
> För appar med flera identiteter, till exempel Microsoft Outlook, kan användarinställningar beaktas. Prioriterad inkorg, till exempel, respekterar användarinställningen och ändrar inte konfigurationen. Andra parametrar gör det möjligt att kontrollera huruvida en användare kan ändra inställningen. Mer information finns i [Distribuera appkonfigurationsinställningar för Outlook för iOS/iPadOS och Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="android-app-configuration-policies"></a>Konfigurationsprinciper för Android-appar

För konfigurationsprinciper för Android-appar kan du välja typ av enhetsregistrering innan du skapar en konfigurationsprofil för appar. Du kan redovisa certifikatprofiler som baseras på registreringstyp (arbetsprofil eller enhetsägare). Den här uppdateringen innehåller följande:

1. Om en ny profil skapas och arbetsprofil och enhetsägarprofil väljs som enhetsregistreringstyp kan du inte associera en certifikatprofil med appkonfigurationsprincipen.
2. Om en ny profil skapas och Endast arbetsprofil har valts kan de certifikatprinciper för arbetsprofil som skapats under Enhetskonfiguration användas.
3. Om en ny profil skapas och Endast enhetens ägare har valts kan de certifikatprinciper för enhetsägare som skapats under Enhetskonfiguration användas. 
4. Om du distribuerar en Gmail- eller Nine-konfigurationsprofil till en dedikerad Android Enterprise-enhet som inte involverar en användare misslyckas det eftersom Intune inte kan matcha användaren.

> [!IMPORTANT]
> För de befintliga principer som skapats före lanseringen av den här funktionen (april 2020, version 2004) och som inte har några associerade certifikatprofiler, används som standard arbetsprofil och enhetsägarprofil som enhetsregistreringstyp. Även för de befintliga principer som skapats före lanseringen av den här funktionen och som har associerade certifikatprofiler, används som standard endast arbetsprofil.
> 
> Befintliga principer kan inte åtgärda eller utfärda nya certifikat.

## <a name="validate-the-applied-app-configuration-policy"></a>Verifiera den tillämpade appkonfigurationsprincipen

Du kan verifiera appkonfigurationsprincipen med följande tre metoder:

   1. Synligt på enheten. Har den avsedda appen det beteende som tillämpats i appkonfigurationsprincipen?
   2. Via diagnostikloggar (se avsnittet Diagnostikloggar nedan).
   3. I Intune-portalen. Avsnittet **Övervakare** i en princip kan ge relevant status:

      ![Första skärmbilden av enhetens installationsstatus](./media/app-configuration-policies-overview/device-install-status-1.png)

      ![Andra skärmbilden av enhetens installationsstatus](./media/app-configuration-policies-overview/device-install-status-2.png)

      Under **Intune** -> **enheter** -> **Alla enheter** på vänster sida av skärmen visar dessutom alternativet **Appkonfiguration** alla tilldelade principer och deras tillstånd:

      ![Skärmbild av appkonfiguration](./media/app-configuration-policies-overview/app-configuration.png)

## <a name="diagnostic-logs"></a>Diagnostikloggar

### <a name="iosipados-configuration-on-unmanaged-devices"></a>iOS/iPadOS-konfiguration på ohanterade enheter

Du kan verifiera iOS/iPadOS-konfigurationen med **Intune-diagnostikloggen** på ohanterade enheter för konfiguration av hanterade appar. Förutom stegen nedan så kan du få åtkomst till hanterade apploggar med hjälp av Microsoft Edge. Mer information finns i [Använda Edge för iOS och Android till att komma åt loggar för hanterade appar](manage-microsoft-edge.md#use-edge-for-ios-and-android-to-access-managed-app-logs).

1. Om den inte redan är installerad på enheten laddar du ned och installerar **Microsoft Edge** från App Store. Mer information finns i [Microsoft Intune-skyddade appar](apps-supported-intune-apps.md).
2. Starta **Microsoft Edge** och välj **Om** > **intunejälp** i navigeringsfältet.
3. Klicka på **Kom igång**.
4. Klicka på **Dela loggar**.
5. Använd valfri e-postapp för att skicka loggen till dig själv så att den kan visas på din dator. 
6. Granska **IntuneMAMDiagnostics.txt** i ditt visningsprogram för textfiler.
7. Sök efter `ApplicationConfiguration`. Resultatet ser ut så här:

    ``` JSON
        {
            (
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.BlockListURLs";
                    Value = "https://www.aol.com";
                },
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.bookmarks";
                    Value = "Outlook Web|https://outlook.office.com||Bing|https://www.bing.com";
                }
            );
        },
        {
            ApplicationConfiguration =             
            (
                {
                Name = IntuneMAMUPN;
                Value = "CMARScrubbedM:13c45c42712a47a1739577e5c92b5bc86c3b44fd9a27aeec3f32857f69ddef79cbb988a92f8241af6df8b3ced7d5ce06e2d23c33639ddc2ca8ad8d9947385f8a";
                },
                {
                Name = "com.microsoft.outlook.Mail.NotificationsEnabled";
                Value = false;
                }
            );
        }
    ```

Informationen om programkonfigurationen bör överensstämma med de programkonfigurationsprinciper som konfigurerats för din klient. 

![Konfiguration av riktade appar](./media/app-configuration-policies-overview/targeted-app-configuration-3.png)

### <a name="iosipados-configuration-on-managed-devices"></a>iOS/iPadOS-konfiguration på hanterade enheter

Du kan verifiera iOS/iPadOS-konfigurationen med **Intune-diagnostikloggen** på hanterade enheter för konfiguration av hanterade appar.

1. Om den inte redan är installerad på enheten laddar du ned och installerar **Microsoft Edge** från App Store. Mer information finns i [Microsoft Intune-skyddade appar](apps-supported-intune-apps.md).
2. Starta **Microsoft Edge** och välj **Om** > **intunejälp** i navigeringsfältet.
3. Klicka på **Kom igång**.
4. Klicka på **Dela loggar**.
5. Använd valfri e-postapp för att skicka loggen till dig själv så att den kan visas på din dator. 
6. Granska **IntuneMAMDiagnostics.txt** i ditt visningsprogram för textfiler.
7. Sök efter `AppConfig`. Resultatet bör överensstämma med de programkonfigurationsprinciper som konfigurerats för din klient.

### <a name="android-configuration-on-managed-devices"></a>Android-konfiguration på hanterade enheter

Du kan verifiera Android-konfigurationen med **Intune-diagnostikloggen** på hanterade enheter för konfiguration av hanterade appar.

Om du vill samla in loggar från en Android-enhet måste du eller slutanvändaren ladda ned loggarna från enheten via en USB-anslutning (eller motsvarigheten till **Utforskaren** på enheten). Här är stegen:

1. Anslut Android-enheten till datorn med USB-kabeln.
2. Leta efter en mapp med namnet på din enhet på datorn. I den katalogen söker du efter `Android Device\Phone\Android\data\com.microsoft.windowsintune.companyportal`.
3. Öppna mappen Filer i mappen `com.microsoft.windowsintune.companyportal` och öppna `OMADMLog_0`.
3. Sök efter `AppConfigHelper` för att leta upp meddelanden relaterade till appkonfigurationen. Resultatet ser ut ungefär så här:

    `2019-06-17T20:09:29.1970000       INFO   AppConfigHelper     10888  02256  Returning app config JSON [{"ApplicationConfiguration":[{"Name":"com.microsoft.intune.mam.managedbrowser.BlockListURLs","Value":"https:\/\/www.aol.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.bookmarks","Value":"Outlook Web|https:\/\/outlook.office.com||Bing|https:\/\/www.bing.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.homepage","Value":"https:\/\/www.arstechnica.com"}]},{"ApplicationConfiguration":[{"Name":"IntuneMAMUPN","Value":"AdeleV@M365x935807.OnMicrosoft.com"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled","Value":"false"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled.UserChangeAllowed","Value":"false"}]}] for user User-875363642`
    
## <a name="graph-api-support-for-app-configuration"></a>Graph API har stöd för appkonfiguration

Du kan använda Graph API för att utföra de här appkonfigurationsuppgifterna. Mer information finns i [Graph API-referens för MAM-riktad konfiguration](https://docs.microsoft.com/graph/api/resources/intune-shared-targetedmanagedappconfiguration?view=graph-rest-beta). Mer information om Intune och Graph finns i [Arbeta med Intune i Microsoft Graph](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-beta).

## <a name="troubleshooting"></a>Felsökning

### <a name="using-logs-to-show-a-configuration-parameter"></a>Använda loggar för att visa en konfigurationsparameter
När loggarna visar en konfigurationsparameter som har bekräftats tillämpas men inte verkar fungera kan det finnas ett problem med konfigurationens implementering av apputvecklaren. Om du kontaktar apputvecklaren först eller läser deras kunskapsbas kan du undvika att behöva ringa Microsofts support. Om det är problem med hur konfigurationen hanteras i en app måste det åtgärdas i en framtida uppdaterad version av den appen.

## <a name="next-steps"></a>Nästa steg

### <a name="managed-devices"></a>Hanterade enheter

- Lär dig hur du använder appkonfiguration med iOS/iPadOS-enheter.  Mer information finns i [Lägg till konfigurationsprinciper för hanterade iOS/iPadOS-mobilappar](app-configuration-policies-use-ios.md).
- Lär dig hur du använder appkonfiguration med Android-enheter.  Se [Lägg till konfigurationsprinciper för hanterade Android-enheter](app-configuration-policies-use-android.md).

### <a name="managed-apps"></a>Hanterade appar

- Lär dig hur du använder appkonfiguration med hanterade appar. Se [Lägg till appkonfigurationsprinciper för hanterade appar utan enhetsregistrering](app-configuration-policies-managed-app.md).
