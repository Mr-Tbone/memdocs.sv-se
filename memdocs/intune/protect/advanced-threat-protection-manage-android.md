---
title: Hantera Microsoft Defender ATP-webbskydd för Android-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera webbskydd i Microsoft Defender Avancerat skydd (Microsoft Defender ATP) för Android i Intune.
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
ms.openlocfilehash: 49423d1d1b887aaf3ed3323ff36678bb7319b1ad
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909473"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Konfigurera Microsoft Defender ATP på Android-enheter som du hanterar med Intune

När du integrerar Microsoft Intune och Microsoft Defender Avancerat skydd (ATP) kan du använda enhetskonfigurationsprofiler när du ska ändra vissa inställningar för Microsoft Defender ATP på Android-enheter.

Innan du fortsätter måste du [konfigurera Microsoft Defender ATP i Intune](../protect/advanced-threat-protection-configure.md) och registrera Android-enheter till Microsoft Defender ATP.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurera webbskydd på enheter som kör Android

Som standard aktiverar Microsoft Defender ATP för Android webbskyddsfunktionen. [Webbskydd](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) hjälper dig att skydda enheter mot olika webbhot och nätfiskeattacker.

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

## <a name="next-steps"></a>Nästa steg

- [Övervaka efterlevnad för risk nivåer](../protect/advanced-threat-protection-monitor.md)
- [Använd säkerhetsaktiviteter med ATP-sårbarhetshantering när du ska åtgärda problem på enheterna](../protect/atp-manage-vulnerabilities.md)

Läs mer i Microsoft Defender ATP-dokumentationen:

- [Villkorlig åtkomst för Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Instrumentpanel för Microsoft Defender ATP-risk](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)