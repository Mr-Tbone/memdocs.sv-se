---
title: Microsoft Intune App SDK Xamarin-bindningar
description: Med Intune App SDK Xamarin-bindningar kan du använda Intunes appskyddsprincip i iOS- och Android-appar som skapats med Xamarin.
keywords: sdk, Xamarin, intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 275d574b-3560-4992-877c-c6aa480717f4
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: b29069d4543d4abb4bc403c446441e181d963bdd
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79345565"
---
# <a name="microsoft-intune-app-sdk-xamarin-bindings"></a>Microsoft Intune App SDK Xamarin-bindningar

> [!NOTE]
> Börja gärna med att läsa artikeln [Komma igång med Intune App SDK](app-sdk-get-started.md). Den här guiden beskriver hur du förbereder dig för integreringen på de plattformar som stöds.

## <a name="overview"></a>Översikt
Med [Intune App SDK Xamarin-bindningar](https://github.com/msintuneappsdk/intune-app-sdk-xamarin) kan du använda [Intunes appskyddsprincip](../apps/app-protection-policy.md) i iOS- och Android-appar som skapats med Xamarin. Bindningarna hjälper utvecklare att enkelt bygga in appskyddsfunktioner för Intune i Xamarin-baserade appar.

Med Microsoft Intune App SDK Xamarin-bindningar kan du inkludera Intunes appskyddsprinciper (även kallade APP- eller MAM-principer) i dina appar som utvecklats med Xamarin. Ett MAM-aktiverat program är ett program som är integrerat med Intune App SDK. Det kan användas av IT-administratörer för att distribuera appskyddsprinciper till din mobilapp om Intune aktivt hanterar appen.

## <a name="whats-supported"></a>Vad stöds?

### <a name="developer-machines"></a>Datorer för utvecklare
* Windows (Visual Studio version 15.7+)
* macOS

### <a name="mobile-app-platforms"></a>Plattformar för mobilappar
* Android
* iOS

### <a name="intune-mobile-application-management-scenarios"></a>Scenarion för Intune Mobile Application Management

* Intune APP-WE (utan enhetsregistrering)
* Intune MDM-registrerade enheter
* EMM-registrerade enheter från tredje part

Xamarin-appar som skapats med Intune App SDK Xamarin-bindningar kan nu ta emot Intunes appskyddsprinciper på både MDM-registrerade Intune-enheter och oregistrerade enheter.

## <a name="prerequisites"></a>Förutsättningar

Granska [licensvillkoren](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20Xamarin%20Component.pdf). Skriv ut och behåll en kopia av licensvillkoren för framtida referens. Genom att ladda ned och använda Intune App SDK Xamarin-bindningar godkänner du licensvillkoren. Om du inte godkänner dem ska du inte använda programvaran.

Intune SDK använder [Active Directory Authentication Library (ADAL)](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) för [autentisering](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) och villkorsstyrda startscenarier som kräver att apparna har konfigurerats med [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/). 

Om programmet redan har konfigurerats för att använda ADAL eller MSAL, och har ett eget anpassat klient-ID som används för att autentisera med Azure Active Directory, ser du till att stegen för att ge Xamarin-appen behörigheter till Intune MAM-tjänsten (hantering av mobilprogram) följs. Följ instruktionerna i avsnittet [Ge din app åtkomst till Intune-appskyddstjänsten](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional) i [guiden Komma igång med Intune-SDK:n](app-sdk-get-started.md).

## <a name="security-considerations"></a>Säkerhetsöverväganden

För att förhindra eventuell förfalskning, avslöjande av information och privilegieangrepp:

* Se till att Xamarin-apputveckling utförs på en säker arbetsstation.
* Se till att bindningarna kommer från en giltig Microsoft-källa:
  * [MS Intune App SDK NuGet Profile](https://www.nuget.org/profiles/msintuneappsdk)
  * [Intune App SDK Xamarin GitHub Repository](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)
* Konfigurera NuGet-konfigurationen för ditt projekt för att lita på signerade, oförändrade NuGet-paket.
Mer information finns i [Installera signerade paket](https://docs.microsoft.com/nuget/consume-packages/installing-signed-packages).
* Skydda den utdatakatalog som innehåller Xamarin-appen. Fundera på att i stället använda en katalog på användarnivå för utdatan.


## <a name="enabling-intune-app-protection-polices-in-your-ios-mobile-app"></a>Aktivera Intune-appskyddsprinciper i din iOS-mobilapp
1. Lägg till [Microsoft.Intune.MAM.Xamarin.iOS NuGet-paketet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.iOS) i ditt Xamarin.iOS-projekt.
2. Följ de allmänna steg som krävs för att integrera Intune App SDK i en mobila iOS-app. Du kan börja med steg 3 av integrationsinstruktionerna från [Utvecklingsguide för Intune App SDK för iOS](app-sdk-ios.md#build-the-sdk-into-your-mobile-app). Du kan hoppa över det sista steget i avsnittet om att köra IntuneMAMConfigurator, eftersom detta verktyg ingår i paketet Microsoft.Intune.MAM.Xamarin.iOS och körs automatiskt under byggtiden.
    **Viktigt**: Aktivering av nyckelringsdelning för en app skiljer sig något åt mellan Visual Studio och Xcode. Öppna appens .plist för rättigheter och kontrollera att alternativet ”Aktivera nyckelringar” är aktiverat och att lämpliga delningsgrupper för nyckelringar har lagts till i avsnittet. Kontrollera sedan att .plist för rättigheter har angetts i fältet ”anpassade rättigheter” i projektets alternativ ”iOS-paketsignering” för alla lämpliga kombinationer av konfiguration/plattform.
3. När bindningarna har lagts till och appen är korrekt konfigurerad, kan din app börja använda Intune SDK:s API:er. Om du vill göra detta, måste du inkludera följande namnrymd:

      ```csharp
      using Microsoft.Intune.MAM;
      ```

4. För att kunna ta emot skyddsprinciper, måste appen registreras i Intune MAM-tjänsten. Om din app inte använder [Azure Active Directory Authentication Library](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) (ADAL) eller [Microsoft Authentication Library](https://www.nuget.org/packages/Microsoft.Identity.Client) (MSAL) för att autentisera användare, och du vill att Intune SDK ska hantera autentisering, bör din app tillhandahålla användarens UPN för IntuneMAMEnrollmentManagers LoginAndEnrollAccount-metod:

      ```csharp
       IntuneMAMEnrollmentManager.Instance.LoginAndEnrollAccount([NullAllowed] string identity);
      ```

      Appar kan skicka null om användarens UPN är okänt vid tidpunkten för anropet. I det här fallet uppmanas användare att ange sin e-postadress och sitt lösenord.
      
      Om appen redan använder ADAL eller MSAL för att autentisera användare kan du konfigurera en upplevelse med enkel inloggning (SSO) mellan din app och Intune SDK. Först behöver du åsidosätta de AAD-standardinställningar som används av Intune SDK med inställningarna för din app. Du kan göra detta via i ordlistan IntuneMAMSettings i appens Info.plist, såsom anges i [Intune App SDK för iOS Developer Guide](app-sdk-ios.md#configure-settings-for-the-intune-app-sdk) eller så kan du använda med kod via AAD-åsidosättningsegenskaper för IntuneMAMSettings-klassen. Metoden Info.plist rekommenderas för program vars ADAL-inställningar är statiska medan egenskaper för åsidosättning rekommenderas för program som fastställer dessa värden vid körning. När alla inställningar för enkel inloggning har konfigurerats bör din app tillhandahålla användarens UPN för IntuneMAMEnrollmentManagers RegisterAndEnrollAccount-metod när den har autentiserats:

      ```csharp
      IntuneMAMEnrollmentManager.Instance.RegisterAndEnrollAccount(string identity);
      ```

      Appar kan fastställa resultatet av ett registreringsförsök genom att implementera metoden EnrollmentRequestWithStatus i en underklass av IntuneMAMEnrollmentDelegate och ange IntuneMAMEnrollmentManagers Delegate-egenskap till en instans av den klassen. 

      Vid en lyckad registrering kan appar fastställa UPN för det registrerade kontot (om det tidigare var okänt) genom att köra frågor mot följande egenskap: 

      ```csharp
       string enrolledAccount = IntuneMAMEnrollmentManager.Instance.EnrolledAccount;
      ```      
### <a name="sample-applications"></a>Exempelprogram
Exempelprogram som lyfter fram MAM-funktioner i Xamarin.iOS-appar finns på [GitHub](https://github.com/msintuneappsdk/sample-intune-xamarin-ios).

> [!NOTE] 
> Det finns ingen ommappning för iOS/iPadOS. Integrering i en Xamarin.Forms-app bör vara samma som för ett vanligt Xamarin.iOS-projekt. 

## <a name="enabling-intune-app-protection-policies-in-your-android-mobile-app"></a>Aktivera skyddsprinciper för Intune-appar i din Android-mobilapp
1. Lägg till [Microsoft.Intune.MAM.Xamarin.Android NuGet-paketet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.Android) i ditt Xamarin.Android-projekt.
    1. För en Xamarin.Forms-app lägger du även till [Microsoft.Intune.MAM.Remapper.Tasks NuGet-paketet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Remapper.Tasks) i Xamarin.Android-projektet. 
2. Följ de allmänna stegen som krävs för att [integrera Intune App SDK](app-sdk-android.md) med en Android-mobilapp och läs det här dokumentet för ytterligare information.

### <a name="xamarinandroid-integration"></a>Xamarin.Android integration

En fullständig översikt över integreringen av Intune App SDK finns i [utvecklarhandboken för Microsoft Intune App SDK för Android](app-sdk-android.md). När du läser handboken och integrerar Intune App SDK med Xamarin-appen beskriver följande avsnitt skillnaderna mellan implementeringen av en intern Android-app som utvecklas i Java och en Xamarin-app som utvecklas i C#. De här avsnitten kompletterar men ersätter inte resten av handboken.

#### <a name="remapper"></a>Remapper
Från och med version 1.4428.1 kan `Microsoft.Intune.MAM.Remapper`-paketet läggas till i en Xamarin.Android-app som [versionsverktyg](app-sdk-android.md#build-tooling) för att utföra MAM-klass-, metod- och systemtjänstersättningar. Om Remapper ingår, utförs motsvarande MAM-ersättningsdelar av de metoder som har bytt namn och MAM-programavsnitt automatiskt när programmet har skapats.

För att undanta en klass från MAM-bearbetning av Remapper kan följande egenskap läggas till i dina projekts `.csproj`-fil.

```xml
  <PropertyGroup>
    <ExcludeClasses>Semicolon separated list of relative class paths to exclude from MAM-ification</ExcludeClasses>
  </PropertyGroup>
```

> [!NOTE]
> Remapper förhindrar för närvarande felsökning i Xamarin.Android-appar. Manuell integrering rekommenderas för att felsöka ditt program.

#### <a name="renamed-methods"></a>[Metoder som fått nya namn](app-sdk-android.md#renamed-methods)
I många fall har en metod som är tillgänglig i Android-klassen markerats som slutgiltig i MAM-ersättningsklassen. I detta fall tillhandahåller MAM-ersättningsklassen en metod med liknande namn (med suffixet `MAM`) som ska åsidosättas i stället. Om du härleder från `MAMActivity`, i stället för att åsidosätta `OnCreate()` och anropa `base.OnCreate()`, måste `Activity` åsidosätta `OnMAMCreate()` och anropa `base.OnMAMCreate()`.

#### <a name="mam-application"></a>[MAM-program](app-sdk-android.md#mamapplication)
Din app måste definiera en `Android.App.Application`-klass. Om du integrerar MAM manuellt måste det ärva från `MAMApplication`. Se till att din underklass är korrekt dekorerad med attributet `[Application]` och åsidosätter konstruktorn `(IntPtr, JniHandleOwnership)`.

```csharp
    [Application]
    class TaskrApp : MAMApplication
    {
    public TaskrApp(IntPtr handle, JniHandleOwnership transfer)
        : base(handle, transfer) { }
```

> [!NOTE]
> Ett problem med MAM Xamarin-bindningar kan göra att programmet kraschar när det distribueras i felsökningsläge. För att komma runt problemet måste du lägga till `Debuggable=false`-attributet i `Application`-klassen och ta bort `android:debuggable="true"`-flaggan från manifestet om den angetts manuellt.

#### <a name="enable-features-that-require-app-participation"></a>[Aktivera funktioner som kräver appmedverkan](app-sdk-android.md#enable-features-that-require-app-participation)
Exempel: Bestäm om en PIN-kod ska krävas för appen

```csharp
MAMPolicyManager.GetPolicy(currentActivity).IsPinRequired;
```

Exempel: Fastställa den primära Intune-användaren

```csharp
IMAMUserInfo info = MAMComponents.Get<IMAMUserInfo>();
return info?.PrimaryUser;
```

Exempel: Bestäm om det ska vara tillåtet att spara till enheten eller lagra i molnet

```csharp
MAMPolicyManager.GetPolicy(currentActivity).GetIsSaveToLocationAllowed(SaveLocation service, String username);
```

#### <a name="register-for-notifications-from-the-sdk"></a>[Registrera för meddelanden från SDK:n](app-sdk-android.md#register-for-notifications-from-the-sdk)
Appen måste först registreras för meddelanden från SDK:n genom att en `MAMNotificationReceiver` skapas och registreras med `MAMNotificationReceiverRegistry`. Du gör detta genom att ange önskad mottagare och typ av meddelande i `App.OnMAMCreate`, vilket illustreras i exemplet nedan:

```csharp
public override void OnMAMCreate()
{
    // Register the notification receivers
    IMAMNotificationReceiverRegistry registry = MAMComponents.Get<IMAMNotificationReceiverRegistry>();
    foreach (MAMNotificationType notification in MAMNotificationType.Values())
    {
        registry.RegisterReceiver(new ToastNotificationReceiver(this), notification);
    }
    ...
```

#### <a name="mam-enrollment-manager"></a>[MAM-registreringshanterare](app-sdk-android.md#mamenrollmentmanager)

```csharp
IMAMEnrollmentManager mgr = MAMComponents.Get<IMAMEnrollmentManager>();
```

### <a name="xamarinforms-integration"></a>Xamarin.Forms integration

För `Xamarin.Forms`-program utför `Microsoft.Intune.MAM.Remapper`-paketet MAM-klassersättning automatiskt genom att injicera `MAM`-klasser i klasshierarkin för vanliga `Xamarin.Forms`-klasser. 

> [!NOTE]
> Xamarin.Forms-integrationen ska göras utöver Xamarin.Android-integreringen som beskrivs ovan. Remapper fungerar annorlunda för Xamarin.Forms-appar, så manuella MAM-ersättningar måste fortfarande göras.

När ommappningen har lagts till i ditt projekt måste du utföra motsvarande MAM-ersättningar. Exempelvis kan `FormsAppCompatActivity` och `FormsApplicationActivity` fortsätta att användas i dina program förutsatt att `OnCreate`- och `OnResume`-åsidosättningar ersätts med MAM-motsvarigheterna `OnMAMCreate` respektive `OnMAMResume`.

```csharp
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        protected override void OnMAMCreate(Bundle savedInstanceState)
        {
            base.OnMAMCreate(savedInstanceState);
            global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
            LoadApplication(new App());
        }
```

Om ersättningarna inte görs kan du få följande kompileringsfel tills du gör ersättningarna:
* [Kompilatorfel CS0239](https://docs.microsoft.com/dotnet/csharp/misc/cs0239). Det här felet hittas oftast i det här formatet ``'MainActivity.OnCreate(Bundle)': cannot override inherited member 'MAMAppCompatActivityBase.OnCreate(Bundle)' because it is sealed``.
Det här förväntas, eftersom när ommappningen ändrar arvet för Xamarin-klasser så blir vissa funktioner `sealed`, och en ny variant av MAM läggs i stället till som åsidosättning.
* [Kompilatorfel CS0507](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0507): Det här felet uppstår ofta i följande form: ``'MyActivity.OnRequestPermissionsResult()' cannot change access modifiers when overriding 'public' inherited member ...``. När ommappningen ändrar arvet för några av Xamarin-klasserna ändras vissa av medlemsfunktionerna till `public`. Om du åsidosätter någon av dessa funktioner måste du ändra åtkomstmodifierarna för dessa åsidosättningar till `public`.

> [!NOTE]
> Ommappningen skriver om ett beroende som Visual Studio använder för automatisk komplettering med IntelliSense. Därför kan du behöva återskapa och läsa in projektet igen när ommappningen läggs till för att IntelliSense ska identifiera ändringarna korrekt.

#### <a name="troubleshooting"></a>Felsökning
* Om du stöter på en tom, vit skärm i programmet vid start kan du behöva tvinga navigeringsanropen att köras på huvudtråden.
* Intune SDK Xamarin-bindningarna stöder inte appar som använder ett plattformsoberoende ramverk, till exempel MvvmCross, på grund av konflikter mellan MvvmCross- och Intune MAM-klasser. Vissa kunder kan ha haft framgång med integreringen efter att ha flyttat sina appar till vanliga Xamarin.Forms. Vi tillhandahåller inte uttryckligen vägledning eller plugin-program för apputvecklare som använder MvvmCross.

### <a name="company-portal-app"></a>Företagsportalappen
Intune SDK Xamarin-bindningar använder sig av närvaron av Android-appen för [Företagsportal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) på enheten för att aktivera skyddsprinciper. Företagsportalen hämtar appskyddsprinciper från Intune-tjänsten. När appen initieras läser den in principen och koden för att kunna aktivera principen från företagsportalen. Användaren behöver inte vara inloggad.

> [!NOTE]
> Om Företagsportalsappen inte finns på **Android**-enheten fungerar en Intune-hanterad app som en normal app som saknar stöd för Intunes appskyddsprinciper.

Vid appskydd utan enhetsregistrering behöver användaren _**inte**_ registrera enheten med företagsportalappen.

### <a name="sample-applications"></a>Exempelprogram
Exempelprogram som markerar MAM-funktioner i Xamarin.Android- och Xamarin.Forms-appar finns på [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps).

## <a name="support"></a>Stöd
Om din organisation är en befintlig Intune-kund kan du kontakta din representant på Microsofts support för att öppna en supportbegäran och skapa ett ärende [på sidan med GitHub-ärenden](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/issues). Vi kommer att hjälpa dig så snart vi kan. 
