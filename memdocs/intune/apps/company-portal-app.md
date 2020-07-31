---
title: Anpassa Intune-företagsportalens appar, Företagsportal-webbplatsen och Intune-appen
titleSuffix: Microsoft Intune
description: Läs mer om hur du kan använda företagsspecifik anpassning i Intune-företagsportsalapparna, på Företagsportal-webbplatsen och i Intune-appen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d979001f159b427314f8bc53788ccce0acd13d11
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365550"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Anpassa Intune-företagsportalens appar, Företagsportal-webbplatsen och Intune-appen

Företagsportal-appar, Företagsportal-webbplatsen och Intune-appen på Android är de ställen användarna kan få åtkomst till företagsdata och utföra vanliga uppgifter. Vanliga uppgifter kan vara att registrera enheter, installera appar och hitta information (t.ex. när det gäller att få hjälp från IT-avdelningen). Dessutom erbjuder de användarna ett säkert sätt att få åtkomst till företagets resurser. Slutanvändarupplevelsen omfattar flera olika sidor, till exempel Start, Appar, Appinformation, Enheter och Enhetsinformation. Om du snabbt vill hitta appar i företagsportalen kan du filtrera apparna på sidan appar.

## <a name="customizing-the-user-experience"></a>Anpassa användarupplevelsen

Genom att anpassa slutanvändarupplevelsen kan du skapa en välbekant miljö för dina slutanvändare. Om du vill göra detta navigerar du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Innehavaradministration** > **Anpassning**, där du kan redigera standardprincipen eller skapa upp till 10 gruppinriktade principer. De här inställningarna gäller för Företagsportal-appar, Företagsportal-webbplatsen och Intune-appen på Android.

## <a name="branding"></a>Anpassning

I följande tabell visas anpassningsinformation för slutanvändarupplevelsen:

| Fältnamn | Mer information |
|---|---|---|
| **Organisationsnamn** | Det här namnet visas i alla meddelanden i slutanvändarupplevelsen. Du kan ställa in den så att den visas i sidhuvuden och använder inställningen **Visa i sidhuvud**. Maxlängden är 40 tecken. |
| **Färg** | Välj **Standard** och välj bland fem standardfärger. Välj **Anpassad** om du vill välja en specifik färg baserat på en hexadecimal kod. |
| **Temafärg** | Ange den temafärg som ska visas i hela slutanvändarupplevelsen. Vi ställer automatiskt in textfärgen på svart eller vit, så att den visas ovanpå den valda temafärgen. |
| **Visa i sidhuvud** | Ange om slutanvändarupplevelsens sidhuvud ska visa **Organisationens logotyp och namn**, **Endast organisationens logotyp** eller **Endast organisationens namn**. I förhandsgranskningsrutorna nedan visas endast logotypen, inte namnet.  |
| **Ladda upp logotypen för temafärgsbakgrund** | Ladda upp den logotyp som du vill visa ovanpå den valda temafärgen. För bäst resultat rekommenderar vi att du laddar upp en logotyp med genomskinlig bakgrund. Du kan se hur detta kommer att se ut i förhandsgranskningsrutan under inställningen.<p>Maximal bildstorlek: 400 x 400 px<br>Maximal filstorlek:   750 KB<br>Filtyp: PNG, JPG eller JPEG |
| **Ladda upp logotyp för vit eller ljus bakgrund** | Ladda upp logotypen som du vill visa ovanpå vita eller ljusa bakgrunder. För bäst resultat rekommenderar vi att du laddar upp en logotyp med genomskinlig bakgrund. Du kan se hur detta kommer att se ut mot en vit bakgrund i förhandsgranskningsrutan under inställningen.<p>Maximal bildstorlek: 400 x 400 px<br>Maximal filstorlek: 750 KB<br>Filtyp: PNG, JPG eller JPEG |
| **Ladda upp varumärkesbild** | Ladda upp en bild som återspeglar organisationens varumärke.<p><ul><li>Rekommenderad bildbredd: Större än 1125 px (måste vara minst 650 px)</li><li>Maximal bildstorlek: 1,3 MB</li><li>Filtyp: PNG, JPG eller JPEG</li><li>Den visas på följande platser:</li><ul><li>iOS/iPadOS-företagsportalen: Bakgrundsbild på användarens profilsida.</li><li>Företagsportalens webbplats:   Bakgrundsbild på användarens profilsida.</li><li>Android Intune-app: I lådan och som bakgrundsbild på användarens profilsida.</li></ul></ul> |

> [!NOTE]
> När en användare installerar ett iOS/iPadOS-program från företagsportalen får de ett meddelande. Detta inträffar när iOS/iPadOS-appen är länkad till App Store, ett volymköpt program (VPP) eller en verksamhetsspecifik app (LOB). Användaren kan acceptera åtgärden eller tillåta hantering av appen. Meddelandet visar företagets namn. Om företagets namn inte är tillgängligt visas **företagsportalen**.

### <a name="brand-image-best-practices"></a>Metodtips för grafisk profil

Rätt grafisk profil kan stärka användarnas förtroende genom att den skapar en tydlig bild av organisationens varumärke. Här följer några tips på hur du kan hitta, välja ut och optimera bilden som ska visas upp.

- Kontakta företagets marknadsförings- eller designavdelning. De kanske redan har en godkänd uppsättning företagsanpassade varumärkesbilder. De kanske också kan hjälpa dig att optimera bilderna om det behövs.
- Överväg både stående och liggande bilder. Det bör finnas tillräckligt med bakgrund runt bildens mittpunkt. Bilden kan beskäras på olika sätt beroende på enhetens storlek, orientering och plattform.
- Undvik att använda en generisk bild. Bilden bör återspegla din organisations varumärke och vara välbekant för användarna. Om du inte har någon bild är det bättre att inte använda någon bild över huvud taget än att använda vilken bild som helst som inte är meningsfull för dina användare.
- Ta bort onödiga metadata. Bildfilen kan innehålla metadata, till exempel kameraprofil, geografisk plats, rubrik, beskrivning och så vidare. Ta bort den här informationen med hjälp av ett bildoptimeringsverktyg för att upprätthålla kvaliteten och uppfylla storleksgränsen för filer.

### <a name="brand-image-examples"></a>Exempel på varumärkesavbildning

Följande bild är ett exempel på en grafisk profil för en iPhone:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Det följande är ett exempel på den grafiska profilen i Intune-appen för Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Supportinformation

Ange din organisations supportinformation, så att anställda kan kontakta dig med frågor. Den här supportinformationen visas på sidorna **Support**, **Hjälp och support** och **Supportavdelningen** i slutanvändarupplevelsen.

| Fältnamn | Maximal längd | Mer information |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kontaktnamn | 40 | Det här är namnet på den person som användarna kommer i kontakt med när de kontaktar supporten. |
| Telefonnummer | 20 | Med det här numret kan användarna ringa och be om support. |
| E-postadress | 40 | Den här e-postadressen kan användarna använda för att skicka e-post till supporten. Du måste ange en giltig e-postadress i formatet `alias@domainname.com`. |
| Namn på webbplats | 40 | Det här är det användarvänliga namn som visas på några platser för supportwebbplatsens URL. Om du anger en supportwebbplats-URL och inget användarvänligt namn, så visas själva URL:en i slutanvändarupplevelsen.  |
| Webbplats-URL | 150 | Den supportwebbplats som användarna bör använda. Webbadressen måste anges i formatet `https://www.contoso.com`.  |
| Ytterligare information | 120 | Ta med ytterligare supportrelaterade meddelanden till användarna här. |

## <a name="configuration"></a>Konfiguration

Du kan konfigurera Företagsportal-miljön specifikt för registrering, sekretess, meddelanden, appkällor och självbetjäningsåtgärder.

### <a name="enrollment"></a>Registrering

I den här tabellen visas registreringsspecifik konfigurationsinformation:

| Fältnamn | Maximal längd | Mer information |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enhetsregistrering | E.t. | Ange om och hur användarna ska uppmanas att registrera sig för hantering av mobilenheter. Mer information finns i [Inställningsalternativ för enhetsregistrering](../apps/company-portal-app.md#device-enrollment-setting-options). |

#### <a name="device-enrollment-setting-options"></a>Alternativ för inställning av enhetsregistrering

> [!NOTE]
> Stöd för inställningen för enhetsregistrering kräver att slutanvändarna har följande Företagsportal-versioner:
> - Företagsportal på iOS/iPadOS: version 4.4 eller senare
> - Företagsportal på Android: version 5.0.4715.0 eller senare 

> [!IMPORTANT]
> Följande inställningar gäller inte för iOS/iPad-enheter som är konfigurerade att registreras med [automatisk enhetsregistrering](../enrollment/device-enrollment-program-enroll-ios.md). Oavsett hur de här inställningarna konfigureras så kommer iOS/iPad-enheter som är konfigurerade att registreras med automatisk enhetsregistrering att registreras i det inledande flödet, och användarna uppmanas att logga in när de startar Företagsportal.

|    Alternativ för enhetsregistrering    |    Beskrivning    |    Checklisteprompter    |    Meddelande    |    Enhetsstatusinformation    |    Appstatusinformation (om en app som kräver registrering)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Tillgänglig, med prompter    |    Standardupplevelsen med prompter för registrering på valfria platser.    |    Ja    |    Ja    |    Ja    |    Ja    |
|    Tillgängligt, inga prompter    |    Användaren kan registrera sig via statusen i enhetsinformationen för den aktuella enheten eller från appar som kräver registrering.    |    Nej    |    Nej    |    Ja    |    Ja    |
|    Ej tillgänglig    |    Det finns inget sätt för användarna att registrera sig.    |    Nej    |    Nej    |    Nej    |    Nej    |

### <a name="privacy"></a>Sekretess

I den här tabellen visas sekretesspecifik konfigurationsinformation:

| Fältnamn | Maximal längd | Mer information |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL för sekretesspolicy | 79 | Ange din organisations sekretesspolicy så att den visas när användarna klickar på sekretesslänkar. Du måste ange en giltig URL i formatet `https://www.contoso.com`. |
| Sekretessmeddelande i Företagsportal för iOS/iPad | 520 | Behåll **Standard** eller ange ett **Anpassat** meddelande som listar de objekt din organisation inte kan se på hanterade iOS/iPad-enheter. Du kan använda Markdown när du ska lägga till punkter, fet stil, kursiv stil och länkar. Användarna ser också en lista med saker som din organisation kan se och göra, men den listan genereras automatiskt av Intune och kan inte anpassas. |

### <a name="device-ownership-notification"></a>Avisering om filägarskap

I den här tabellen visas meddelandespecifik konfigurationsinformation:

| Fältnamn | Maximal längd | Mer information |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Skicka ett push-meddelande till användarna när typen av enhetsägande ändras från privat till företag (endast Android och iOS/iPadOS) | E.t. | Skicka ett push-meddelande till användarna av företagsportalsappen (både Android och iOS) när deras ägarskapstyp ändras från personlig till företag. Som standard är push-meddelandet inställt på av. När ägarskapet för enheten är inställt på företagsägarskap har Intune större åtkomst till enheten, som innehåller fullständig app-inventering, FileVault-nyckelrotering, hämtning av telefonnummer och ett urval av fjärråtgärder. Mer information finns i [Ändra enhetsägande](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="app-sources"></a>Appkällor

Du kan välja vilka ytterligare appkällor som ska visas i Företagsportal. I den här tabellen visas konfigurationsinformation specifik för appkällor:

| Fältnamn | Maximal längd | Mer information |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Azure AD Enterprise-program | E.t. | Välj om du vill **Dölja** eller **Visa** **Azure AD Enterprise-program** i Företagsportal för varje slutanvändare. Mer information finns i [Inställningsalternativ för appkällor](../apps/company-portal-app.md#app-source-setting-options). |
| Office Online-program | E.t. | Välj om du vill **Dölja** eller **Visa** **Office Online-program** i Företagsportal för varje slutanvändare. Mer information finns i [Inställningsalternativ för appkällor](../apps/company-portal-app.md#app-source-setting-options). |

#### <a name="app-source-setting-options"></a>Inställningsalternativ för appkällor

> [!NOTE]
> På webbplatsen Företagsportal kan du initialt visa appar från andra Microsoft-tjänster.

Du kan dölja eller visa **Azure AD Enterprise-program** och **Office Online-program** i Företagsportal för varje slutanvändare. **Visa** gör att Företagsportal visar hela programkatalogen från de valda Microsoft-tjänster som har tilldelats till användaren. **Azure AD Enterprise-program** registreras och tilldelas via [Azure-portalen](https://portal.azure.com). **Office Online-program** tilldelas med de licenskontroller som är tillgängliga i [administrationscentret för M365](https://admin.microsoft.com). Du hittar den här konfigurationsinställningen i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) genom att välja **Administration av klientorganisation** > **Anpassning**. Som standard är **Dölj** valt för alla ytterligare appkällor. 

### <a name="customizing-user-self-service-actions-for-the-company-portal"></a>Anpassa självbetjäningsåtgärder för användare i Företagsportal

Du kan anpassa vilka självbetjäningsåtgärder som visas för slutanvändare i appen Företagsportal och på webbplatsen. För att förhindra oavsiktliga enhetsåtgärder kan du konfigurera inställningarna för appen Företagsportal genom att välja **Administration av klientorganisation** > **Anpassning**. 

Följande alternativ är tillgängliga:
- Dölj knappen **Ta bort** på Windows-företagsenheter.
- Dölj knappen **Återställ** på Windows-företagsenheter.
- Dölj knappen **Ta bort** på iOS/iPadOS-företagsenheter.
- Dölj knappen **Återställ** på iOS/iPadOS-företagsenheter.

> [!NOTE]
> De här åtgärderna kan användas till att begränsa enhetsåtgärder i appen Företagsportal och på webbplatsen, och implementerar inte några policyer för enhetsbegränsning. Om du vill förhindra att användare fabriksåterställer eller tar bort MDM från inställningarna måste du konfigurera policyer för enhetsbegränsning. 

## <a name="opening-web-company-portal-applications"></a>Öppna appar i Företagsportal på webben
Om slutanvändaren har appen Företagsportal installerad visas en dialogruta för appar i Företagsportal på webben där användaren kan välja att öppna appen utanför webbläsaren. Om appen inte finns med i sökvägen för appen Företagsportal öppnar Företagsportal startsidan. Om appen finns med i sökvägen öppnar Företagsportal den aktuella appen. 

När användaren väljer Företagsportal öppnas motsvarande sida i appen när URI-sökvägen är något av följande:

- `/apps` – Företagsportal på webben öppnar sidan Appar med samtliga appar.
- `/apps/[appID]` – Företagsportal på webben öppnar sidan Information för motsvarande app.
- *URI-sökvägen är en annan eller oväntad* – Företagsportal på webben visar startsidan.

Om användaren inte har installerat appen Företagsportal öppnas Företagsportal på webben.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Företagsportal-härledda autentiseringsuppgifter för iOS/iPadOS-enheter

Intune stöder PIV- (Personal Identity Verification) och CAC-härledda (Common Access Card) autentiseringsuppgifter i partnerskap med autentiseringsuppgiftsprovidrarna DISA Purebred, Entrust Datacard och Intercede. Slutanvändare går igenom ytterligare steg efter registreringen av sin iOS/iPadOS-enhet för att verifiera sin identitet i företagsportalappen. Härledda autentiseringsuppgifter aktiveras för användare genom att en autentiseringsuppgiftsprovider först konfigureras för din klientorganisation. Därefter anges en profil som mål som använder härledda autentiseringsuppgifter till användare eller enheter.

> [!NOTE]
> Användaren får instruktioner om härledda autentiseringsuppgifter baserat på den länk som du har angett via Intune.

Mer information om härledda autentiseringsuppgifter för iOS/iPadOS-enheter finns i [Använda härledda autentiseringsuppgifter i Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-the-company-portal"></a>Mörkt läge för företagsportalen

Mörkt läge är tillgängligt för företagsportalen i iOS/iPadOS, macOS och Windows. Användarna kan ladda ned appar, hantera sina enheter och få IT-support i valfritt färgschema baserat på enhetsinställningarna. Företagsportalen i iOS/iPadOS, macOS och Windows matchar automatiskt slutanvändarens enhetsinställningar för mörkt eller ljust läge.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Kortkommandon för Windows-företagsportalen

Slutanvändare kan utlösa navigerings-, app- och enhetsåtgärder i Windows-företagsportalen med hjälp av kortkommandon (acceleratorer).

Följande kortkommandon är tillgängliga i Windows-företagsportalappen.

| Område | Beskrivning | Kortkommando |
|--------------------|----------------|-------------------|
| Navigeringsmenyn | Navigering | Alt+M |
|  | Hem | Alt+H |
|  | Alla appar | Alt+A |
|  | Installerade appar | Alt+I |
|  | Skicka feedback | Alt+F |
|  | Min profil | Alt+U |
|  | Inställningar | Alt+T |
| Start – Enhetspanel | Byt namn | F2 |
|  | Ta bort | CTRL + D eller ta bort |
|  | Kontrollera åtkomst | CTRL + M eller F9 |
| Information om enhet | Byt namn | F2 |
|  | Ta bort | CTRL + D eller ta bort |
|  | Kontrollera åtkomst | CTRL + M eller F9 |
| Appinformation | Installera | Ctrl + I |
| Egenskaper | Tillgänglig | Ctrl+D |

Slutanvändarna kommer också att kunna se tillgängliga genvägar i Windows-företagsportalens app.

![Skärmbild av tillgängliga genvägar i Windows-företagsportalen](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Åtgärder för självbetjäningsenhet för användare från företagsportalen

Användare kan utföra åtgärder på sina lokala eller fjärranslutna enheter via appen Företagsportal, webbplatsen Företagsportal eller Intune-appen i Android. De åtgärder som en användare kan utföra varierar beroende på enhetens plattform och konfiguration. I samtliga fall kan fjärrenhetsåtgärder endast utföras av enhetens primära användare.  

Här är några av de tillgängliga självbetjäningsåtgärderna:

- **Dra tillbaka** – tar bort enheten från Intune-hantering. I appen och webbplatsen för företagsportalen visas detta som **Ta bort**.
- **Rensa** – den här åtgärden startar en återställning av enheten. På företagsportalens webbplats visas detta som **Återställ** eller **Återställ till fabriksinställningar** i företagsportalappen för iOS/iPadOS.
- **Byt namn** – den här åtgärden ändrar enhetsnamnet som användaren kan se i företagsportalen. Namnet ändras inte på den lokala enheten utan endast i företagsportalen.
- **Synkronisera** – den här åtgärden startar en enhetsincheckning med Intune-tjänsten. Detta visas som **Kontrollera status** i företagsportalen.
- **Fjärrlåsning** – detta låser enheten och kräver en PIN-kod för att låsa upp den.
- **Återställ lösenord** – den här åtgärden används för att återställa enhetens lösenord. På iOS/iPadOS-enheter tas lösenordet bort och slutanvändaren måste ange ett nytt lösenord i inställningarna. På Android-enheter som stöds skapas ett nytt lösenord av Intune som visas tillfälligt i företagsportalen.
- **Nyckelåterställning** – Den här åtgärden används för att återställa en personlig återställningsnyckel för krypterade macOS-enheter från företagsportalens webbplats. 

Om du vill anpassa vilka självbetjäningsåtgärder som är tillgängliga för användare kan du läsa [Anpassa självbetjäningsåtgärder för användare i Företagsportal](../apps/company-portal-app.md#customizing-user-self-service-actions-for-the-company-portal).

### <a name="self-service-actions"></a>Självbetjäningsåtgärder

Vissa plattformar och konfigurationer tillåter inte självbetjäning av enhetsåtgärder. I tabellen nedan finns mer information om självbetjäningsåtgärder:

| Action | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Pensionera | Tillgängligt<sup>(1)</sup> | Tillgänglig<sup>(9)</sup> | Tillgänglig | Tillgängligt<sup>(7)</sup> |
| Rensning | Tillgänglig | Tillgänglig<sup>(5)</sup><sup>(9)</sup> | NA | Tillgängligt<sup>(7)</sup> |
| Byt namn <sup>(4)</sup> | Tillgänglig | Tillgänglig | Tillgänglig | Tillgänglig |
| Synkronisera | Tillgänglig | Tillgänglig | Tillgänglig | Tillgänglig |
| Fjärrlåsning | Endast på Windows Phone | Tillgänglig | Tillgänglig | Tillgänglig |
| Återställ lösenord | Endast på Windows Phone | Tillgängligt<sup>(8)</sup> | NA | Tillgängligt<sup>(6)</sup> |
| Nyckelåterställning | NA | NA | Tillgängligt<sup>(2)</sup> | NA |

<sup>(1) </sup> **Dra tillbaka** är alltid blockerat på Azure AD-anslutna Windows-enheter.<br>
<sup>(2) </sup> **Nyckelåterställning** för MacOS är endast tillgängligt via webbportalen.<br>
<sup>(3) </sup> Alla fjärråtgärder inaktiveras om du registrerar med en enhetsregistreringshanterare.<br>
<sup>(4)</sup> **Byt namn** ändrar endast enhetsnamnet i företagsportalappen eller i webbportalen, inte på enheten.<br>
<sup>(5)</sup> **Rensa** är inte tillgängligt på användarregistrerade iOS/iPadOS-enheter.<br>
<sup>(6) </sup> **Återställ lösenord** stöds inte på vissa Android- och Android Enterprise-konfigurationer. För mer information, se [Återställa eller ta bort ett enhetslösenord i Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7) </sup> **Dra tillbaka** och **Rensa** är inte tillgängliga i scenarier för Android Enterprise-enhetsägare (COPE, COBO, COSU).<br>
<sup>(8)</sup> **Återställ lösenord** stöds inte på användarregistrerade iOS/iPadOS-enheter.<br>
<sup>(9)</sup>Alla iOS/iPadOS-enheter med automatisk enhets registrering (tidigare DEP) har alternativen **Ta ur bruk** och **Rensa** inaktiverade.

### <a name="app-logs"></a>Apploggar

Om du använder Azure Government har slutanvändarna tillgång till apploggar som hjälper dem att avgöra hur de ska dela när de inleder processen för att få hjälp med ett problem. Om du inte använder Azure Government skickar företagsportalen apploggar direkt till Microsoft när användaren initierar processen för att få hjälp med ett problem. När apploggarna skickas till Microsoft blir det enklare att felsöka och lösa problem.

> [!NOTE]
> I enlighet med Microsoft och Apples policy säljer vi inte några data som samlas in av vår tjänst till någon tredje part av någon anledning.

## <a name="next-steps"></a>Nästa steg

- [Konfigurera din organisations logotyp och varumärkesfärg för nya flikar i Microsoft Edge för iOS och Android](manage-microsoft-edge.md#organization-logo-and-brand-color)
- [Lägga till appar](apps-add.md)
