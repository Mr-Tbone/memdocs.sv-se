---
title: Lägg till appar i Microsoft Intune
titleSuffix: ''
description: Läs mer om att lägga till appar i Microsoft Intune så att du kan tilldela appar till användare och enheter. Intune stöder en mängd olika apptyper.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0cf2096b4a8862a29d47bc05aa29f0cbb48792b
ms.sourcegitcommit: fb84a87e46f9fa126c1c24ddea26974984bc9ccc
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/22/2020
ms.locfileid: "82023256"
---
# <a name="add-apps-to-microsoft-intune"></a>Lägg till appar i Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Innan du kan konfigurera, tilldela, skydda eller övervaka appar måste du lägga till dem i Microsoft Intune.

De som använder appar och enheter på företaget (personalen på ditt företag) kan ha flera appkrav. Innan du lägger till appar i Intune och gör dem tillgängliga för personalen kan det vara bra att utvärdera och förstå ett par grundläggande saker om appar. Det finns olika typer av appar som är tillgängliga för Intune. Du måste fastställa vilka krav företagsanvändarna har på appen, till exempel vilka plattformar och funktioner som behövs. Du måste bestämma om du vill använda Intune för att hantera enheterna (inklusive appar) eller om du vill låta Intune hantera apparna utan hantering av enheterna. Slutligen måste du fastställa vilka appar och funktioner som personalen behöver och vilka som behöver dem. Informationen i den här artikeln hjälper dig att komma igång.

## <a name="app-types-in-microsoft-intune"></a>Apptyper i Microsoft Intune

Intune stöder en mängd olika apptyper. De tillgängliga alternativen skiljer sig åt för varje apptyp. I Intune kan du lägga till och tilldela följande apptyper:

| Apptyper | Installation | Uppdateringar |
|---|---|---|
| Appar från butiken (Store-appar) | Intune installerar apparna på enheten.  | Uppdateringar av appar sker automatiskt. |
| Appar om skrivits internt (verksamhetsspecifika) | Intune installerar appen på enheten (du tillhandahåller installationsfilen). | Du måste uppdatera appen. |
| Appar som är inbyggda (inbyggda appar) | Intune installerar apparna på enheten.  | Uppdateringar av appar sker automatiskt. |
| Appar på webben (webblänk) | Intune skapar en genväg till webbappen på enhetens startskärm. | Uppdateringar av appar sker automatiskt. |

### <a name="specific-app-type-details"></a>Information för specifika apptyper
 
I följande tabell visas de specifika apptyperna och hur du kan lägga till dem i Intune-fönstret **Lägg till app**:

| **Appspecifik typ** | **Allmän typ** | **Appspecifika procedurer** |
| --- | --- | --- |
| Android Store-appar  | Store-app  | Välj **Android** som **apptyp** och ange appens webbadress på Google Play. |
| Android Enterprise-appar  | Store-app  | Välj **Android** som **apptyp** och ange appens hanterade webbadress på Google Play. <sup>1</sup> |
| Store-appar för iOS/iPadOS  | Store-app  | Välj **iOS** som **apptyp**, sök efter appen och välj appen i Intune. |
| Windows Phone 8.1 Store-appar  | Store-app  | Välj **Windows Phone 8.1** som **apptyp** och ange appens webbadress på Microsoft Store. |
| Microsoft Store-appar  | Store-app  | Välj **Windows** som **apptyp** och ange appens webbadress på Microsoft Store. |
| Google Play-appar som hanteras | Store-app  | Välj **Hanterad Google Play** som **apptyp**, sök efter appen och välj appen i Intune. |
| Office 365-appar för Windows 10  | Store-app (Office 365) | Välj **Windows 10** under **Microsoft 365 Apps** som **apptyp** och välj sedan den Office 365-app du vill installera.  |
| Office 365-appar för macOS | Store-app (Office 365) | Välj **macOS** under **Microsoft 365 Apps** som **apptyp** och välj sedan Office 365-serien. |
| Microsoft Edge version 77 och senare för Windows 10 | Store-app | Välj **Windows 10** under **Microsoft Edge, version 77 och senare** som **apptyp**. |
| Microsoft Edge version 77 och senare för Windows 10 | Store-app | Välj **macOS** under **Microsoft Edge, version 77 och senare** som **apptyp**. |
| Verksamhetsspecifika appar för Android | Verksamhetsspecifik app | Välj **Branschspecifik app** som **apptyp**, välj **Appaketfil** och ange sedan en Android-installationsfil med tillägget **.apk**.  |
| Verksamhetsspecifika appar för iOS/iPadOS | Verksamhetsspecifik app | Välj **Branschspecifik app** som **apptyp**, välj **Appaketfil** och ange sedan en iOS/iPadOS-installationsfil med tillägget **.ipa**.  |
| Windows Phone LOB-appar | Verksamhetsspecifik app | Välj **Branschspecifik app** som **apptyp**, välj **Appaketfil** och ange sedan en Windows Phone-installationsfil med tillägget **.xap**.  |
| Verksamhetsspecifika Windows-appar | Verksamhetsspecifik app | Välj **Branschspecifik** app som apptyp, välj **Appaketfil** och ange sedan en Windows-installationsfil med tillägget **.msi**, **.appx**, **.appxbundle**, **.msix** eller **.msixbundle**. |
| Inbyggd iOS/iPadOS-app  | Inbyggd app | Välj **Inbyggd app** som **apptyp** och välj sedan den inbyggda appen i listan med appar.  |
| Inbyggd Android-app  | Inbyggd app | Välj **Inbyggd app** som **apptyp** och välj sedan den inbyggda appen i listan med appar.  |
| Webbappar  | Webbapp  | Välj **Webblänk** som **apptyp** och ange sedan en giltig URL som pekar till webbappen.  |
| Android Enterprise-systemprogram  | Store-app  | Välj **Android Enterprise-systemapp** som **apptyp** och ange sedan appens namn, utgivare och paketfil.  |
| Windows-app (Win32)  | Verksamhetsspecifik app  | Välj **Windows-app (Win32)** som **apptyp**, välj **appaketfilen** och välj sedan en installationsfil med tillägget **.intunewin**.  |
| macOS LOB-appar | Verksamhetsspecifik app  | Välj **Line-of-business** som **apptyp**, välj **appaketfilen** och välj sedan en installationsfil med tillägget **.intunemac**.  |


<sup>1</sup> Mer information om Android Enterprise- och Android Work-profiler finns i [Förstå licensierade appar](apps-add.md#understanding-licensed-apps) nedan.

Du kan lägga till en app i Microsoft Intune genom att välja **Appar** > **Alla appar** > **Lägg till**. Fönstret **Välj apptyp** visas där du kan välja **Apptyp**. 

>[!TIP]
> En verksamhetsspecifik app är en app som du lägger till från en appinstallationsfil. För att exempelvis installera en verksamhetsspecifik iOS/iPadOS-app lägger du till appen genom att välja **Branschspecifik app** som **Apptyp** i fönstret **Välj apptyp**. Välj sedan appaketfilen (tillägget .ipa). Dessa typer av appar är vanligen skrivna internt.

## <a name="assess-app-requirements"></a>Utvärdera appkrav
Som IT-administratör ska du inte bara bestämma vilka appar gruppen måste använda, utan du ska även bestämma vilka funktioner som behövs för varje grupp och undergrupp. För varje app ska du besluta vilka plattformar som behövs, vilka användargrupper som behöver appen, vilka konfigurationsprinciper som ska gälla för grupperna och vilka skyddsprinciper som ska gälla.  

Du måste dessutom bestämma om du ska fokusera på focus Mobile Device Management (MDM) eller enbart på Mobile Application Management (MAM). 

Det är praktiskt att använda Intune för att hantera enheten med MDM när:
- Användare behöver en WiFi- eller VPN-företagsanslutningsprofil för att vara produktiva.
- Användare behöver en uppsättning appar som ska push-överföras till deras enhet.
- Din organisation behöver uppfylla regler eller andra principer som ska beskriva MDM-kontroller som säkerhet eller kryptering.

Det är praktiskt att använda Intune för att hantera appar med MAM utan att hantera enheten när:
- Du vill att användare ska kunna använda sin egen enhet (BYOD).
- Du vill tillhandahålla enstaka popup-meddelanden för att informera användarna om att det finns MAM-skydd istället för kontinuerliga meddelanden på enhetsnivå.
- Du måste följa principer som kräver mindre hanteringsfunktioner på personliga enheter. Du kanske till exempel vill hantera apparnas företagsdata istället för att hantera företagsdata för hela enheten.

Mer information finns i [Jämför MDM och MAM](../fundamentals/byod-technology-decisions.md).

### <a name="determine-who-will-use-the-app"></a>Bestämma vem som ska använda appen

När du avgör vilka appar som din personal behöver, överväg att olika grupper av användare och de olika appar som de använder. Det är också bra att känna till dessa grupper efter att du har lagt till en app. När du har lagt till en app tilldelar du en grupp av användare som ska kunna använda appen. 

Du måste först bestämma vilken grupp som ska ha åtkomst till appen baserat på hur känsliga data appen innehåller. Du kanske behöver inkludera eller exkludera vissa typer av roller i organisationen. Till exempel kan endast vissa verksamhetsspecifika appar krävas för säljgruppen, medan personer som arbetar med ingenjörskonst, ekonomi, HR eller juridik kanske inte behöver använda de verksamhetsspecifika apparna. Dessutom kanske säljgruppen behöver ytterligare dataskydd och åtkomst till interna företagstjänster på sina mobila enheter. Du måste bestämma hur den här gruppen ska ansluta till resurser med appen. Kommer de data som appen kommer åt finnas i molnet eller lokalt? Och hur kommer användarna att ansluta till resurser med appen? 

Med Intune kan du också aktivera åtkomst till klientappar som kräver säker åtkomst till lokala data, t.ex. servrar för affärsappar. Den här typen av åtkomst görs normalt med [Intune-hanterade certifikat](../protect/certificates-configure.md) för åtkomstkontroll som kombineras med en VPN-gateway eller proxy av standardtyp i perimeternätverket, t.ex. Azure Active Directory-programproxy. Intunes [App Wrapping Tool och App SDK](../developer/apps-prepare-mobile-application-management.md) kan användas för att hålla kvar data i den verksamhetsspecifika appen, så att det inte går att vidareföra företagsdata till konsumentappar eller konsumenttjänster.

Använd [guiden för planering, utformning och implementering för distribution av Intune](../fundamentals/planning-guide.md) och få hjälp med att bestämma hur du ska identifiera de organisatoriska grupper som är associerade med varje användningsfall och underanvändningsfall i appen. Mer information om hur du tilldelar appar till grupper finns i [Tilldela appar till grupper med Microsoft Intune](apps-deploy.md).

### <a name="determine-the-type-of-app-for-your-solution"></a>Bestämma typ av app för en lösning

Du kan välja bland följande app-typer:
- **Appar från butiken**: Appar som har laddats upp till antingen Microsoft Store, iOS/iPadOS Store eller Android Store kallas för Store-appar. En store-apps provider underhåller och tillhandahåller uppdateringar för appen. Du väljer appen i Store-listan och lägger till den med hjälp av Intune som en app som är tillgänglig för användarna.
- **Appar som har skrivits internt (verksamhetsspecifika)** : Appar som har skapats internt kallas för verksamhetsspecifika appar (LOB). Funktionerna i den här apptypen har skapats för någon av plattformarna som stöds av Intune, som Windows, iOS/iPadOS, macOS eller Android. Din organisation skapar och förser dig med uppdateringar som en separat fil. Du ger användarna uppdateringar för appen genom att lägga till och distribuera uppdateringarna med Intune.
- **Appar på webben**: Webbappar är klientserverprogram. Servern tillhandahåller webbappen, som inkluderar användargränssnitt, innehåll och funktioner. Dessutom erbjuder moderna webbtjänstplattformar dessutom vanligen säkerhet, belastningsutjämning och andra förmåner. Den här typen av app underhålls separat på webben. Du använder Intune för att peka på den här apptypen. Du tilldelar också vilka användargrupper som ska kunna få åtkomst till den här appen. Observera att Android inte har stöd för webbappar.

När du bestämmer vilka appar som krävs för din organisation behov, bör du överväga hur apparna integrerar med molntjänster, vilka data apparna kan få åtkomst till, om apparna är tillgängliga för BYOD-användare och om apparna kräver internetåtkomst.

Mer information om vilken typ av appar din organisation behöver finns i avsnittet ”Appar” i avsnittet ”Funktionskrav” i [Skapa en design](../fundamentals/planning-guide-design.md#feature-requirements).

### <a name="understanding-app-management-and-protection-policies"></a>Förstå principer för apphantering och skydd
Med Intune kan du ändra funktionen för appar som du distribuerar för att justera dem efter företagets principer för efterlevnad och säkerhet. Med den här kontrollen kan du också bestämma hur företagets data ska skyddas. Intune-hanterade appar har en omfattande uppsättning skyddsprinciper för mobila program som:

- Begränsning av funktionerna kopiera och klistra in och spara som.
- Konfiguration av webblänkar så att de öppnas i Microsoft Edge-appen.
- Aktivering av användning av flera identiteter och villkorlig åtkomst på appnivå.

Intune-hanterade appar kan även aktivera appskydd utan att kräva registrering. På så sätt får du möjligheten att tillämpa principer för förebyggande av dataförlust utan att hantera användarens enhet. Dessutom kan du införliva hantering av mobilappar i dina mobila och verksamhetsspecifika appar med Intune App SDK och App Wrapping Tool. Mer information om verktygen finns i [Översikt över Intune App SDK](../developer/app-sdk.md).

### <a name="understanding-licensed-apps"></a>Förstå licensierade appar
Utöver att förstå webbappar, Store-appar och verksamhetsspecifika appar bör du också vara medveten om destinationen för appar för volymköpsprogram och licensierade appar som: 
- **Apples volyminköpsprogram för företag (iOS)** : I iOS/iPadOS App Store kan du köpa flera licenser för en app som du vill använda i företaget. Om du köper flera exemplar så blir det lättare att effektivt hantera appar i ditt företag. Mer information finns i [Hantera volyminköpta iOS/iPadOS-appar](vpp-apps-ios.md).
- **Android-arbetsprofil**: Hur du tilldelar appar till Android-arbetsprofilenheter skiljer sig från hur du tilldelar dem till vanliga Android-enheter. Alla appar som du installerar för Android-arbetsprofiler kommer från den hanterade Google Play-butiken. Du använder Intune för att bläddra efter de appar som du vill ha och godkänna dem. Appen visas sedan i noden **Licensierade appar** i Azure Portal och du kan hantera tilldelning av appen precis som för alla andra appar.
- **Microsoft Store för företag (Windows 10)** : I Microsoft Store för företag kan du söka efter och köpa appar till din organisation, separat eller i volym. Genom att ansluta butiken till Microsoft Intune kan du hantera volyminköpta program i Azure-portalen. Mer information finns i [Hantera appar från Microsoft Store för företag](windows-store-for-business.md).

    > [!NOTE]
    > Filnamnstillägg för Windows-appar omfattar **.msi**, **.appx**, **.appxbundle**, **.msix** och **.msixbundle**.  

## <a name="before-you-add-apps"></a>Innan du lägger till appar
Tänk på följande innan du börjar lägga till och tilldela appar:

- När du lägger till och tilldelar en app från en butik måste din användare ha ett konto med den butiken för att kunna installera appen.
- Vissa appar eller objekt som du tilldelar kan vara beroende av inbyggda iOS/iPadOS-appar. Om du till exempel tilldelar en bok från iOS/iPadOS Store måste appen iBooks finnas på enheten. Om du har tagit bort den inbyggda iBooks-appen, kan du inte använda Intune för att återinföra den.

> [!IMPORTANT]
> Om du ändrar namnet på appen via Intune i Azure Portal när du har distribuerat och installerat den kan du inte längre använda appen som mål i dina kommandon.

## <a name="cloud-storage-space"></a>Molnlagringsutrymme
Alla appar som du skapar med installationstypen Programinstallation (till exempel en verksamhetsspecifik app) måste paketeras och överföras till Microsoft Intunes molnlagring. En utvärderingsprenumeration på Intune inkluderar 2 GB molnbaserad lagring som används för att lagra hanterade appar och uppdateringar. Den totala mängden lagringsutrymme är inte begränsad med en fullständig prenumeration.

Krav för lagringsutrymme i molnet:

- Alla appinstallationsfiler måste finnas i samma mapp.
- Den maximala filstorleken för en fil som du överför är 8 GB.

  > [!NOTE]
  > Windows verksamhetsspecifika appar (LOB), inklusive Win32, Windows Universal AppX, Windows Universal AppX-paket, Windows Universal MSI X och Windows Universal MSI X-paket, har en maximal storleksgräns på 8 GB per app. Alla andra verksamhetsspecifika appar, inklusive verksamhetsspecifika appar för iOS/iPadOS, har en maximal storleksgräns på 2 GB per app.

## <a name="create-and-edit-categories-for-apps"></a>Skapa och redigera kategorier för appar

Appkategorier kan användas för att sortera appar så att användarna lättare kan hitta dem i företagsportalen. Du kan tilldela en eller flera kategorier till en app, till exempel *Utvecklarprogram* eller *Kommunikationsappar*.

När du lägger till en app i Intune ges möjlighet att välja den kategori som du önskar. Använd de plattformsspecifika avsnitten för att lägga till en app och tilldela kategorier. Använd följande procedur för att skapa och redigera dina egna kategorier:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Appar** > **Appkategorier**.  
    Fönstret **Appkategorier** visar en lista över aktuella kategorier. 
5. Gör något av följande:
    - För at lägga till en kategori i fönstret **Skapa kategori** väljer du **Lägg till**, och anger sedan ett namn på kategorin.  
    Namn kan bara anges på ett språk och de översätts inte av Intune.
    - Om du vill redigera en kategori väljer du de tre punkterna ( **...** ) bredvid kategorin och välj sedan **Fäst på instrumentpanelen** eller **Ta bort**.
6. Välj **Skapa**.

## <a name="apps-that-are-added-automatically-by-intune"></a>Appar som läggs till automatiskt av Intune

Tidigare innehöll Intune ett antal inbyggda appar för snabb tilldelning. Vi har tagit bort den här listan utifrån feedback för Intune, och de inbyggda apparna visas inte längre. Om du har redan har tilldelat några inbyggda appar kommer apparna även i fortsättningen att finnas kvar i listan över appar. Du kan fortsätta att tilldela dessa appar vid behov.

> [!NOTE]
> Vid installation av en nödvändig affärsapplikation försöker Intune installera appen genom att skicka ett installationskommando när enheten checkar in, förutsatt att appen inte kan identifieras och att appens installationsstatus inte är *Installation väntar*.

## <a name="installing-updating-or-removing-required-apps"></a>Installera, uppdatera eller ta bort obligatoriska appar

Intune installerar automatiskt om, uppdaterar eller tar bort appen inom 24 timmar i stället för att vänta på omvärderingscykeln på 7 dagar.

Intune kommer automatiskt att installera om, uppdatera eller ta bort en obligatorisk app baserat på följande villkor:
- Om en användare avinstallerar en app som du har angett som obligatorisk på slutanvändarens enhet installerar Intune automatiskt om appen enligt det här schemat.
- Om en obligatorisk app inte kan installeras eller på något sätt inte finns på enheten utvärderar Intune kompatibilitet och installerar om appen enligt det här schemat.  
- En administratör anger en app som är tillgänglig för en användargrupp och en slutanvändare installerar appen från företagsportalen på enheten. Senare uppdaterar administratören appen från v1 till v2. Intune uppdaterar appen enligt det här schemat, förutsatt att eventuell tidigare version av appen finns kvar på enheten.
- Om administratören distribuerar avinstallationsavsikt och appen finns på enheten men gick inte att avinstallera, utvärderar Intune kompatibilitet och avinstallerar appen enligt det här schemat.   

## <a name="app-installation-errors"></a>Appinstallationsfel

Mer information om installationsfel för Intune-appar finns i [Appinstallationsfel](troubleshoot-app-install.md).

## <a name="next-steps"></a>Nästa steg

Information om hur du lägger till appar för varje plattform till Intune finns i:

- [Android Store-appar](store-apps-android.md)
- [Android LOB-appar](lob-apps-android.md)
- [iOS Store-appar](store-apps-ios.md)
- [iOS LOB-appar](lob-apps-ios.md)
- [macOS LOB apps](lob-apps-macos.md)
- [Webbappar (för alla plattformar)](web-app.md)
- [Windows Phone 8.1 Store-appar](store-apps-windows-phone-8-1.md)
- [Windows Phone LOB-appar](lob-apps-windows-phone.md)
- [Microsoft Store-appar](store-apps-windows.md)
- [Windows LOB-appar](lob-apps-windows.md)
- [Office 365-appar för Windows 10](apps-add-office365.md)
- [Office 365-appar för macOS](apps-add-office365-macos.md)
- [Google Play-appar som hanteras](apps-add-android-for-work.md)
- [Microsoft Edge för Windows 10](apps-windows-edge.md)
- [Microsoft Edge för macOS](apps-edge-macos.md)
- [Inbyggda appar](apps-add-built-in.md)
- [Android Enterprise-systemprogram](apps-ae-system.md)
- [Win32-appar](apps-win32-app-management.md)
