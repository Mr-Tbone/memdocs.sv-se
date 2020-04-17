---
title: Anpassa Intune-företagsportalens appar, Företagsportal-webbplatsen och Intune-appen
titleSuffix: Microsoft Intune
description: Läs mer om hur du kan använda företagsspecifik anpassning i Intune-företagsportsalapparna, på Företagsportal-webbplatsen och i Intune-appen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/16/2020
ms.topic: conceptual
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
ms.openlocfilehash: e6a3152966dee507cde690d9be8f5a7e210c7945
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407759"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Anpassa Intune-företagsportalens appar, Företagsportal-webbplatsen och Intune-appen

Företagsportal-appar, Företagsportal-webbplatsen och Intune-appen på Android är de ställen användarna kan få åtkomst till företagsdata och utföra vanliga uppgifter. Vanliga uppgifter kan vara att registrera enheter, installera appar och hitta information (t.ex. när det gäller att få hjälp från IT-avdelningen). Dessutom erbjuder de användarna ett säkert sätt att få åtkomst till företagets resurser. Slutanvändarupplevelsen omfattar flera olika sidor, till exempel Start, Appar, Appinformation, Enheter och Enhetsinformation. Om du snabbt vill hitta appar i företagsportalen kan du filtrera apparna på sidan appar.

## <a name="customizing-the-user-experience"></a>Anpassa användarupplevelsen

Genom att anpassa slutanvändarupplevelsen kan du skapa en välbekant miljö för dina slutanvändare. Det gör du genom att navigera till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välja **Innehavaradministratör** > **Anpassning** och sedan konfigurera de nödvändiga inställningarna. De här inställningarna gäller för Företagsportal-appar, Företagsportal-webbplatsen och Intune-appen på Android.

## <a name="branding"></a>Anpassning

I följande tabell visas anpassningsinformation för slutanvändarupplevelsen:

| Fältnamn | Mer information |
|---|---|---|
| **Organisationsnamn** | Det här namnet visas i alla meddelanden i slutanvändarupplevelsen. Du kan ställa in den så att den visas i sidhuvuden och använder inställningen **Visa i sidhuvud**. Maxlängden är 40 tecken. |
| **Färg** | Välj **Standard** och välj bland fem standardfärger. Välj **Anpassad** om du vill välja en specifik färg baserat på en hexadecimal kod. |
| **Temafärg** | Ange den temafärg som ska visas i hela slutanvändarupplevelsen. Vi ställer automatiskt in textfärgen på svart eller vit, så att den visas ovanpå den valda temafärgen. |
| **Visa i sidhuvud** | Ange om slutanvändarupplevelsens sidhuvud ska visa **Företagslogotyp och företagsnamn**, **Endast företagslogotyp** eller **Endast företagsnamn**. I förhandsgranskningsrutorna nedan visas endast logotypen, inte namnet.  |
| **Ladda upp logotypen för temafärgsbakgrund** | Ladda upp den logotyp som du vill visa ovanpå den valda temafärgen. För bäst resultat rekommenderar vi att du laddar upp en logotyp med genomskinlig bakgrund. Du kan se hur detta kommer att se ut i förhandsgranskningsrutan under inställningen.<p>Maximal bildstorlek: 400 x 400 px<br>Maximal filstorlek:   750 KB<br>Filtyp: PNG, JPG eller JPEG |
| **Ladda upp logotyp för vit eller ljus bakgrund** | Ladda upp logotypen som du vill visa ovanpå vita eller ljusa bakgrunder. För bäst resultat rekommenderar vi att du laddar upp en logotyp med genomskinlig bakgrund. Du kan se hur detta kommer att se ut mot en vit bakgrund i förhandsgranskningsrutan under inställningen.<p>Maximal bildstorlek: 400 x 400 px<br>Maximal filstorlek: 750 KB<br>Filtyp: PNG, JPG eller JPEG |
| **Ladda upp varumärkesbild** | Ladda upp en bild som återspeglar organisationens varumärke.<p><ul><li>Rekommenderad bildbredd: Större än 1 125 px (måste vara minst 650 px)</li><li>Maximal bildstorlek: 1,3 MB</li><li>Filtyp: PNG, JPG eller JPEG</li><li>Den visas på följande platser:</li><ul><li>iOS/iPadOS-företagsportalen: Bakgrundsbild på användarens profilsida.</li><li>Företagsportalens webbplats:   Bakgrundsbild på användarens profilsida.</li><li>Android Intune-app: I lådan och som bakgrundsbild på användarens profilsida.</li></ul></ul> |

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

Följande tabell tillhandahåller ytterligare konfigurationsinformation:

| Fältnamn | Maximal längd | Mer information |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL för sekretesspolicy | 79 | Ange din organisations sekretesspolicy så att den visas när användarna klickar på sekretesslänkar. Du måste ange en giltig URL i formatet `https://www.contoso.com`. |
| Sekretessmeddelande i Företagsportal för iOS/iPad | 520 | Behåll standardvärdet eller ange ett anpassat meddelande som listar de objekt som din organisation kan eller inte kan se på hanterade iOS/iPad-enheter. Du kan använda Markdown när du ska lägga till punkter, fet stil, kursiv stil och länkar. |
| Enhetsregistrering | E.t. | Ange om och hur användarna ska uppmanas att registrera sig för hantering av mobilenheter. Informationen finns nedan. |

### <a name="device-enrollment-setting-options"></a>Alternativ för inställning av enhetsregistrering

> [!NOTE]
> Stöd för inställningen för enhetsregistrering kräver att slutanvändarna har följande Företagsportal-versioner:
> - Företagsportal på iOS/iPadOS: version 4.4 eller senare
> - Företagsportal på Android: version 5.0.4715.0 eller senare 

|    Alternativ för enhetsregistrering    |    Beskrivning    |    Checklisteprompter    |    Meddelande    |    Enhetsstatusinformation    |    Appstatusinformation (om en app som kräver registrering)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Tillgänglig, med prompter    |    Standardupplevelsen med prompter för registrering på valfria platser.    |    Ja    |    Ja    |    Ja    |    Ja    |
|    Tillgängligt, inga prompter    |    Användaren kan registrera sig via statusen i enhetsinformationen för den aktuella enheten eller från appar som kräver registrering.    |    Nej    |    Nej    |    Ja    |    Ja    |
|    Ej tillgänglig    |    Det finns inget sätt för användarna att registrera sig.    |    Nej    |    Nej    |    Nej    |    Nej<sup>(1)</sup>    |

<sup>(1)</sup> **Känt ärende:** Om du konfigurerar appar till att kräva registrering vid installation och även anger enhetsregistreringen som ”Ej tillgänglig”, så kommer Företagsportal-appen på Android fortfarande att hjälpa användarna att registrera sig. Detta kommer att tas bort inom kort.

> [!NOTE]
> Om du använder Azure Government har slutanvändarna tillgång till apploggar som hjälper dem att avgöra hur de ska dela när de inleder processen för att få hjälp med ett problem. Om du inte använder Azure Government skickar företagsportalen apploggar direkt till Microsoft när användaren initierar processen för att få hjälp med ett problem. När apploggarna skickas till Microsoft blir det enklare att felsöka och lösa problem.

> [!NOTE]
> I enlighet med Microsoft och Apples policy säljer vi inte några data som samlas in av vår tjänst till någon tredje part av någon anledning.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Företagsportal-härledda autentiseringsuppgifter för iOS/iPadOS-enheter

Intune stöder PIV- (Personal Identity Verification) och CAC-härledda (Common Access Card) autentiseringsuppgifter i partnerskap med autentiseringsuppgiftsprovidrarna DISA Purebred, Entrust Datacard och Intercede. Slutanvändare går igenom ytterligare steg efter registreringen av sin iOS/iPadOS-enhet för att verifiera sin identitet i företagsportalappen. Härledda autentiseringsuppgifter aktiveras för användare genom att en autentiseringsuppgiftsprovider först konfigureras för din klientorganisation. Därefter anges en profil som mål som använder härledda autentiseringsuppgifter till användare eller enheter.

> [!NOTE]
> Användaren får instruktioner om härledda autentiseringsuppgifter baserat på den länk som du har angett via Intune.

Mer information om härledda autentiseringsuppgifter för iOS/iPadOS-enheter finns i [Använda härledda autentiseringsuppgifter i Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-iosipados-company-portal"></a>Mörkt läge för iOS/iPadOS-företagsportalen

Mörkt läge är tillgängligt för iOS/iPadOS-företagsportalen. Användarna kan ladda ned appar, hantera sina enheter och få IT-support i valfritt färgschema baserat på enhetsinställningarna. iOS/iPadOS-företagsportalen matchar automatiskt slutanvändarens enhetsinställningar för mörkt eller ljust läge.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Kortkommandon för Windows-företagsportalen

Slutanvändare kan utlösa navigerings-, app- och enhetsåtgärder i Windows-företagsportalen med hjälp av kortkommandon (acceleratorer).

Följande kortkommandon är tillgängliga i Windows-företagsportalappen.

| Område | Beskrivning | Kortkommando |
|:------------------:|:--------------:|:-----------------:|
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

Användare kan utföra åtgärder på sina lokala eller fjärranslutna enheter via företagsportalens app eller webbplats, eller via Intune-appen på Android. De åtgärder som en användare kan utföra varierar beroende på enhetens plattform och konfiguration. I samtliga fall kan fjärrenhetsåtgärder endast utföras av enhetens primära användare.

- **Dra tillbaka** – tar bort enheten från Intune-hantering. I appen och webbplatsen för företagsportalen visas detta som **Ta bort**.
- **Rensa** – den här åtgärden startar en återställning av enheten. På företagsportalens webbplats visas detta som **Återställ** eller **Återställ till fabriksinställningar** i företagsportalappen för iOS/iPadOS.
- **Byt namn** – den här åtgärden ändrar enhetsnamnet som användaren kan se i företagsportalen. Namnet ändras inte på den lokala enheten utan endast i företagsportalen.
- **Synkronisera** – den här åtgärden startar en enhetsincheckning med Intune-tjänsten. Detta visas som **Kontrollera status** i företagsportalen.
- **Fjärrlåsning** – detta låser enheten och kräver en PIN-kod för att låsa upp den.
- **Återställ lösenord** – den här åtgärden används för att återställa enhetens lösenord. På iOS/iPadOS-enheter tas lösenordet bort och slutanvändaren måste ange ett nytt lösenord i inställningarna. På Android-enheter som stöds skapas ett nytt lösenord av Intune som visas tillfälligt i företagsportalen.
- **Nyckelåterställning** – Den här åtgärden används för att återställa en personlig återställningsnyckel för krypterade macOS-enheter från företagsportalens webbplats. 

### <a name="self-service-actions"></a>Självbetjäningsåtgärder

Vissa plattformar och konfigurationer tillåter inte självbetjäning av enhetsåtgärder. I tabellen nedan finns mer information om självbetjäningsåtgärder:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Pensionera | Tillgängligt<sup>(1)</sup> | Tillgänglig | Tillgänglig | Tillgängligt<sup>(7)</sup> |
| Rensning | Tillgänglig | Tillgänglig<sup>(5)</sup> | NA | Tillgängligt<sup>(7)</sup> |
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
<sup>(8)</sup> **Återställ lösenord** stöds inte på användarregistrerade iOS/iPadOS-enheter.

## <a name="next-steps"></a>Nästa steg

- [Lägga till appar](apps-add.md)
