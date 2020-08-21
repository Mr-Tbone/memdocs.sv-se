---
title: Skapa och distribuera appskyddsprinciper
titleSuffix: Microsoft Intune
description: Det här ämnet beskriver hur du skapar och tilldelar Microsoft Intunes appskyddsprinciper.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1cb05cb518d4edfb443bf4f70ff1c51154e17f4c
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217647"
---
# <a name="how-to-create-and-assign-app-protection-policies"></a>Hur du skapar och tilldelar skyddsprinciper för appar

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Lär dig hur du skapar och tilldelar Microsoft Intune-appskyddsprinciper (APP) för användare i din organisation. Det här avsnittet beskriver också hur du ändrar befintliga principer.

## <a name="before-you-begin"></a>Innan du börjar

Appskyddsprinciper kan tillämpas på appar som körs på enheter som kan, men som inte nödvändigtvis, hanteras av Intune. En mer detaljerad beskrivning av hur appskyddsprinciper fungerar och scenarier som stöds av appskyddsprinciper i Intune finns i [Översikt över principer för appskydd](app-protection-policy.md).

De alternativ som är tillgängliga i appskyddsprinciper (APP) gör det möjligt för organisationer att skräddarsy skyddet för deras specifika behov. För vissa är det inte alltid uppenbart vilka policyinställningar som krävs för att implementera ett fullständigt scenario. För att hjälpa organisationer att prioritera härdning av mobilklientslutpunkter har Microsoft infört taxonomi för dataskyddsramverket med APP:er för mobilappshantering för iOS och Android.

Dataskyddsramverket för APP:er är indelat i tre olika konfigurationsnivåer där varje nivå bygger på den föregående nivån:

- **Grundläggande dataskydd för företag** (nivå 1) säkerställer att apparna skyddas med en PIN-kod, krypteras och utför åtgärder för selektiv rensning. För Android-enheter verifierar den här nivån Android-enhetsattestering. Det här är en konfiguration på ingångsnivå som ger liknande dataskyddskontroll som policyer för Exchange Online-postlådor och introducerar IT-avdelningen och användarna för APP.
- **Förbättrat dataskydd för företag** (nivå 2) introducerar APP-mekanismer för att förhindra dataläckage och minimikrav för operativsystem. Den här konfigurationen gäller för de flesta mobila användare som har åtkomst till arbets- eller skoldata.
- **Starkt dataskydd för företag** (nivå 3) introducerar avancerade mekanismer för dataskydd, förbättrad PIN-konfiguration och skydd mot mobila hot i appar. Den här konfigurationen passar för användare som hanterar skyddsvärda data.

Om du vill se specifika rekommendationer för varje konfigurationsnivå och minsta antal appar som måste skyddas går du till [Dataskyddsramverk med hjälp av appskyddsprinciper](app-protection-framework.md).

Om du letar efter en lista över appar som har integrerat Intune SDK kan du gå till [Skyddade appar i Microsoft Intune](apps-supported-intune-apps.md).

Information om att lägga till organisationens affärsapplikationer i Microsoft Intune och förbereda för appskyddsprinciper finns i [Lägga till appar i Microsoft Intune](apps-add.md).

## <a name="app-protection-policies-for-iosipados-and-android-apps"></a>Appskyddsprinciper för iOS/iPadOS-appar och Android-appar

När du skapar en appskyddsprincip för iOS/iPad-appar och Android-appar följer du ett modernt Intune-processflöde som resulterar i en ny appskyddsprincip. Information om att skapa appskyddsprinciper för Windows-appar finns i [Skapa och distribuera en WIP-princip (Windows Information Protection) med Intune](../apps/windows-information-protection-policy-create.md).

### <a name="create-an-iosipados-or-android-app-protection-policy"></a>Skapa en appskyddsprincip för iOS/iPadOS eller Android

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Appskyddsprinciper** i Intune-portalen. Därmed öppnas **Principer för appskydd** där du kan skapa nya principer och redigera befintliga.
3. Välj **Skapa princip** och välj antingen **iOS/iPadOS** eller **Android**. Fönstret **Skapa princip** visas.
4. På sidan **Grundläggande** lägger du till följande värden:

    | Värde | Beskrivning |
    |--------------|------------------------------------------------|
    | Name | Namnet på den här appskyddsprincipen. |
    | Beskrivning | [Valfritt] Beskrivningen av den här appskyddsprincipen. |


    Värdet för **Plattform** anges baserat på ditt val ovan.

    ![Skärmbild av sidan Grundläggande i fönstret Skapa princip](./media/app-protection-policies/app-protection-add-policies-01.png)

5. Klicka på **Nästa** för att visa sidan **Appar**.<br>
    På sidan **Appar** kan du välja hur du vill tillämpa den här principen på appar på olika enheter. Du måste lägga till minst en app.<p>

    | Värde/alternativ | Beskrivning |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Rikta till appar på alla enhetstyper | Använd det här alternativet om du vill att principen ska riktas mot appar på enheter i valfritt hanteringstillstånd. Välj **Nej** om du vill rikta till appar på specifika enhetstyper. Information finns i [Ange mål för appskyddsprinciper utifrån enhetens hanteringsstatus](#target-app-protection-policies-based-on-device-management-state) |
    |     Enhetstyper | Använd det här alternativet för att ange huruvida den här principen gäller för MDM-hanterade enheter eller ohanterade enheter. När det gäller iOS/iPadOS APP-principer väljer du bland **Ohanterade** och **Hanterade** enheter. För Android APP-principer väljer du från **Ohanterade**, **Android-enhetsadministratör** och **Android Enterprise**.  |
    | Offentliga appar | Klicka på **Välj offentliga appar** för att välja de appar som ska vara mål. |
    | Anpassade appar | Klicka på **Välj anpassade appar** för att välja anpassade appar som mål baserat på ett paket-ID. |

    Den app eller de appar som du har valt visas i listan över offentliga och anpassade appar.
6. Klicka på **Nästa** för att visa sidan **Dataskydd**.<br>
    Den här sidan innehåller inställningar för DLP-kontroller (dataförlustskydd), däribland begränsningar för att klippa ut, kopiera, klistra in och spara som. De här inställningarna avgör hur användarna interagerar med data i de appar som den här appskyddsprincipen gäller för.

    **Inställningar för dataskydd**:<br>
    - **Dataskydd för iOS/iPadOS** – mer information finns i [Inställningar för iOS/iPadOS-appskyddsprincip – dataskydd](app-protection-policy-settings-ios.md#data-protection).
    - **Dataskydd för Android** – mer information finns i [Inställningar för Android-appskyddsprincip – dataskydd](app-protection-policy-settings-android.md#data-protection).

7. Klicka på **Nästa** för att visa sidan **Åtkomstkrav**.<br>
    Den här sidan innehåller inställningar som gör att du kan konfigurera de krav för PIN-kod och autentiseringsuppgifter som användarna måste uppfylla för att få åtkomst till appar i en arbetskontext.
 
    **Inställningar för åtkomstkrav**:<br>
    - **Åtkomstkrav för iOS/iPadOS** – mer information finns i [Inställningar för iOS/iPadOS-appskyddsprincip – åtkomstkrav](app-protection-policy-settings-ios.md#access-requirements).
    - **Åtkomstkrav för Android** – mer information finns i [Inställningar för Android-appskyddsprincip – åtkomstkrav](app-protection-policy-settings-android.md#access-requirements).

8. Klicka på **Nästa** för att visa sidan **Villkorsstyrd start**.<br>
    Den här sidan innehåller inställningar med vilka du anger krav för inloggningssäkerhet för din appskyddsprincip. Välj en **inställning** och ange det **värde** som användare måste uppfylla för att logga in på företagsappen. Välj sedan den **Åtgärd** som du vill vidta om användarna inte uppfyller dina krav. I vissa fall kan flera åtgärder konfigureras för en och samma inställning.

    **Inställningar för villkorsstyrd start**:<br>
    - **Villkorsstyrd start för iOS/iPadOS** – mer information finns i [Inställningar för iOS/iPadOS-appskyddsprincip – villkorsstyrd start](app-protection-policy-settings-ios.md#conditional-launch).
    - **Villkorsstyrd start för Android** – mer information finns i [Inställningar för Android-appskyddsprincip – villkorsstyrd start](app-protection-policy-settings-android.md#conditional-launch).

9. Klicka på **Nästa** för att visa sidan **Tilldelningar**.<br>
   På sidan **Tilldelningar** kan du tilldela appskyddsprincipen till grupper av användare. Du måste tillämpa principen på en grupp användare för att principen ska börja gälla.

10. Klicka på **Nästa: Granska och skapa** för att granska de värden och inställningar som du angav för den här appskyddsprincipen.

11. När du är klar klickar du på **Skapa** för att skapa appskyddsprincipen i Intune.

    > [!TIP]
    > Följande principinställningar används endast när du använder appar i arbetskontexten. När slutanvändarna använder appen för att utföra personliga uppgifter påverkas de inte av dessa principer. Observera att när du skapar en ny fil så betraktas den som en personlig fil.

    > [!IMPORTANT]
    > Det kan ta tid innan appskyddsprinciper tillämpas på befintliga enheter. Slutanvändarna får ett meddelande på enheten när appskyddsprincipen har tillämpats. Tillämpa dina appskyddsprinciper på enheter innan du tillämpar regler för villkorlig åtkomst.

Slutanvändarna kan hämta apparna från App Store eller Google Play. Mer information finns i:
* [Vad som händer när din Android-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-android.md)
* [Vad som händer när din iOS/iPadOS-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-ios.md)

## <a name="change-existing-policies"></a>Ändra befintliga principer
Du kan redigera en befintlig princip och tillämpa den på inriktade användare. När du ändrar befintliga principer ser dock inte användare som redan är inloggade i apparna ändringarna förrän efter åtta timmar.

För att kunna se effekten av ändringarna direkt måste slutanvändaren logga ut ur appen och sedan logga in igen.

### <a name="to-change-the-list-of-apps-associated-with-the-policy"></a>Ändra listan över appar som är associerade med principen

1. I fönstret **Appskyddsprinciper** väljer du den princip som du vill ändra.

2. Välj **Egenskaper** i fönstret *Intune-appskydd*.

3. Välj **Redigera** bredvid avsnittet *Appar*.

4. På sidan **Appar** kan du välja hur du vill tillämpa den här principen på appar på olika enheter. Du måste lägga till minst en app.<p>
    
    | Värde/alternativ | Beskrivning |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Rikta till appar på alla enhetstyper | Använd det här alternativet om du vill att principen ska riktas mot appar på enheter i valfritt hanteringstillstånd. Välj **Nej** om du vill rikta till appar på specifika enhetstyper. Det kan krävas ytterligare appkonfiguration för den här inställningen. Mer information finns i [Target app protection policies based on device management state](#target-app-protection-policies-based-on-device-management-state) (Ange mål för appskyddsprinciper utifrån enhetens hanteringsstatus). |
    |     Enhetstyper | Använd det här alternativet för att ange huruvida den här principen gäller för MDM-hanterade enheter eller ohanterade enheter. När det gäller iOS/iPadOS APP-principer väljer du bland **Ohanterade** och **Hanterade** enheter. För Android APP-principer väljer du från **Ohanterade**, **Android-enhetsadministratör** och **Android Enterprise**.  |
    | Offentliga appar | Klicka på **Välj offentliga appar** för att välja de appar som ska vara mål. |
    | Anpassade appar | Klicka på **Välj anpassade appar** för att välja anpassade appar som mål baserat på ett paket-ID. |

    Den app eller de appar som du har valt visas i listan över offentliga och anpassade appar.

5. Klicka på **Granska + skapa** för att granska de appar som valts för den här principen.

6. När du är klar klickar du på **Spara** för att uppdatera appskyddsprincipen.
 
#### <a name="to-change-the-list-of-user-groups"></a>Ändra listan över användargrupper

1. I fönstret **Appskyddsprinciper** väljer du den princip som du vill ändra.

2. Välj **Egenskaper** i fönstret *Intune-appskydd*.

3. Välj **Redigera** bredvid avsnittet *Tilldelningar*.

4. Om du vill lägga till en ny användargrupp för principen väljer du **Välj grupper att ta med** på fliken *Inkludera* och sedan användargruppen. Lägg till gruppen genom att välja **Välj**. 

5. Om du vill exkludera en användargrupp väljer du **Välj grupper att exkludera** på fliken *Exkludera* och väljer sedan användargruppen. Välj **Välj** för att ta bort användargruppen.  

6. Om du vill ta bort grupper som har lagts till tidigare markerar du ellipsen (...) och väljer **Ta bort** på någon av flikarna *Inkludera* eller *Exkludera*.

7. Klicka på **Granska + skapa** för att granska de användargrupper som valts för den här principen.

8. När dina ändringar av tilldelningarna är klar sparar du konfigurationen genom att välja **Spara** och distribuerar principen till den nya uppsättningen användare. Om du väljer **Avbryt** innan du sparar konfigurationen ignoreras alla ändringar som du har gjort på flikarna *Inkludera* och *Exkludera*.

### <a name="to-change-policy-settings"></a>Ändra principinställningar

1. I fönstret **Appskyddsprinciper** väljer du den princip som du vill ändra.

2. Välj **Egenskaper** i fönstret *Intune-appskydd*.

3. Välj **Redigera** bredvid det avsnitt som motsvarar de inställningar som du vill ändra. Ändra inställningarna till nya värden.

7. Klicka på **Granska + skapa** för att granska de uppdaterade inställningarna för den här principen.

4. Välj **Spara** för att spara dina ändringar. Upprepa processen för att välja ett inställningsområde och ändra och spara sedan ändringarna, tills alla ändringar har slutförts. Därefter kan du stänga fönstret *Intune-appskydd – Egenskaper*. 

## <a name="target-app-protection-policies-based-on-device-management-state"></a>Ange mål för appskyddsprinciper utifrån enhetens hanteringsstatus
I många organisationer är det vanligt att tillåta användare att använda både enheter som hanteras av hantering av mobilenheter (MDM) i Intune, till exempel företagsägda enheter, och ohanterade enheter som endast är skyddade med Intune-appskyddsprinciper. Ohanterade enheter är ofta kända som BYOD-enheter (Bring Your Own Devices).

Eftersom Intune-appskyddsprinciper som är riktade till en användares identitet kan skyddsinställningarna för en användare gälla både för registrerade (MDM-hanterade) och icke-registrerade enheter (utan MDM). Därför kan du rikta en Intune-appskyddsprincip till Intune-registrerade enheter eller icke-registrerade iOS/iPadOS- och Android-enheter. Du kan ha en skyddsprincip för ohanterade enheter där ett strikt dataförlustskydd (DLP) används och en separat skyddsprincip för MDM-hanterade enheter, där du kan använda lite mindre strikta DLP-kontroller. Mer information om hur det här fungerar på personliga Android Enterprise-enheter finns i [Appskyddsprinciper och arbetsprofiler](android-deployment-scenarios-app-protection-work-profiles.md).

Om du vill skapa de här principerna, så gå till **Appar** > **Appskyddsprinciper** på Intune-konsolen och välj **Skapa princip**. Du kan även redigera eller en befintlig princip. För att appskyddsprincipen ska gälla för både hanterade och ohanterade enheter går du till sidan **Appar** och bekräftar att **Rikta till appar på alla typer av enheter** är angett till **Ja**, som är standardvärdet. Om du vill tilldela detaljerat baserat på hanteringstillståndet anger du **Rikta till appar på alla typer av enheter** till **Nej**. 

### <a name="device-types"></a>Enhetstyper

- **Ohanterade**: För iOS/iPad-enheter räknas alla enheter där antingen Intune MDM-hantering eller en MDM/EMM-lösning från tredje part inte skickar nyckeln `IntuneMAMUPN` som ohanterade enheter. För Android-enheter räknas alla enheter där ingen Intune MDM-hantering kan identifieras som ohanterade enheter. Detta innefattar enheter som hanteras av MDM-leverantörer från tredje part.
- **Intune-hanterade enheter**: Hanterade enheter hanteras av Intune MDM.
- **Android-enhetsadministratör**: Intune-hanterade enheter som använder Androids enhetsadministrations-API.
- **Android Enterprise**: Intune-hanterade enheter som använder Android Enterprise-arbetsprofiler eller Android Enterprise fullständig enhetshantering.

När det gäller Android så uppmanar Android-enheter användarna att installera Intune-företagsportalsappen oavsett vilken typ av enhet som valts. Om du till exempel väljer Android Enterprise kommer användare med ohanterade Android-enheter fortfarande att frågas.

Om valet av Enhetstyp ska framtvingas på Intune-hanterade enheter i iOS/iPadOS så krävs ytterligare appkonfigurationsinställningar. De här konfigurationerna kommunicerar med APP-tjänsten om att en viss app hanteras och att appinställningarna inte gäller:

- **IntuneMAMUPN** måste konfigureras för alla MDM-hanterade program. Mer information finns i [Hantera dataöverföring mellan iOS/iPadOS-appar med Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- **IntuneMAMDeviceID** måste konfigureras för alla tredjeparts och verksamhetsspecifika MDM-hanterade program. **IntuneMAMDeviceID** ska konfigureras till enhetens ID-token. Exempelvis `key=IntuneMAMDeviceID, value={{deviceID}}`. Mer information finns i [Lägg till appkonfigurationsprinciper för hanterade iOS/iPadOS-enheter](app-configuration-policies-use-ios.md).
- Om bara **IntuneMAMDeviceID** är konfigurerat kan Intune App betrakta enheten som ohanterad.

> [!NOTE]
> Läs [MAM protection policies targeted based on management state](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state) (MAM-skyddsprinciper som riktas baserat på hanteringstillstånd) om du vill ha specifik information om iOS/iPadOS-stöd och appskyddsprinciper som baseras på hanteringstillstånd.

## <a name="policy-settings"></a>Principinställningar
Välj någon av följande länkar om du vill se en fullständig lista med principinställningar för iOS/iPadOS och Android:

- [iOS/iPadOS-principer](app-protection-policy-settings-ios.md)
- [Android-principer](app-protection-policy-settings-android.md)

## <a name="next-steps"></a>Nästa steg
[Övervaka efterlevnad och användarstatus](app-protection-policies-monitor.md)

## <a name="see-also"></a>Se även
* [Vad som händer när din Android-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-android.md)
* [Vad som händer när din iOS/iPadOS-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-ios.md)
