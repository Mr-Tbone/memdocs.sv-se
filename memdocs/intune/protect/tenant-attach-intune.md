---
title: Använda Intune-principer med klientanslutna Configuration Manager-enheter | Microsoft Docs
description: Konfigurera klientanslutningen för Configuration Manager-enheter till administrationscentret för Microsoft Endpoint Manager så att du kan distribuera principer som stöds från Microsoft Intune till dessa enheter.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193673"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Konfigurera klientanslutning för att stödja Endpoint Security-principer från Intune

När du använder Configuration Manager-klientkopplingsscenario kan du distribuera Endpoint Security-principer från Intune till enheter som du hanterar med Configuration Manager. Om du vill använda det här scenariot måste du först konfigurera klientanslutning för Configuration Manager och aktivera samlingar av enheter från Configuration Manager för användning med Intune. När samlingar har aktiverats för användning använder du Microsoft Endpoint Manager admin center för att skapa och distribuera principer.

Följande principtyper stöds av Configuration Manager-enheter som är kopplade till klienten:

- Antivirusprincip för Endpoint Security
- Endpoint Security-principen Slutpunktsidentifiering och svarsprincip

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Krav för att använda Intune-principen för klientkoppling

Om du vill använda Intune Endpoint Security-principer med Configuration Manager-enheter måste du utföra följande konfigurationer i Configuration Manager-miljön. Det finns en [konfigurationsguide](#set-up-configuration-manager-to-support-intune-policies) i den här artikeln:

### <a name="general-requirements-for-tenant-attach"></a>Allmänna krav för klientkoppling

- **Konfigurera anslutning av klientorganisationen** – med scenariot *klientkoppling* kan du synkronisera samlingar av enheter från Configuration Manager till administrationscentret för Microsoft Endpoint Manager. Sedan kan du använda administrationscentret till att distribuera principer som stöds till samlingarna.

  Anslutning av klientorganisationen konfigureras ofta med samhantering, men du kan konfigurera anslutningen av klientorganisationen separat.

- **Synkronisera Configuration Manager-samlingar** – när du konfigurerar anslutning av klientorganisationen kan du välja de Configuration Manager-enhetssamlingar som ska synkroniseras med administrationscentret för Microsoft Endpoint Manager. Du kan också återgå senare och ändra de enhetssamlingar du synkroniserar. Principer som stöds för Configuration Manager-enheter kan bara tilldelas till samlingar du har synkroniserat.

  När du har valt samlingar att synkronisera måste du aktivera dem för användning med Endpoint Security-principer från Intune.

- **Behörigheter till Azure AD-** – om du vill slutföra installationen av klientkoppling behöver du ett konto med globala administratörsbehörigheter till din Azure-prenumeration.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Särskilda krav för Endpoint Security-principer för Intune

- **Antivirus-princip** (*förhandsversion*):

  - **Configuration Manager** – Följande miljöer stöds:

    - **Nuvarande gren av Configuration Manager version 2006 eller senare** – stöd för Intune Antivirus-principer har lagts till i den aktuella grenversionen.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Klientorganisation för Microsoft Defender Advanced Threat Protection** – din Microsoft Defender ATP-klientorganisation måste vara integrerad med Microsoft Endpoint Manager-klientorganisationen (Intune-prenumerationen).  Läs mer i [Använda Microsoft Defender ATP](advanced-threat-protection.md) i Intune-dokumentationen.

- **Slutpunktsidentifiering och svarsprincip**:

  - **Configuration Manager** – Följande miljöer stöds:

    - **Configuration Manager teknisk förhandsversion 2003 eller senare** – stöd för Intune slutpunktsidentifierings- och svarsprinciper för lades till i den tekniska förhandsversionen 2003.

    - **Nuvarande gren av Configuration Manager version 2002 eller senare** – om du använder Configuration Manager med version 2002 måste du installera konsoluppdateringen **Configuration Manager 2002 Hotfix (KB4563473)** . Den här uppdateringen aktiverar stöd i Configuration Manager 2002 för användning av Endpoint Security-principer.

  - **Klientorganisation för Microsoft Defender Advanced Threat Protection** – din Microsoft Defender ATP-klientorganisation måste vara integrerad med Microsoft Endpoint Manager-klientorganisationen (Intune-prenumerationen).  Läs mer i [Använda Microsoft Defender ATP](advanced-threat-protection.md) i Intune-dokumentationen.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Konfigurera Configuration Manager med stöd för Intune-principer

Innan du kan distribuera Intune-principer till Configuration Manager-enheter ska du utföra konfigurationerna som beskrivs i följande avsnitt. Dessa konfigurationer registrerar dina Configuration Manager-enheter med Microsoft Defender ATP och gör det möjligt för dem att arbeta med Intune-principerna.

Följande uppgifter har slutförts i Configuration Manager-konsolen. Om du inte är bekant med Configuration Manager bör du utföra de här uppgifterna tillsammans med en Configuration Manager-administratör.

1. [Installera uppdateringen för Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Aktivera anslutning av klientorganisationen](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Välja vilka samlingar som ska synkroniseras](#task-3-select-collections-to-synchronize)
4. [Aktivera samlingar som stöder Intune-principer](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Mer information om hur du använder Microsoft Defender ATP med Configuration Manager finns i följande artiklar i Configuration Manager-innehållet:
>
> - [Registrera Configuration Manager-klienter i Microsoft Defender ATP via administrationscentret för Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Ansluta klientorganisationer i Microsoft Endpoint Manager: enhetssynkronisering och enhetsåtgärder](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Uppgift 1: Installera uppdateringen för Configuration Manager

Om du använder den nuvarande grenen av Configuration Manager version 2002 installerar du följande uppdatering i konsolen som lägger till stöd för de Endpoint Security-säkerhetsprinciper som du distribuerar från administrationscentret för Microsoft Endpoint Manager.

**Uppdateringsinformation**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

Om du vill installera uppdateringen följer du anvisningarna i [Installera uppdateringar i konsolen](../../configmgr/core/servers/manage/install-in-console-updates.md) i Configuration Manager-dokumentationen.

När du har installerat uppdateringen går du tillbaka hit och fortsätter konfigurera din miljö med stöd för Endpoint Security-principer från administrationscentret för Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Uppgift 2: Konfigurera anslutning av klientorganisationen och synkronisera samlingar

Med anslutning av klientorganisationen anger du samlingar av enheter från Configuration Manager-distributionen som ska synkroniseras med administrationscentret för Microsoft Endpoint Manager. När samlingarna synkroniseras kan du använda administrationscentret till att visa information om enheterna och distribuera Endpoint Security-principer från Intune till dem.

Mer information om anslutning av klientorganisationen finns i [Aktivera anslutning av klientorganisation](../../configmgr/tenant-attach/device-sync-actions.md) i Configuration Manager-dokumentationen.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Aktivera anslutning av klientorganisationen när samhantering inte har aktiverats

> [!TIP]
> Du kan använda guiden **Konfiguration av samhantering** i Configuration Manager-konsolen när du ska aktivera anslutning av klientorganisationen, men du behöver inte aktivera samhantering.
>
> Om du planerar att aktivera samhantering bör du vara bekant med fenomenet samhantering, vilka förutsättningar som gäller och hur du hanterar arbetsbelastningar innan du fortsätter. Läs mer i [Vad är samhantering?](../../configmgr/comanage/overview.md) i Configuration Manager-dokumentationen.

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.
2. Klicka på **Konfigurera samhantering** i menyfliksområdet för att öppna guiden.
3. På sidan **Registrering av klientorganisation** väljer du **AzurePublicCloud** som miljö. Du kan inte använda molnet Azure Government.
   1. Klicka på **Logga in**. Logga in med ditt *globala administratörskonto*.

   2. Se till att alternativet **Ladda upp till administrationscentret för Microsoft Endpoint Manager** är valt på sidan **Registrering av klientorganisation**.

   3. Ta bort bockmarkeringen från **Aktivera automatisk klientregistrering för samhantering**.

      När det här alternativet är valt visar guiden ytterligare sidor för att slutföra konfigurationen av samhanteringen. Mer information finns i [Aktivera samhantering](../../configmgr/comanage/how-to-enable.md) i Configuration Manager-dokumentationen.

     ![Konfigurera anslutning av klientorganisationen](./media/tenant-attach-intune/tenant-onboarding.png)

4. Klicka på **Nästa** och sedan **Ja** för att godkänna meddelandet **Skapa AAD-program**. Den här åtgärden etablerar ett huvudnamn för tjänsten och skapar en Azure AD-programregistrering för att underlätta synkroniseringen av samlingar till administrationscentret för Microsoft Endpoint Manager.

5. På sidan **Konfigurera uppladdning** konfigurerar du vilka samlingar du vill synkronisera. Du kan begränsa konfigurationen till en eller flera enhetssamlingar eller använda den rekommenderade inställningen **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**.

   > [!TIP]
   > Du kan hoppa över att välja samlingar nu och senare använda informationen i följande uppgift, uppgift 3, för att konfigurera vilka samlingar som ska synkronisera med Microsoft Endpoint Manager-administrationscentret.

6. Klicka på **Sammanfattning** för att granska dina val och klicka sedan på **Nästa**.

7. När guiden är slutförd klickar du på **Stäng**.

   Nu är anslutningen till klientorganisationen konfigurerad och du har valt samlingar att synkronisera till administrationscentret för Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Aktivera anslutning av klientorganisationen när du redan använder samhantering

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.

2. Högerklicka på inställningarna för samhantering och välj **Egenskaper**.

3. På fliken **Konfigurera uppladdning** väljer du **Ladda upp till administrationscentret för Microsoft Endpoint Manager**. Klicka på **Använd**.

   Standardinställningen för uppladdning av enheter är **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Du kan också välja att begränsa konfigurationen till en eller flera enhetssamlingar.

   ![Visa fliken Egenskaper för samhantering](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > Du kan hoppa över att välja samlingar nu och senare använda informationen i följande uppgift, uppgift 3, för att konfigurera vilka samlingar som ska synkronisera med Microsoft Endpoint Manager-administrationscentret.

4. Logga in med ditt *globala administratörskonto* när du uppmanas till det.

5. Klicka på **Ja** för att godkänna meddelandet **Skapa AAD-program**. Den här åtgärden etablerar ett huvudnamn för tjänsten och skapar en Azure AD-programregistrering för att underlätta synkroniseringen.

6. Klicka på **OK** för att stänga egenskaperna för samhantering när du har gjort dina ändringar.

   Nu är anslutningen till klientorganisationen konfigurerad och du har valt samlingar att synkronisera till administrationscentret för Microsoft Endpoint Manager.

### <a name="task-3-select-collections-to-synchronize"></a>Uppgift 3: Välja vilka samlingar som ska synkroniseras

När du har konfigurerat anslutningen av klientorganisationen kan du välja vilka samlingar som ska synkroniseras. Om du inte redan har synkroniserat samlingar eller om du behöver konfigurera om vilka du ska synkronisera kan du redigera egenskaperna för samhantering i Configuration Manager-konsolen.

#### <a name="select-collections"></a>Välja samlingar

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.

2. Högerklicka på inställningarna för samhantering och välj **Egenskaper**.

3. På fliken **Konfigurera uppladdning** väljer du **Ladda upp till administrationscentret för Microsoft Endpoint Manager**. Klicka på **Använd**.

   Standardinställningen för uppladdning av enheter är **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Du kan också välja att begränsa konfigurationen till en eller flera enhetssamlingar.

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Uppgift 4: Aktivera samlingar för slutpunktssäkerhetsprinciper

När du har konfigurerat samlingarna för synkronisering till Microsoft Endpoint Manager-administrationscenter kan du aktivera dessa samlingar för att arbeta med slutpunktssäkerhetsprinciper. När du aktiverar samlingar av enheter för att arbeta med säkerhetsprinciper för slutpunkter från Intune, konfigurerar du de enheter i dessa samlingar som ska publiceras med Microsoft Defender ATP.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Aktivera samlingar som ska användas med slutpunktssäkerhetsprinciper

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Nästa steg

- [Konfigurera slutpunktssäkerhetsprinciper](endpoint-security-policy.md#create-an-endpoint-security-policy) för *Antivirus* och *Slutpunktsidentifiering och svar*.

- Läs mer om [Slutpunktsidentifiering och svar](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) i dokumentationen för Microsoft Defender ATP.