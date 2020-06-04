---
title: Kryptera macOS-enheter med FileVault-diskkryptering med Intune
titleSuffix: Microsoft Intune
description: Kryptera macOS-enheter med inbyggda krypteringsmetoder som FileVault och hantera återställningsnycklarna för de krypterade enheterna på Intune-portalen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: 99facc87d068239962ab0d40874aa081f5e19189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989685"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Använda FileVault-diskkryptering för macOS med Intune

Intune stöder macOS FileVault-diskkryptering. FileVault är ett program för kryptering av hela diskar som ingår i macOS. Du kan använda Intune för att konfigurera FileVault på enheter som kör **MacOS 10.13 eller senare**.

Använd någon av följande principtyper för att konfigurera FileVault på dina hanterade enheter:

- **[Endpoint Security-säkerhetsprincip för macOS FileVault](#create-an-endpoint-security-policy-for-filevault)** . FileVault-profilen i *Endpoint Security* är en fokuserad grupp med inställningar som är dedikerade för att konfigurera FileVault.

  Visa [FileVault-inställningar som är tillgängliga i profiler för diskkrypteringsprincip](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Enhetskonfigurationsprofil för Endpoint Protection för macOS FileVault](#create-an-endpoint-security-policy-for-filevault)** . FileVault-inställningar är en av de tillgängliga inställningskategorierna för macOS-slutpunktsskydd. Mer information om hur du använder en profil för enhetskonfiguration finns [Skapa en enhetsprofil i Intune](../configuration/device-profile-create.md).

  Visa de [FileVault-inställningar som är tillgängliga för i Endpoint Protection-profiler från policyn Enhetskonfiguration](../protect/endpoint-protection-macos.md#filevault).

Information om hur du hanterar BitLocker för Windows 10 finns i [Hantera BitLocker-princip](../protect/encrypt-devices.md).

> [!TIP]
> [krypteringsrapport](encryption-monitor.md) som visar information om krypteringsstatusen för enheter, för alla dina hanterade enheter.

När du har skapat en princip för att kryptera enheter med FileVault tillämpas principen på enheter i två steg. Först förbereds enheten så att Intune kan hämta och säkerhetskopiera återställningsnyckeln. Den här åtgärden kallas deponering eller deposition. När nyckeln har deponerats kan diskkrypteringen starta.

Användargodkänd enhetsregistrering krävs för att FileVault ska fungera på en enhet. Användaren måste godkänna hanteringsprofilen manuellt i systeminställningarna för att registreringen ska betraktas som användargodkänd.

## <a name="permissions-to-manage-filevault"></a>Behörighet att hantera FileVault

För att kunna hantera FileVault i Intune måste ditt konto ha rätt behörigheter för [rollbaserad åtkomstkontroll](../fundamentals/role-based-access-control.md) (RBAC) i Intune.

Nedan visas de FileVault-behörigheter som ingår i kategorin **Fjärruppgifter** och de inbyggda RBAC-roller som ger behörigheten:

- **Hämta FileVault-nyckel**:
  - Supportavdelningen
  - Slutpunktssäkerhetshanteraren

- **Rotera FileVault-nyckel**
  - Supportavdelningen

## <a name="create-and-deploy-policy"></a>Skapa och distribuera princip

### <a name="create-an-endpoint-security-policy-for-filevault"></a>Skapa en säkerhetsprincip för slutpunkt för FileVault

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktsskydd** > **Diskkryptering** > **Skapa princip**.

3. På sidan **Grundläggande** anger du följande egenskaper och väljer sedan **Nästa**.
   1. **Plattform**: macOS
   2. **Profil**: FileVault

   ![Välj FileVault-profilen](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. På sidan **Konfigurationsinställningar**:
   1. Ställ in *Aktivera FileVault* på **Ja**.
   2. För *Typ av återställningsnyckel* stöds endast **Privat återställningsnyckel**.
   3. Konfigurera ytterligare inställningar för att uppfylla dina krav.

   Överväg att lägga till ett meddelande som hjälper användarna att hämta återställningsnyckeln för deras enheter. Den här informationen kan vara användbar för dina användare när du använder inställningen för rotation av personliga återställningsnycklar, som automatiskt kan generera en ny återställningsnyckel för en enhet med jämna mellanrum.

   Exempel: Om du vill hämta en förlorad eller nyligen roterad återställningsnyckel loggar du in på webbplatsen för Intune-företagsportalen från valfri enhet. På portalen går du till Enheter och väljer den enhet där FileVault är aktiverat och väljer sedan *Hämta återställningsnyckel*. Den aktuella återställningsnyckeln visas.

5. När du har konfigurerat inställningarna väljer du **Nästa**.

6. På sidan **Omfång (taggar)** väljer du **Välj omfångstaggar** för att öppna fönstret Välj taggar för att tilldela omfångstaggar till profilen.

   Fortsätt genom att välja **Nästa**.

7. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om hur du tilldelar profiler finns i Tilldela användar- och enhetsprofiler.
Välj **Nästa**.

8. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

### <a name="create-a-device-configuration-policy-for-filevault"></a>Skapa en princip för enhetskonfiguration för FileVault

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. Ange följande alternativ:
   1. **Plattform**: macOS
   2. **Profil**: Endpoint Protection

   ![Välj FileVault-profilen](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Välj **Inställningar** > **FileVault**.

   ![FileVault-inställningar](./media/encrypt-devices-filevault/filevault-settings.png)

5. För *FileVault* väljer du **Aktivera**.

6. För *Typ av återställningsnyckel* stöds endast **Privat nyckel**.

   Överväg att lägga till ett meddelande som hjälper användarna att hämta återställningsnyckeln för deras enheter. Den här informationen kan vara användbar för dina användare när du använder inställningen för rotation av personliga återställningsnycklar, som automatiskt kan generera en ny återställningsnyckel för en enhet med jämna mellanrum.

   Exempel: Om du vill hämta en förlorad eller nyligen roterad återställningsnyckel loggar du in på webbplatsen för Intune-företagsportalen från valfri enhet. På portalen går du till *Enheter* och väljer den enhet där FileVault är aktiverat och väljer sedan *Hämta återställningsnyckel*. Den aktuella återställningsnyckeln visas.

7. Konfigurera de återstående [FileVault](endpoint-protection-macos.md#filevault)inställningarna efter dina affärsbehov och välj **OK**.

8. Slutför konfigurationen av ytterligare inställningar och spara sedan profilen.

## <a name="manage-filevault"></a>Hantera FileVault

Om du vill visa information om enheter som tar emot FileVault-principer läser du [Övervaka diskkryptering](../protect/encryption-monitor.md).

När Intune först krypterar en macOS-enhet med FileVault skapas en personlig återställningsnyckel. Efter krypteringen visas den personliga nyckeln en enda gång för enhetsanvändaren.

För hanterade enheter kan Intune deponera en kopia av den personliga återställningsnyckeln. Deponeringen av nycklar gör att Intune-administratörer kan rotera nycklar för att skydda enheter, och användare för att återställa en förlorad eller roterad personlig återställningsnyckel.

När Intune har krypterat en macOS-enhet med FileVault:

- Administratörer kan visa och hantera återställningsnycklar för FileVault med hjälp av Intunes krypteringsrapport.
- Användare kan visa en enhets personliga återställningsnyckel från webbföretagsportalen på enheten. Från Intune-företagsportalen väljer du den krypterade macOS-enheten och väljer sedan Hämta återställningsnyckel som en fjärrenhetsåtgärd.

> [!IMPORTANT]
> Enheter som krypteras av användare, och inte av Intune, kan inte hanteras av Intune. Det innebär att Intune inte kan deponera den personliga återställningsnyckeln för dessa enheter, eller hantera rotationen av återställningsnyckeln. Innan Intune kan hantera FileVault och återställningsnycklar för enheten måste användaren dekryptera enheten och sedan låta Intune kryptera enheten.

### <a name="retrieve-personal-recovery-key"></a>Hämta privat återställningsnyckel

För en macOS-enhet som har krypterats av Intune kan slutanvändare hämta sin privata återställningsnyckel (FileVault Key) med hjälp av iOS-företagsportalappen, Android-företagsportalappen eller Android Intune-appen.

Den enhet som har den personliga återställningsnyckeln måste registreras med Intune och krypteras med FileVault via Intune. Med hjälp av iOS-företagsportalappen, Android-företagsportalsappen, Android Intune-appen eller företagsportalwebbplatsen kan användaren se den **FileVault**-återställningsnyckel som krävs för att få åtkomst till deras Mac-enheter.

Enhetsanvändare kan välja **Enheter** > *den krypterade och registrerade macOS-enheten* > **Hämta återställningsnyckel**. Webbläsaren visar webbföretagsportalen och visar återställningsnyckeln.

### <a name="rotate-recovery-keys"></a>Rotera återställningsnycklar

Intune stöder flera alternativ för att rotera och återställa personliga återställningsnycklar. En nyckel kan exempelvis roteras om den nuvarande personliga nyckeln försvinner eller misstänks vara utsatt för risk.

- **Automatisk rotation**: Som administratör kan du konfigurera FileVault-inställningen Rotering av privat återställningsnyckel för att automatiskt generera nya återställningsnycklar med jämna mellanrum. När en ny nyckel skapas för en enhet visas inte nyckeln för användaren. Användaren måste i stället få nyckeln från en administratör eller via företagsportalappen.

- **Manuell rotation**: Som administratör kan du visa information om en enhet som du hanterar med Intune och som krypteras med FileVault. Du kan sedan välja att manuellt rotera återställningsnyckeln för företagsenheter. Du kan inte rotera återställningsnycklar för personliga enheter.

  Så här roterar du en återställningsnyckel:

  1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

  2. Välj **Enheter** > **Alla enheter**.

  3. I listan med enheter väljer du den enhet som är krypterad och som du vill rotera nyckeln för. Välj  **Återställningsnycklar** under Övervaka.
  
  4. Välj **Rotera FileVault-återställningsnyckel** i fönstret Återställningsnycklar.

     Nästa gång enheten checkar in med Intune roteras den personliga nyckeln. Om det behövs kan den nya nyckeln hämtas av användaren via företagsportalen.

### <a name="recover-recovery-keys"></a>Återställa återställningsnycklar

- **Administratör**: Administratörer kan inte visa personliga återställningsnycklar för enheter som är krypterade med FileVault.

- **Slutanvändare**: Slutanvändare använder webbplatsen för företagsportalen från valfri enhet för att visa den aktuella personliga återställningsnyckeln för någon av deras hanterade enheter. Du kan inte visa återställningsnycklar från appen Företagsportal.

  Så här visar du en återställningsnyckel:
  
  1. Logga in på webbplatsen för *Intune-företagsportalen* från valfri enhet.

  2. På portalen går du till **Enheter** och väljer den macOS-enhet som är krypterad med FileVault.

  3. Välj **Hämta återställningsnyckel**. Den aktuella återställningsnyckeln visas.

## <a name="next-steps"></a>Nästa steg

[Hantera BitLocker-princip](../protect/encrypt-devices.md)

[Övervaka diskkryptering](../protect/encryption-monitor.md)
