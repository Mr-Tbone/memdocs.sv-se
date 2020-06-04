---
title: Kryptera Windows 10-enheter med BitLocker i Intune
titleSuffix: Microsoft Intune
description: Kryptera enheter med inbyggda krypteringsmetoder i BitLocker och hantera återställningsnycklarna för de krypterade enheterna i Intune-portalen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 16a2558a0f4b002528e749f4a66d3341e83c8576
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989664"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>Hantera BitLocker-policy för Windows 10 i Intune

Använd Intune för att konfigurera BitLocker-diskkryptering på enheter som kör Windows 10.

BitLocker är tillgängligt på enheter som kör Windows 10 eller senare. För vissa BitLocker-inställningar måste enheten har en TPM som stöds.

Använd någon av följande policytyper till att konfigurera BitLocker på dina hanterade enheter

- **[Endpoint Security-policyn Diskkryptering för BitLocker i Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . BitLocker-profilen i *Endpoint Security* är en fokuserad grupp inställningar som är dedikerade för att konfigurera BitLocker.

  Visa BitLocker-inställningarna som är tillgängliga i [BitLocker-profiler från policyn Diskkryptering](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Enhetskonfigurationsprofil för Endpoint Protection för BitLocker i Windows 10](#create-an-endpoint-security-policy-for-bitlocker)** . BitLocker-inställningarna är en av de tillgängliga inställningskategorierna för Endpoint Protection i Windows 10.

  Visa de BitLocker-inställningar som är tillgängliga för [BitLocker i Endpoint Protection-profiler från policyn Enhetskonfiguration](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune har en inbyggd [krypteringsrapport](encryption-monitor.md) som visar information om krypteringsstatusen för alla dina hanterade enheter. När Intune krypterar en Windows 10-enhet med BitLocker kan du visa och hämta BitLocker-återställningsnycklar när du visar krypteringsrapporten.
>
> Du kan också komma åt viktig information för BitLocker från dina enheter, som du hittar i Azure Active Directory (Azure AD).
[krypteringsrapport](encryption-monitor.md) som visar information om krypteringsstatusen för alla dina hanterade enheter.

## <a name="permissions-to-manage-bitlocker"></a>Behörighet att hantera BitLocker

För att kunna hantera BitLocker i Intune måste ditt konto ha rätt behörigheter för [rollbaserad åtkomstkontroll](../fundamentals/role-based-access-control.md) (RBAC) i Intune.

Nedan ser du BitLocker-behörigheterna som ingår i kategorin Fjärruppgifter och de inbyggda RBAC-roller som ger behörigheten:

- **Rotera Bitlocker-nycklar**
  - Supportavdelningen

## <a name="create-and-deploy-policy"></a>Skapa och distribuera policy

Använd någon av följande procedurer för att skapa de policytyper du vill använda.

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>Skapa en Endpoint Security-policy för BitLocker

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Endpoint Security** > **Diskkryptering** > **Skapa princip**.

3. Ange följande alternativ:
   1. **Plattform**: Windows 10 eller senare
   2. **Profil**: BitLocker

   ![Välj BitLocker-profilen](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. Konfigurera inställningarna för BitLocker enligt dina affärsbehov på sidan **Konfigurationsinställningar**.  

   Om du vill aktivera BitLocker tyst läser du [Tyst aktivering av BitLocker på enheter](#silently-enable-bitlocker-on-devices) i den här artikeln, där står ytterligare förutsättningar och den specifika inställningskonfiguration du måste använda.

   Välj **Nästa**.

5. På sidan **Omfång (taggar)** väljer du **Välj omfångstaggar** för att öppna fönstret Välj taggar och tilldela omfångstaggar till profilen.

   Fortsätt genom att välja **Nästa**.

6. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om att tilldela profiler finns i Tilldela profiler till användare och enheter.

   Välj **Nästa**.

7. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>Skapa en enhetskonfigurationsprofil för BitLocker

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande alternativ:
   1. **Plattform**: Windows 10 och senare
   2. **Profiltyp**: Endpoint Protection

   ![Välj BitLocker-profilen](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. Välj **Inställningar** > **Windows-kryptering**.

   ![BitLocker-inställningar](./media/encrypt-devices/bitlocker-settings.png)

5. Konfigurera inställningarna för BitLocker enligt dina affärsbehov.

   Om du vill aktivera BitLocker tyst läser du [Tyst aktivering av BitLocker på enheter](#silently-enable-bitlocker-on-devices) i den här artikeln, där står ytterligare förutsättningar och den specifika inställningskonfiguration du måste använda.

6. Välj **OK**.

7. Slutför konfigurationen av ytterligare inställningar och spara sedan profilen.

## <a name="manage-bitlocker"></a>Hantera BitLocker

Om du vill visa information om de enheter som tar emot BitLocker-policyer läser du [Övervaka diskkryptering](../protect/encryption-monitor.md). Du kan också visa och hämta återställningsnycklar för BitLocker när du visar krypteringsrapporten.

### <a name="silently-enable-bitlocker-on-devices"></a>Aktivera BitLocker på enheter tyst

Du kan konfigurera en BitLocker-princip som automatiskt och tyst aktiverar BitLocker på en enhet. Det innebär att BitLocker aktiveras utan att ett användargränssnitt visas för slutanvändaren, även om den användaren inte är lokal administratör på enheten.

**Enhetskrav**:

Enheter måste uppfylla följande villkor för att kunna användas för tyst aktivering av BitLocker:

- Enheter måste köra Windows 10 version 1809 eller senare
- Enheter måste vara Azure AD-kopplade  

**Konfiguration av BitLocker-princip**:

Följande två inställningar för *BitLocker-basinställningarna* måste vara konfigurerade i BitLocker-principen:

- **Varning för annan diskkryptering** = *Blockera*.
- **Låt standardanvändare aktivera kryptering under Azure AD-anslutning** = *Tillåt*

BitLocker-principen **får inte kräva** användning av en PIN-startkod eller startnyckel. När en PIN-startkod eller startnyckel för TPM *krävs* kan BitLocker inte aktiveras tyst eftersom det krävs interaktion från slutanvändaren.  Detta krav uppfylls genom följande tre *BitLocker OS-enhetsinställningar* i samma princip:

- **Kompatibel PIN-startkod för TPM** får inte vara inställd på *Kräv PIN-startkod med TPM*
- **Kompatibel startnyckel för TPM** får inte vara inställd på *Kräv startnyckel med TPM*
- **Kompatibel startnyckel och PIN-startkod för TPM** får inte vara inställd på *Kräv startnyckel och PIN-startkod med TPM*

### <a name="view-details-for-recovery-keys"></a>Visa information om återställningsnycklar

Intune ger åtkomst till Azure AD-bladet för BitLocker så att du kan visa BitLocker-nyckel-ID:n och återställningsnycklar för dina Windows 10-enheter från Intune-portalen. För att enheten ska vara nåbar måste dess nycklar vara deponerade till Azure AD.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Alla enheter**.

3. Välj en enhet i listan. Under *Övervaka* väljer du sedan **Återställningsnycklar**.
  
   När nycklar är tillgängliga i Azure AD finns följande information tillgänglig:
   - BitLocker-nyckel-ID
   - BitLocker-återställningsnyckel
   - Enhetstyp

   När nycklar inte finns i Azure AD visar Intune *Det gick inte att hitta någon BitLocker-nyckel för den här enheten*.

Information för BitLocker hämtas med hjälp av den [BitLocker-CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp). BitLocker-CSP stöds på Windows 10 version 1703 och senare samt för Windows 10 Pro version 1809 och senare.

### <a name="rotate-bitlocker-recovery-keys"></a>Rotera BitLocker-återställningsnycklar

Du kan använda en enhetsåtgärd i Intune för att fjärrrotera BitLocker-återställningsnyckeln på en enhet som kör Windows 10 version 1909 eller senare.

#### <a name="prerequisites"></a>Krav

Enheter måste uppfylla följande krav för att stödja rotation av BitLocker-återställningsnyckel:

- Enheterna måste köra Windows 10 version 1909 eller senare

- Azure Active Directory-anslutna och hybridanslutna enheter måste ha stöd för nyckelrotation aktiverat:

  - **Klientbaserad rotering av återställningslösenord**

  Den här inställningen finns under *Windows-kryptering* som en del av en enhetskonfigurationsprincip för Windows 10 slutpunktsskydd.

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>Så här roterar du BitLocker-återställningsnycklar

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Alla enheter**.

3. I listan över enheter som du hanterar väljer du en enhet, väljer **Mer** och sedan fjärråtgärden **BitLocker-nyckelrotering**.

4. På sidan **Översikt** på enheten väljer du **BitLocker-nyckelrotering**. Om du inte ser det här alternativet väljer du ellipsen ( **...** ) för att visa fler alternativ och väljer sedan fjärrenhetsåtgärden **BitLocker-nyckelrotering**.

   ![Välj ellipsen för att visa fler alternativ](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>Nästa steg

[Hantera FileVault-policy](../protect/encrypt-devices-filevault.md)

[Övervaka diskkryptering](../protect/encryption-monitor.md)
