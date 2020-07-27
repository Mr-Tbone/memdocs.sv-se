---
title: Kryptera macOS-enheter med FileVault-diskkryptering med Intune
titleSuffix: Microsoft Intune
description: Kryptera macOS-enheter med inbyggda krypteringsmetoder som FileVault och hantera återställningsnycklarna för de krypterade enheterna på Intune-portalen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460492"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Använda FileVault-diskkryptering för macOS med Intune

Intune stöder macOS FileVault-diskkryptering. FileVault är ett program för kryptering av hela diskar som ingår i macOS. Du kan använda Intune för att konfigurera FileVault på enheter som kör **MacOS 10.13 eller senare**.

Använd någon av följande principtyper för att konfigurera FileVault på dina hanterade enheter:

- **[Endpoint Security-säkerhetsprincip för macOS FileVault](#create-endpoint-security-policy-for-filevault)** . FileVault-profilen i *Endpoint Security* är en fokuserad grupp med inställningar som är dedikerade för att konfigurera FileVault.

  Visa [FileVault-inställningar som är tillgängliga i profiler för diskkrypteringsprincip](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Enhetskonfigurationsprofil för Endpoint Protection för macOS FileVault](#create-endpoint-security-policy-for-filevault)** . FileVault-inställningar är en av de tillgängliga inställningskategorierna för macOS-slutpunktsskydd. Mer information om hur du använder en profil för enhetskonfiguration finns [Skapa en enhetsprofil i Intune](../configuration/device-profile-create.md).

  Visa de [FileVault-inställningar som är tillgängliga för i Endpoint Protection-profiler från policyn Enhetskonfiguration](../protect/endpoint-protection-macos.md#filevault).

Information om hur du hanterar BitLocker för Windows 10 finns i [Hantera BitLocker-princip](../protect/encrypt-devices.md).

> [!TIP]
> Intune har en inbyggd [krypteringsrapport](encryption-monitor.md) som visar information om krypteringsstatusen för alla dina hanterade enheter.

När du har skapat en princip för att kryptera enheter med FileVault tillämpas principen på enheter i två steg. Först förbereds enheten så att Intune kan hämta och säkerhetskopiera återställningsnyckeln. Den här åtgärden kallas deponering eller deposition. När nyckeln har deponerats kan diskkrypteringen starta.

Förutom att använda Intune-principer för att kryptera en enhet med FileVault, kan du distribuera principer till en hanterad enhet för att Intune ska kunna [hantera FileVault när enheten har krypterats av användaren](#assume-management-of-filevault-on-previously-encrypted-devices). Det här scenariot kräver att enheten tar emot FileVault-principer från Intune, samt att användaren laddar upp sin personliga återställningsnyckel till Intune.

Användargodkänd enhetsregistrering krävs för att FileVault ska fungera på en enhet. Användaren måste godkänna hanteringsprofilen manuellt i systeminställningarna för att registreringen ska betraktas som användargodkänd.

## <a name="permissions-to-manage-filevault"></a>Behörighet att hantera FileVault

För att kunna hantera FileVault i Intune måste ditt konto ha rätt behörigheter för [rollbaserad åtkomstkontroll](../fundamentals/role-based-access-control.md) (RBAC) i Intune.

Nedan visas de FileVault-behörigheter som ingår i kategorin **Fjärruppgifter** och de inbyggda RBAC-roller som ger behörigheten:

- **Hämta FileVault-nyckel**:
  - Supportavdelningen
  - Slutpunktssäkerhetshanteraren

- **Rotera FileVault-nyckel**
  - Supportavdelningen

## <a name="create-device-configuration-policy-for-filevault"></a>Skapa en princip för enhetskonfiguration för FileVault

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.

3. På sidan **Skapa en profil** anger du följande alternativ och klickar sedan på **Skapa**:
   - **Plattform**: macOS
   - **Profil**: Endpoint Protection

   ![Välj FileVault-profilen](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. På sidan **Grundläggande** anger du följande egenskaper:

   - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Ett bra namn kan till exempel innehålla profiltypen och plattformen.

   - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

5. På sidan **Konfigurationsinställningar** väljer du **FileVault** för att expandera de tillgängliga inställningarna:

   > [!div class="mx-imgBorder"]
   > ![FileVault-inställningar](./media/encrypt-devices-filevault/filevault-settings.png)

6. Konfigurera följande inställningar:
  
   - För *Aktivera FileVault* väljer du **Ja**.

   - För *Återställningsnyckeltyp* väljer du **Personlig nyckel**.

   - För *Beskrivning av depositionsplats för privat återställningsnyckel* lägger du till ett meddelande som hjälper användarna att [hämta återställningsnyckeln](#retrieve-a-personal-recovery-key) för sina enheter. Den här informationen kan vara användbar för dina användare när du använder inställningen för rotation av personliga återställningsnycklar, som automatiskt kan generera en ny återställningsnyckel för en enhet med jämna mellanrum.

     Exempel: Om du vill hämta en förlorad eller nyligen roterad återställningsnyckel loggar du in på webbplatsen för Intune-företagsportalen från valfri enhet. På portalen går du till *Enheter* och väljer den enhet där FileVault är aktiverat och väljer sedan *Hämta återställningsnyckel*. Den aktuella återställningsnyckeln visas.

   Konfigurera de återstående [FileVault](endpoint-protection-macos.md#filevault)-inställningarna efter dina affärsbehov och välj **Nästa**.

7. På sidan **Omfång (taggar)** väljer du **Välj omfångstaggar** för att öppna fönstret Välj taggar och tilldela omfångstaggar till profilen.

   Fortsätt genom att välja **Nästa**.

8. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om att tilldela profiler finns i Tilldela profiler till användare och enheter.
Välj **Nästa**.

9. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="create-endpoint-security-policy-for-filevault"></a>Skapa en Endpoint Security-princip för FileVault

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktsskydd** > **Diskkryptering** > **Skapa princip**.

3. På sidan **Grundläggande** anger du följande egenskaper och väljer sedan **Nästa**.
   - **Plattform**: macOS
   - **Profil**: FileVault

   ![Välj FileVault-profilen](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. På sidan **Konfigurationsinställningar**:
   1. Ställ in *Aktivera FileVault* på **Ja**.
   2. För *Typ av återställningsnyckel* stöds endast **Privat återställningsnyckel**.
   3. Konfigurera ytterligare inställningar för att uppfylla dina krav.

   Du kan lägga till ett meddelande som hjälper användarna [att hämta återställningsnyckeln](#retrieve-a-personal-recovery-key) för deras enheter. Den här informationen kan vara användbar för dina användare när du använder inställningen för rotation av personliga återställningsnycklar, som automatiskt kan generera en ny återställningsnyckel för en enhet med jämna mellanrum.

   Exempel: Om du vill hämta en förlorad eller nyligen roterad återställningsnyckel loggar du in på webbplatsen för Intune-företagsportalen från valfri enhet. På portalen går du till Enheter och väljer den enhet där FileVault är aktiverat och väljer sedan *Hämta återställningsnyckel*. Den aktuella återställningsnyckeln visas.

5. När du har konfigurerat inställningarna väljer du **Nästa**.

6. På sidan **Omfång (taggar)** väljer du **Välj omfångstaggar** för att öppna fönstret Välj taggar för att tilldela omfångstaggar till profilen.

   Fortsätt genom att välja **Nästa**.

7. På sidan **Tilldelningar** väljer du de grupper som profilen ska tillämpas på. Mer information om att tilldela profiler finns i Tilldela profiler till användare och enheter.
Välj **Nästa**.

8. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="manage-filevault"></a>Hantera FileVault

Om du vill visa information om enheter som tar emot FileVault-principer läser du [Övervaka diskkryptering](../protect/encryption-monitor.md).

När Intune först krypterar en macOS-enhet med FileVault skapas en personlig återställningsnyckel. Efter krypteringen visas den personliga nyckeln en enda gång för enhetsanvändaren.

För hanterade enheter kan Intune deponera en kopia av den personliga återställningsnyckeln. Deponeringen av nycklar gör att Intune-administratörer kan rotera nycklar för att skydda enheter, och användare för att återställa en förlorad eller roterad personlig återställningsnyckel.

Intune deponerar en återställningsnyckel när Intune-principen krypterar en enhet, eller när en användare laddar upp sin återställningsnyckel för en enhet som är krypterad manuellt.

När Intune har deponerat den personliga återställningsnyckeln:

- Administratörer kan hantera och rotera FileVault-återställningsnycklar för alla hanterade macOS-enheter med hjälp av Intunes krypteringsrapport.
- Administratörer kan endast se den personliga återställningsnyckeln för hanterade macOS-enheter som har markerats som *företag*. De kan inte se återställningsnyckeln för personliga enheter.
- Användarna kan se och [hämta sin personliga återställningsnyckel från en plats som stöds](#retrieve-a-personal-recovery-key). På företagsportalens webbplats kan användaren till exempel välja att *Hämta återställningsnyckel* som en fjärrenhetsåtgärd.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Hantera FileVault på tidigare krypterade enheter

Intune kan hantera FileVault-diskkryptering på macOS-enheter som har krypterats med hjälp av Intune-principer. Intune kan också ta över hanteringen av FileVault på enheter som har krypterats av enhetsanvändarna i stället för Intune-principen.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Förutsättningar för att kunna hantera FileVault

Följande villkor måste vara uppfyllda för att kunna hantera tidigare krypterade enheter:

1. **Distribuera en FileVault-princip till enheten**. Den tidigare krypterade enheten måste ta emot en princip från Intune som aktiverar FileVault-diskkrypteringen.

   I det här scenariot kommer principen inte att kryptera eller omkryptera enheten. I stället aktiverar principen att Intune börjar hantera den FileVault-kryptering som redan finns på enheten.  Du kan antingen använda en princip för diskkryptering av slutpunktssäkerhet, eller en princip för slutpunktsskydd av enhetskonfigurationer med FileVault.

   Se [Skapa och distribuera principer](#create-device-configuration-policy-for-filevault).

2. **Användarna laddar upp sin personliga återställningsnyckel till Intune**.  När enheten har tagit emot FileVault-principen, uppmanas enhetsanvändaren som krypterade enheten att ladda upp sin personliga återställningsnyckel i Intune. Om nyckeln har angetts börjar Intune hantera FileVault-krypteringen och en ny personlig återställningsnyckel skapas för enheten och användaren.

   > [!IMPORTANT]
   > Intune varnar inte användarna om att de måste ladda upp sin personliga återställningsnyckel för att slutföra krypteringen. Använd i stället dina vanliga IT-kommunikationskanaler för att varna användare som tidigare har krypterat sin macOS-enhet med FileVault, att de måste ladda upp sin personliga återställningsnyckel i Intune.  
   >
   > Beroende på din efterlevnadsprincip kan enheter blockeras från åtkomst till företagsresurser tills Intune har börjat hantera FileVault-kryptering på enheten.

#### <a name="upload-a-personal-recovery-key"></a>Ladda upp en personlig återställningsnyckel

Om du vill att Intune ska kunna hantera FileVault på en tidigare krypterad enhet, måste enhetsanvändarna använda företagsportalens webbplats när de laddar upp sina nuvarande personliga återställningsnycklar för enheten i Intune.  Vid uppladdningen roterar Intune nyckeln för att skapa en ny personlig återställningsnyckel. Den lagras sedan av Intune för eventuell framtida återställning.

På företagsportalens webbplats letar användaren upp sin krypterade macOS-enhet och väljer alternativet **Lagra återställningsnyckel**. Så snart den personliga återställningsnyckeln har angetts, försöker Intune att rotera nyckeln för att generera en ny nyckel. Rotationen görs för att verifiera att den angivna nyckeln är korrekt för den enheten. Den nya nyckeln lagras och hanteras av Intune för framtida användning, om användaren behöver återställa sin enhet.

Om nyckelrotationen misslyckas har enheten inte bearbetat FileVault-principen, eller så är nyckeln som angavs inte korrekt för enheten.

Efter en lyckad rotation kan användaren[hämta sin nya personliga återställningsnyckel från en plats som stöds](#retrieve-a-personal-recovery-key).

 Se [slutanvändarinnehåll för uppladdning av den personliga återställningsnyckeln](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> För enheter som har krypterats av användaren och inte av Intune, kan Intune inte hantera enheternas FileVault-kryptering förrän enheten har tagit emot en FileVault-princip och enhetsanvändaren har laddat upp sin personliga återställningsnyckel.

### <a name="retrieve-a-personal-recovery-key"></a>Hämta en personlig återställningsnyckel

För en macOS-enhet där FileVault-krypteringen hanteras av Intune, kan slutanvändarna hämta sin personliga återställningsnyckel (FileVault-nyckel) från följande platser med hjälp av valfri enhet:

- Företagsportalens webbplats
- Företagsportalappen i iOS/iPadOS
- Android-företagsportalsapp
- Intune-appen

Administratörer kan se personliga återställningsnycklar för krypterade macOS-enheter som har markerats som *företagsenheter*. De kan inte se återställningsnyckeln för personliga enheter.

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
