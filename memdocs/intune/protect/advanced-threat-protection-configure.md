---
title: Konfigurera Microsoft Defender ATP i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera Microsoft Defender Avancerat skydd (Microsoft Defender ATP) i Intune, inklusive anslutning till ATP, registrering av enheter, tilldelning av risknivåefterlevnad och principer för villkorsstyrd åtkomst.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e19315f07d803e2aab53b3724fde85f1975c0c5
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264588"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Konfigurera Microsoft Defender ATP i Intune

Informationen och procedurerna i den här artikeln hjälper dig att konfigurera integrering av Microsoft Defender ATP med Intune. Konfigurationen omfattar fölande allmänna steg:

- Aktivera Microsoft Defender ATP i Intune för din klientorganisation
- Registrera enheter som kör Windows och Android
- Konfigurera enhetsrisknivåer med efterlevnadsprinciper
- Använd principer för villkorsstyrd åtkomst när du vill blockera enheter som överskrider dina förväntade risknivåer

Innan du startar måste din miljö uppfylla [kraven](../protect/advanced-threat-protection.md#prerequisites) för att använda Microsoft Defender ATP med Intune.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Aktivera Microsoft Defender ATP i Intune

Det första steget är att skapa en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP. Konfigurationen kräver administrativ åtkomst till både Microsoft Defender Security Center och Intune.

Du behöver bara aktivera Microsoft Defender ATP en gång per klientorganisation.

### <a name="to-enable-microsoft-defender-atp"></a>Aktivera Microsoft Defender ATP

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Microsoft Defender ATP** och välj sedan **Öppna Microsoft Defender Säkerhetscenter**.

   ![Välj att öppna Microsoft Defender Security Center](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. I **Microsoft Defender Security Center**:
   1. Välj **Inställningar** > **Avancerade funktioner**.
   2. För **Microsoft Intune-anslutningen**, välj **På**:

      ![Aktivera anslutningen till Intune](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

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

## <a name="onboard-devices"></a>Registrera enheter

När du aktiverade stöd för Microsoft Defender ATP i Intune upprättade du en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP. Du kan sedan registrera enheter som du hanterar med Intune i Microsoft Defender ATP, vilket möjliggör insamling av data om enhetsrisknivåer.

### <a name="onboard-windows-devices"></a>Registrera Windows-enheter

När du upprättade anslutningen mellan Intune och Microsoft Defender ATP fick Intune ett konfigurationspaket för Microsoft Defender ATP-registrering från Microsoft Defender ATP. Du distribuerar det här konfigurationspaketet till dina Windows-enheter med en enhetskonfigurationsprofil för Microsoft Defender ATP.

Konfigurationspaketet konfigurerar enheter så att de kan kommunicera med [Microsoft Defender ATP-tjänster](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) för att söka igenom filer och identifiera hot. Enheten har också konfigurerats så att den rapporterar enhetsrisknivån till Microsoft Defender ATP baserat på de efterlevnadsprinciper som du skapar.

När du publicerat en enhet med konfigurationspaketet behöver du inte göra det igen. Du kan också publicera enheter med hjälp av en [grupprincip eller Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints).

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Skapa enhetskonfigurationsprofilen så att du kan publicera Windows-enheter

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

### <a name="onboard-android-devices"></a>Registrera Android-enheter

När du har upprättat en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP kan du registrera Android-enheter i Microsoft Defender ATP. Vid registreringen konfigureras enheterna så att de kan kommunicera med Defender ATP, som sedan samlar in data om enheternas risknivå.

Till skillnad från Windows-enheter finns det inget konfigurationspaket för enheter som kör Android. Information om krav och registreringsanvisningar för Android finns i [Översikt över Microsoft Defender ATP för Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android) i Microsoft Defender ATP-dokumentationen.

För enheter som kör Android kan du även använda Intune-principer när du ska ändra Microsoft Defender ATP på Android. Mer information finns i [Microsoft Defender ATP-webbskydd](../protect/advanced-threat-protection-manage-android.md).

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

## <a name="next-steps"></a>Nästa steg

- [Konfigurera Microsoft Defender ATP-inställningar på Android](../protect/advanced-threat-protection-manage-android.md)
- [Övervaka efterlevnad för risk nivåer](../protect/advanced-threat-protection-monitor.md)

Läs mer i Intune-dokumentationen:

- [Använd säkerhetsaktiviteter med ATP:ernas sårbarhetshantering när du ska åtgärda problem på enheterna](atp-manage-vulnerabilities.md)
- [Komma igång med principer för enhetsefterlevnad](device-compliance-get-started.md)

Läs mer i Microsoft Defender ATP-dokumentationen:

- [Villkorlig åtkomst för Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Instrumentpanel för Microsoft Defender ATP-risk](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
