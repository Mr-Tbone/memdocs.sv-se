---
title: Använda Microsoft Defender ATP i Microsoft Intune – Azure | Microsoft Docs
description: Använd Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) med Intune, inklusive installation och konfiguration, publicering av dina Intune-enheter med ATP och använd en ATP-riskutvärdering för enheter med dina Intune-principer för enhetsefterlevnad och villkorsstyrd åtkomst för att skydda nätverksresurserna.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264064"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Tvinga fram kompatibilitet för Microsoft Defender ATP med villkorlig åtkomst i Intune

Du kan integrera Microsoft Defender Avancerat skydd (Microsoft Defender ATP) med Microsoft Intune som en Skydd mot mobilhot-lösning. Integrationen kan hjälpa dig att förhindra säkerhetsöverträdelser och begränsa effekten av överträdelser inom en organisation. Microsoft Defender ATP kan användas med enheter som kör Windows 10 eller senare och med Android-enheter.

För att lyckas använder du följande konfigurationer tillsammans:

- **Etablera en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP**. Med den här anslutningen kan Microsoft Defender ATP samla in data om datorrisker från de enheter du hanterar med Intune.
- **Använd en enhetskonfigurationsprofil för att publicera enheter med Microsoft Defender ATP**. Du registrerar enheter för att konfigurera som så att de kommunicerar med Microsoft Defender ATP och för att tillhandahålla data som hjälper dem att utvärdera sin risknivå.
- **Använd en efterlevnadsprincip för enheter för att ange den risknivå som du vill tillåta**. Risknivåer rapporteras av Microsoft Defender ATP. Enheter som överskrider den tillåtna risknivån anses inte uppfylla efterlevnadskraven.
- **Använd en princip för villkorsstyrd åtkomst** till att blockera användare från att komma åt företagsresurser från enheter som inte uppfyller efterlevnadskraven.

När du integrerar Intune med Microsoft Defender ATP kan du använda TVM-funktionen i Microsoft Defender ATP (Threat & Vulnerability Management) och [använda Intune till att åtgärda sårbarheter i slutpunkter som TVM identifierar](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Exempel på användning av Microsoft Defender ATP med Intune

I följande exempel får du hjälp att förklara hur dessa lösningar fungerar tillsammans för att skydda din organisation. I det här exemplet är Microsoft Defender ATP och Intune redan integrerade.

Föreställ dig en händelse där någon skickar en Word-fil med inbäddad skadlig kod till en användare i din organisation.

- Användaren öppnar den bifogade filen och aktiverar innehållet.
- En attack med utökade privilegier startar och en angripare från en fjärrdator har administratörsrättigheter till den drabbade enheten.
- Angripare har sedan via fjärranslutning tillgång till användarens andra enheter. Det här säkerhetsintrånget kan påverka hela organisationen.

Microsoft Defender ATP kan lösa säkerhetshändelser som det här scenariot.

- I vårt exempel identifierar Microsoft Defender ATP att enheten körde onormal kod, upplevde en processeskalering, infogade skadlig kod och utfärdade ett misstänkt fjärrgränssnitt.
- Baserat på dessa åtgärder från enheten klassificerar Microsoft Defender ATP [enheten som associerad med hög risk](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) och inkluderar en detaljerad rapport om misstänkt aktivitet på Microsoft Defender Security Center-portalen.

Eftersom du har en efterlevnadspolicy för Intune-enheter som anger att enheter med risknivån *Medelhög* eller *Hög* inte uppfyller efterlevnadskraven anges den angripna enheten som icke-kompatibel. Den här klassificeringen gör att din princip för villkorlig åtkomst kan aktiveras och blockera åtkomst från enheten till företagets resurser.

Du kan också använda Intune-policyn till att ändra vissa konfigurationer för Microsoft Defender ATP i Android. Mer information finns i [Konfigurera webbskydd på enheter som kör Android](#configure-web-protection-on-devices-that-run-android) längre fram i den här artikeln.

## <a name="prerequisites"></a>Krav

Om du vill använda Microsoft Defender ATP med Intune måste du ha följande konfigurerat och klart att använda:

- Licensierad klientorganisation för Enterprise Mobility + Security E3 och Windows E5 (eller Microsoft 365 Enterprise E5)
- Microsoft Intune-miljö med [Intune-hanterade](../enrollment/windows-enroll.md) Windows 10-enheter eller Android-enheter som även är Azure AD-anslutna
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) och åtkomst till Microsoft Defender Security Center (ATP-portal)

> [!NOTE]
> Microsoft Defender ATP stöds inte med Intune-appskyddsprinciper för iOS/iPadOS och Android.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Aktivera Microsoft Defender ATP i Intune

Det första steget är att skapa en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP. Detta kräver administrativ åtkomst till både Microsoft Defender Security Center och Intune.

### <a name="to-enable-microsoft-defender-atp"></a>Aktivera Microsoft Defender ATP

Du behöver bara aktivera Microsoft Defender ATP en gång per klientorganisation.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Microsoft Defender ATP** och välj sedan **Öppna Microsoft Defender Säkerhetscenter**.

   ![Välj att öppna Microsoft Defender Security Center](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. I **Microsoft Defender Security Center**:
   1. Välj **Inställningar** > **Avancerade funktioner**.
   2. För **Microsoft Intune-anslutningen**, välj **På**:

      ![Aktivera anslutningen till Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

   3. Välj **Spara inställningar**.

4. Gå tillbaka till **Microsoft Defender Avancerat skydd** i administrationscentret för Microsoft Endpoint Manager. Under **MDM-inställningar för efterlevnadsprinciper**, beroende på organisationens behov:
   - Ställ in **Anslut Windows-enheter med version 10.0.15063 och senare till Microsoft Defender ATP** som **På**
   - Ställ in **Anslut Android-enheter version 6.0.0 och senare till Microsoft Defender ATP** som **På**

5. Välj **Spara**.

> [!TIP]
> När du När du integrerar ett nytt program för Skydd mot mobilhot (MTD) i Intune och aktiverar anslutningen till Intune, skapar Intune en klassisk princip för villkorlig åtkomst i Azure Active Directory. Alla MTD-appar du integrerar, inklusive [Microsoft Defender ATP](advanced-threat-protection.md) eller något annat [MTD-partnerprogram](mobile-threat-defense.md#mobile-threat-defense-partners), skapar en ny klassisk princip för villkorsstyrd åtkomst. Dessa principer kan ignoreras, men de bör inte redigeras, tas bort eller inaktiveras.
>
> Om den klassiska principen tas bort måste du ta bort anslutningen till Intune som var ansvarig för skapandet och sedan konfigurera den igen. Detta återskapar den klassiska principen. Den har inte stöd för att migrera klassiska principer för MTD-appar till den nya principtypen för villkorlig åtkomst.
>
> Klassiska principer för villkorlig åtkomst för MTD-appar:
>
> - Används av Intune MTD för att kräva att enheter registreras i Azure AD så att de har ett enhets-ID innan de kommunicerar med MTD-partners. ID:t krävs så att enheterna kan rapportera deras status till Intune.
> - Har ingen påverkan på andra molnappar eller resurser.
> - Är skilda från principer för villkorlig åtkomst som du kan skapa för att hantera MTD.
> - Samverkar inte som standard med andra principer för villkorsstyrd åtkomst som du använder för utvärdering.
>
> Du kan visa klassiska principer för villkorlig åtkomst genom att gå till **Azure Active Directory** > **Villkorlig åtkomst** > **Klassiska principer** i [Azure](https://portal.azure.com/#home).

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Publicera Windows-enheter med en konfigurationsprofil

För Windows-plattformen ska du publicera dina Intune-hanterade enheter till Microsoft Defender ATP när du har upprättat tjänst-till-tjänst-anslutningen mellan Intune och Microsoft Defender ATP, så att data om deras risknivå kan samlas in och användas. Använd en enhetskonfigurationsprofil för att publicera enheter med Microsoft Defender ATP.

När du upprättar anslutningen till Microsoft Defender ATP fick Intune ett konfigurationspaket för Microsoft Defender ATP-registrering från Microsoft Defender ATP. Det här paketet distribueras till enheter med enhetskonfigurationsprofilen. Konfigurationspaketet konfigurerar enheter för att kommunicera med [Microsoft Defender ATP-tjänster](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) för att söka igenom filer, identifiera hot och rapportera risken till Microsoft Defender ATP. När du publicerat en enhet med konfigurationspaketet behöver du inte göra det igen. Du kan också publicera enheter med hjälp av en [grupprincip eller Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile"></a>Skapa en enhetskonfigurationsprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange ett **Namn** och en **Beskrivning**.
4. För **Plattform** väljer du **Windows 10 och senare**
5. För **Profiltyp** väljer du **Microsoft Defender ATP (Windows 10 Desktop)** .
6. Konfigurera inställningarna:

   - **Pakettyp för konfiguration av Microsoft Defender ATP-klient**: Välj **Publicera** för att lägga till konfigurationspaketet i profilen. Välj **Avregistrera** för att ta bort konfigurationspaketet från profilen.
  
     > [!NOTE]
     > Om du har upprättat en anslutning på rätt sätt med Microsoft Defender ATP, kommer Intune automatiskt **publicera** konfigurationsprofilen åt dig, och inställningen **Pakettyp för konfiguration av Microsoft Defender ATP-klient** kommer inte vara tillgänglig.
  
   - **Exempeldelning för alla filer**: **Aktivera** tillåter att exempel samlas in och delas med Microsoft Defender ATP. Till exempel om du ser en misstänkt fil kan du skicka den till Microsoft Defender ATP för djupgående analys. **Inte konfigurerad** delar inte några exempel med Microsoft Defender ATP.
   - **Skicka frekvensvärde för telemetrirapportering**: För enheter med hög risk kan du **Aktivera** den här inställningen så att den rapporterar telemetri till tjänsten Microsoft Defender ATP oftare.

     [Registrera Windows 10-datorer med hjälp av Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) innehåller mer information om dessa Microsoft Defender ATP-inställningar.

7. Välj **OK** och sedan **Skapa** för att spara ändringarna och skapa profilen.
8. [Tilldela en enhetskonfigurationsprofil](../configuration/device-profile-assign.md) till enheter som du vill utvärdera med Microsoft Defender ATP.

## <a name="onboard-android-devices"></a>Registrera Android-enheter
När du har upprättat tjänst-till-tjänst-anslutningen mellan Intune och Microsoft Defender ATP måste du registrera dina hanterade enheter till Microsoft Defender ATP så att data om deras risknivå kan samlas in och användas.

Det finns detaljerade anvisningar för registrering av Android-enheter, inklusive krav för slutanvändare och administratörer, i [Microsoft Defender Advanced Threat Protection för Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) i dokumentationen för Microsoft Defender ATP.

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Skapa och tilldela en efterlevnadspolicy för att ange en enhets risknivå

För både Windows- och Android-enheter bestämmer efterlevnadsprincipen risknivån som du bedömer som lämplig för en enhet.

Om du inte vet hur du skapar en efterlevnadspolicy kan du läsa om proceduren [Skapa en policy](../protect/create-compliance-policy.md#create-the-policy) i artikeln *Skapa en policy för efterlevnad i Microsoft Intune*. Följande information gäller konfigurering av Defender ATP som en del av en policy för efterlevnad.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Efterlevnadsprinciper** > **Principer** > **Skapa princip**.

3. Vid **Plattform** väljer du något av följande alternativ i listrutan:
   - **Windows 10 och senare**
   - **Android-enhetsadministratör**
   - **Android enterprise**

   Välj sedan **Skapa** för att öppna konfigurationsfönstret **Skapa princip**.

4. Ange ett **Namn** som hjälper dig att identifiera policyn senare. Du kan också välja att ange en **Beskrivning**.
  
5. På fliken **Efterlevnadsinställningar** utökar du gruppen **Microsoft Defender ATP** och ställer in önskad nivå för alternativet **Kräv att enheten ska hållas vid eller under riskpoängen**.

   Klassificeringar för hotnivå [bestäms av Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Rensa**: Den här nivån är säkrast. Enheten får inte ha några existerande hot och ska ha tillgång till företagsresurser. Om något hot identifieras på enheten kommer den att utvärderas som icke-kompatibel. (Microsoft Defender ATP använder värdet *Säkert*.)
   - **Låg**: Enheten följer standard om det enbart finns hot på låg nivå på enheten. Enheter med medel- eller hög risk är inte kompatibla.
   - **Medel**: Enheten följer standard om hoten som hittas på enheten är låga eller medelhöga. Om hot på en högre nivå identifieras på enheten får den statusen icke-kompatibel.
   - **Hög**: Den här nivån är den minst säkra och tillåter alla hotnivåer. Enheter med höga, medelhöga eller låga risknivåer anses uppfylla efterlevnadskraven.

6. Slutför konfigurationen av principen, inklusive tilldelning av principen till tillämpliga grupper.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurera webbskydd på enheter som kör Android

Som standard aktiverar Microsoft Defender ATP för Android webbskyddsfunktionen. [Webbskydd](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) hjälper dig att skydda enheter mot olika webbhot och nätfiskeattacker.

Även om funktionen är aktiverad som standard finns det skäl att inaktivera det här skyddet på vissa Android-enheter. Du kan till exempel välja att endast använda appavsökningsfunktionen i Microsoft Defender ATP eller förhindra att webbskyddsfunktionen använder ditt VPN under sökningen efter skadliga webbadresser.

Du kan inaktivera hela eller delar av webbskyddsfunktionen i Intune. Vilken metod du använder och vilka funktioner du kan inaktivera beror på hur Android-enheten är registrerad i Intune:

- **Android-enhetsadministratör**: Använd en konfigurationsprofil till att ange anpassade OMA-URI-inställningar på enheten för att inaktivera hela webbskyddsfunktionen eller bara inaktivera användningen av VPN. Allmän information om anpassade inställningar för Android-enheter finns i [Anpassade inställningar](../configuration/custom-settings-android.md).

- **Android Enterprise-arbetsprofil**: Använd en appkonfigurationsprofil och *konfigurationsdesignern* till att inaktivera webbskydd. Den här metoden och registreringstypen gör att du kan inaktivera alla webbskyddsfunktioner, men inte endast användningen av VPN. Allmän information om policyer för appkonfigurering finns i [Använda konfigurationsdesignern](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Om du vill konfigurera webbskydd på enheter använder du följande procedurer till att skapa och distribuera den aktuella konfigurationen.

### <a name="disable-web-protection-for-android-device-administrator"></a>Inaktivera webbskydd för Android-enhetsadministratör

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande inställningar:

   - **Plattform**: Välj **Android-enhetsadministratör**
   - **Profil**: Välj **Anpassad**

   Välj **Skapa**.

4. Ange följande information på sidan **Allmänt**:

   - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Till exempel *Anpassad Android-profil för webbskydd i Microsoft Defender ATP*
   - **Beskrivning**: Ange en beskrivning av profilen. Den här inställningen är valfri men rekommenderas.

5. Gå till **Konfigurationsinställningar** och välj **Lägg till**.

   Ange inställningar för den konfiguration du vill distribuera:

   - **Inaktivera webbskydd**:
     - **Namn**: Ange ett unikt namn för den här OMA-URI-inställningen så att du lätt kan hitta den. Till exempel *Inaktivera webbskydd i Microsoft Defender ATP*
     - **Beskrivning**: (Valfritt) Ange en beskrivning som ger en översikt över inställningen samt annan viktig information.
     - **OMA-URI**: Ange **./Vendor/MSFT/DefenderATP/AntiPhishing**
     - **Datatyp**: Använd listrutan och välj **Heltal**
     - **Värde**: Ange **0** om du vill inaktivera Webbskydd, inklusive den VPN-baserade genomsökningen.
       > [!NOTE]
       > Ange **1** om du vill aktivera Webbskydd, vilket är standardinställningen för webbskyddet.

   - **Inaktivera endast användningen av VPN för webbskydd**:
     - **Namn**: Ange ett unikt namn för den här OMA-URI-inställningen så att du lätt kan hitta den. Till exempel *Inaktivera VPN-användning av webbskydd i Microsoft Defender ATP*
     - **Beskrivning**: (Valfritt) Ange en beskrivning som ger en översikt över inställningen samt annan viktig information.
     - **OMA-URI**: Ange **./Vendor/MSFT/DefenderATP/Vpn**
     - **Datatyp**: Använd listrutan och välj **Heltal**
     - **Värde**: Ange **0** om du vill inaktivera den VPN-baserade genomsökningen.
       > [!NOTE]
       > Ange **1** om du vill aktivera Webbskydd, vilket är standardinställningen för webbskyddet.

   Välj **Lägg till** om du vill spara konfigurationen av OMA-URI-inställningarna och välj sedan **Nästa** för att fortsätta.

6. På sidan **Tilldelningar** väljer du de grupper som ska få profilen. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

7. Välj **Skapa** på sidan **Granska + skapa** när du är färdig. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Inaktivera webbskydd för Android Enterprise-arbetsprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Appar** > **Appkonfigurationsprinciper** > **Lägg till** och välj sedan Hanterade enheter.

3. Ange följande information på sidan **Allmänt**:

   - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Till exempel *Anpassad appkonfiguration för webbskydd i Microsoft Defender ATP*
   - **Beskrivning**: Ange en beskrivning av profilen. Den här inställningen är valfri men rekommenderas.
   - **Plattform**: Välj **Android Enterprise**
   - **Profiltyp**: Välj **Endast arbetsprofil**
   - **Målapp**: Klicka på **Välj app**.

4. På sidan **Tillhörande app** letar du rätt på och väljer **Defender ATP**, och väljer sedan **OK** > **Nästa**.

5. På sidan **Inställningar** använder du listrutan **Format för konfigurationsinställningar**, väljer **Använd konfigurationsdesignern** och klickar sedan på **Lägg till**. JSON-redigeraren öppnas.

6. Leta rätt på och välj **Webbskydd** och välj sedan **OK** för att återgå till sidan **Inställningar**.

7. Som **Konfigurationsvärde** anger du **0** om du vill inaktivera webbskyddet.

   > [!NOTE]
   > Ange **1** om du vill aktivera Webbskydd, vilket är standardinställningen för webbskyddet.

   Fortsätt genom att välja **Nästa**.

8. På sidan **Tilldelningar** väljer du de grupper som ska få profilen. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

9. Välj **Skapa** på sidan **Granska + skapa** när du är färdig. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="create-a-conditional-access-policy"></a>Skapa en princip för villkorlig åtkomst

Principer för villkorsstyrd åtkomst kan använda Microsoft Defender ATP till att blockera åtkomsten till resurser för enheter som överskrider den hotnivå du anger. Du kan blockera enhetens åtkomst till företagets resurser, såsom SharePoint eller Exchange Online.

> [!TIP]
> Villkorsstyrd åtkomst är en teknik i Azure Active Directory (Azure AD). Noden *Villkorsstyrd åtkomst* i administrationscentret för Microsoft Endpoint Manager är noden från *Azure AD*.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Villkorlig åtkomst** > **Ny princip**.

3. Ange ett **Namn** på principen och välj **Användare och grupper**. Använd inkludera eller exkludera alternativ för att lägga till grupper för principen och välj **Klar**.

4. Välj **Molnappar**, och välj vilka appar som ska skyddas. Välj t.ex. **Välj appar**, och välj **Office 365 SharePoint Online** och **Office 365 Exchange Online**.

   Klicka på **Klar** för att spara ändringarna.

5. Välj **Villkor** > **Klientappar** för att tillämpa principen till appar och webbläsare. Välj exempelvis **Ja** och aktivera sedan **Webbläsare** och **Mobilappar och skrivbordsklienter**.

   Klicka på **Klar** för att spara ändringarna.

6. Välj **Bevilja** för att använda villkorlig åtkomst baserat på enhetsefterlevnad. Välj exempelvis **Bevilja åtkomst** > **Kräv att enheten markerats som kompatibel**.

    Välj **OK** för att spara ändringarna.

7. Välj **Aktiverar principen**, och sedan **Skapa** för att spara ändringarna.

## <a name="monitor-device-compliance"></a>Övervaka enhetsefterlevnad

Övervaka status för enheter som har Microsoft Defender ATP-policyn för efterlevnad.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Övervaka** > **Principefterlevnad**.

3. Hitta din Microsoft Defender ATP-princip i listan och se vilka enheter som är kompatibla eller inkompatibla.

Du kan också använda den *operativa* rapporten för icke-kompatibla enheter från samma plats:

1. Välj **Enheter** > **Övervaka** > **icke-kompatibla enheter**.

Mer information om rapporter finns i [Intune-rapporter](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Visa registreringsstatus

Om du vill se registreringsstatus för alla Intune-hanterade enheter kan du gå till **Slutpunktssäkerhet** > **Microsoft Defender ATP**. Från den här sidan kan du också börja skapa en enhetskonfigurationsprofil som kan registrera fler enheter i Microsoft Defender ATP.

## <a name="next-steps"></a>Nästa steg

[Villkorlig åtkomst för Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Instrumentpanel för Microsoft Defender ATP-risk](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Använd säkerhetsaktiviteter med ATP:s sårbarhetshantering för att åtgärda problem på enheterna](atp-manage-vulnerabilities.md).

[Komma igång med principer för enhetsefterlevnad](device-compliance-get-started.md)
