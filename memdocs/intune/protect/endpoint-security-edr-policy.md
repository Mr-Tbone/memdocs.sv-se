---
title: Hantera inställningar för Slutpunktsidentifiering och svar med Endpoint Security-policyer i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer för enheter du hanterar med Endpoint Security-policyn Slutpunktsidentifiering och svar i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
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
ms.openlocfilehash: d0ba328f1976d0463c6be042dfd6f8a7570d6dac
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206340"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Endpoint Security-policyn Slutpunktsidentifiering och svar i Intune

När du integrerar Defender Advanced Threat Protection (Defender ATP) med Intune kan du använda Endpoint Security-policyn Slutpunktsidentifiering och svar (EDR) till att hantera EDR-inställningarna och registrera enheter i Defender ATP.

Funktionerna i Defender ATP Slutpunktsidentifiering och svar identifierar attacker nära nog i realtid så att du kan åtgärda dem. Säkerhetsanalytiker kan effektivt prioritera aviseringar, få insyn i hela omfattningen av ett intrång och vidta svarsåtgärder för att motverka hot.

EDR-policyerna omfattar bland annat plattformsspecifika profiler för hantering av inställningar för EDR. Profilerna innehåller automatiskt ett *registreringspaket* för Defender ATP. Registreringspaket anger hur enheter ska fungera med Defender ATP. När en enhet registrerar sig kan du börja använda hotinformation från enheten.

EDR-policyer distribueras till grupper av enheter i Azure Active Directory (Azure AD) som du hanterar med Intune, och till samlingar av lokala enheter som du hanterar med Configuration Manager, inklusive Windows-servrar. Du behöver olika registreringspaket för EDR-policyerna för de olika hanteringsvägarna. Därför ska du skapa separata EDR-policyer för de olika typer av enheter du hanterar.

> [!TIP]
> Stödet för enheter du hanterar med Configuration Manager finns i *offentlig förhandsversion*.

Du hittar Endpoint Security-policyn Slutpunktsidentifiering och svar under *Hantera* i noden **Endpoint Security** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visa [inställningar för Slutpunktsidentifiering och svar](endpoint-security-edr-profile-settings.md).

## <a name="prerequisites-for-edr-policies"></a>Förutsättningar för EDR-policyer

**Allmänt**:

- **Klientorganisation för Microsoft Defender Advanced Threat Protection** – din Defender ATP-klientorganisation måste vara integrerad med Microsoft Endpoint Manager-klientorganisationen (Intune-prenumerationen) innan du kan skapa EDR-principer. Läs mer i [Använda Microsoft Defender ATP](advanced-threat-protection.md) i Intune-dokumentationen.

**Så här använder du enheter från Configuration Manager**:

Om du vill använda EDR-policyer med Configuration Manager-enheter måste du utföra följande konfigurationer i Configuration Manager-miljön. Det finns en [konfigurationsguide](#set-up-configuration-manager-to-support-edr-policy) i den här artikeln:

- **Configuration Manager med version 2002 eller senare** – webbplatsen måste köra Configuration Manager 2002 eller senare.

- **Installera Configuration Manager-uppdateringen** – om du vill aktivera stödet i Configuration Manager 2002 för användning av EDR-policyer du skapar i administrationscentret för Microsoft Endpoint Manager installerar du följande uppdatering från Configuration Manager-konsolen:
  - **Configuration Manager 2002 Hotfix (KB4563473)**

- **Konfigurera anslutning av klientorganisationen** – med anslutning av klientorganisationen kan du synkronisera samlingar av enheter från Configuration Manager till administrationscentret för Microsoft Endpoint Manager. Sedan kan du använda administrationscentret till att distribuera EDR-policyer till samlingarna.

  Anslutning av klientorganisationen konfigureras ofta med samhantering, men du kan konfigurera anslutningen av klientorganisationen separat.

- **Synkronisera Configuration Manager-samlingar** – när du konfigurerar anslutning av klientorganisationen kan du välja de Configuration Manager-enhetssamlingar som ska synkroniseras med administrationscentret för Microsoft Endpoint Manager. Du kan också återgå senare och ändra de enhetssamlingar du synkroniserar. EDR-policyer för Configuration Manager-enheter kan bara tilldelas till samlingar du har synkroniserat.

  När du har valt samlingar att synkronisera måste du aktivera dem för användning med Microsoft Defender ATP.

- **Behörigheter till Azure AD** – när du ska slutföra anslutningen av klientorganisationen och konfigurera vilka Configuration Manager-samlingar som ska synkroniseras med administrationscenter för Microsoft Endpoint Manager behöver du ett konto med behörighet som global administratör för din Azure-prenumeration.

## <a name="edr-profiles"></a>EDR-profiler

[Visa inställningarna](endpoint-security-edr-profile-settings.md) du kan konfigurera för följande plattformar och profiler.

**Intune** – följande stöds för enheter du hanterar med Intune:

- Plattform: **Windows 10 och senare** – Intune distribuerar policyn till enheter i dina Azure AD-grupper.
- Profil: **Slutpunktsidentifiering och svar (MDM)**

**Configuration Manager** *(i förhandsversion)* – följande stöds för enheter du hanterar med Configuration Manager:

- Plattform: **Windows 10 och Windows Server** – Configuration Manager distribuerar policyn till enheter i dina Configuration Manager-samlingar.
- Profil: **Slutpunktsidentifiering och svar (ConfigMgr) (förhandsversion)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Konfigurera Configuration Manager med stöd för EDR-policyer

Innan du kan distribuera EDR-policyer till Configuration Manager-enheter ska du utföra konfigurationerna som beskrivs i följande avsnitt.

De här konfigurationerna görs i Configuration Manager-konsolen för din Configuration Manager-distribution. Om du inte är bekant med Configuration Manager bör du utföra de här uppgifterna tillsammans med en Configuration Manager-administratör.  

Följande avsnitt beskriver de uppgifter du måste utföra:

1. [Installera uppdateringen för Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Aktivera anslutning av klientorganisationen](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Välja vilka samlingar som ska synkroniseras](#task-3-select-collections-to-synchronize)
4. [Aktivera samlingar för Microsoft Defender ATP](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Mer information om hur du använder Microsoft Defender ATP med Configuration Manager finns i följande artiklar i Configuration Manager-innehållet:
>
> - [Registrera Configuration Manager-klienter i Microsoft Defender ATP via administrationscentret för Microsoft Endpoint Manager](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Ansluta klientorganisationer i Microsoft Endpoint Manager: enhetssynkronisering och enhetsåtgärder](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Uppgift 1: Installera uppdateringen för Configuration Manager

Configuration Manager version 2002 måste uppdateras för att du ska kunna använda de Slutpunktsidentifiering och svar-policyer du distribuerar från administrationscentret för Microsoft Endpoint Manager.

**Uppdateringsinformation**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

Du hittar den här uppdateringen som en *konsoluppdatering* för Configuration Manager 2002.

Om du vill installera uppdateringen följer du anvisningarna i [Installera uppdateringar i konsolen](../../configmgr/core/servers/manage/install-in-console-updates.md) i Configuration Manager-dokumentationen.

När du har installerat uppdateringen går du tillbaka hit och fortsätter konfigurera din miljö med stöd för EDR-policyer från administrationscentret för Microsoft Endpoint Manager.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Uppgift 2: Konfigurera anslutning av klientorganisationen och synkronisera samlingar

Om du har aktiverat samhantering tidigare är anslutningen av klientorganisationen redan utförd, och då kan du gå vidare till [uppgift 3](#task-3-select-collections-to-synchronize).

Med anslutning av klientorganisationen anger du samlingar av enheter från Configuration Manager-distributionen som ska synkroniseras med administrationscentret för Microsoft Endpoint Manager. När samlingarna synkroniseras kan du använda administrationscentret till att visa information om enheterna och distribuera EDR-policyer från Intune till dem.  

Mer information om anslutning av klientorganisationen finns i [Aktivera anslutning av klientorganisation](../../configmgr/tenant-attach/device-sync-actions.md) i Configuration Manager-dokumentationen.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Aktivera anslutning av klientorganisationen när samhantering inte har aktiverats

> [!TIP]
> Du kan använda guiden **Konfiguration av samhantering** i Configuration Manager-konsolen när du ska aktivera anslutning av klientorganisationen, men du behöver inte aktivera samhantering.

Om du planerar att aktivera samhantering bör du vara bekant med fenomenet samhantering, vilka förutsättningar som gäller och hur du hanterar arbetsbelastningar innan du fortsätter. Läs mer i [Vad är samhantering?](../../configmgr/comanage/overview.md) i Configuration Manager-dokumentationen.

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.
2. Klicka på **Konfigurera samhantering** i menyfliksområdet för att öppna guiden.
3. På sidan **Registrering av klientorganisation** väljer du **AzurePublicCloud** som miljö. Du kan inte använda molnet Azure Government.
   1. Klicka på **Logga in**. Logga in med ditt *globala administratörskonto*.

   2. Se till att alternativet **Ladda upp till administrationscentret för Microsoft Endpoint Manager** är valt på sidan **Registrering av klientorganisation**.

   3. Ta bort bockmarkeringen från **Aktivera automatisk klientregistrering för samhantering**.

      När det här alternativet är valt visar guiden ytterligare sidor för att slutföra konfigurationen av samhanteringen. Mer information finns i [Aktivera samhantering](../../configmgr/comanage/how-to-enable.md) i Configuration Manager-dokumentationen.

     ![Konfigurera anslutning av klientorganisationen](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Klicka på **Nästa** och sedan **Ja** för att godkänna meddelandet **Skapa AAD-program**. Den här åtgärden etablerar ett huvudnamn för tjänsten och skapar en Azure AD-programregistrering för att underlätta synkroniseringen av samlingar till administrationscentret för Microsoft Endpoint Manager.

5. På sidan **Konfigurera uppladdning** konfigurerar du vilka samlingar du vill synkronisera. Du kan begränsa konfigurationen till en eller flera enhetssamlingar eller använda den rekommenderade inställningen **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**.

6. Klicka på **Sammanfattning** för att granska dina val och klicka sedan på **Nästa**.

7. När guiden är slutförd klickar du på **Stäng**.

   Nu är anslutningen till klientorganisationen konfigurerad och du har valt samlingar att synkronisera till administrationscentret för Microsoft Endpoint Manager.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Aktivera anslutning av klientorganisationen när du använder samhantering

1. Gå till **Administration** > **Översikt** > **Molntjänster** > **Samhantering** i administrationskonsolen för Configuration Manager.

2. Högerklicka på inställningarna för samhantering och välj **Egenskaper**.

3. På fliken **Konfigurera uppladdning** väljer du **Ladda upp till administrationscentret för Microsoft Endpoint Manager**. Klicka på **Använd**.
   - Standardinställningen för uppladdning av enheter är **Alla mina enheter som hanteras av Microsoft Endpoint Configuration Manager**. Du kan också välja att begränsa konfigurationen till en eller flera enhetssamlingar.

     ![Visa fliken Egenskaper för samhantering](media/endpoint-security-edr-policy/configure-upload.png)

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

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Uppgift 4: Aktivera samlingar för Microsoft Defender ATP

När du har konfigurerat vilka samlingar som ska synkroniseras till administrationscentret för Microsoft Endpoint Manager måste du ändå aktivera samlingarna så att de är godkända för registrering och kan hantera Microsoft Defender ATP-policyer.  Det gör du genom att redigera egenskaperna för varje samling i Configuration Manager-konsolen.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Aktivera samlingar för användning med Advanced Threat Protection

1. Använd en Configuration Manager-konsol som är ansluten till webbplatsen på den högsta nivån, högerklicka du på en enhetssamling du synkroniserar med administrationscentret för Microsoft Endpoint Manager och välj **Egenskaper**.

2. På fliken **Molnsynkronisering** aktiverar du alternativet **Gör den här samlingen tillgänglig för tilldelning av Microsoft Defender ATP-policyer i Intune**.

   - Du kan inte välja det här alternativet om Configuration Manager-hierarkin inte är ansluten till klientorganisationen.
  
   ![Konfigurera molnsynkronisering](media/endpoint-security-edr-policy/cloud-sync.png)

3. Välj **OK** för att spara konfigurationen.

   Enheter i den här samlingen kan nu ta emot Microsoft Defender ATP-policyer.

## <a name="create-and-deploy-edr-policies"></a>Skapa och distribuera EDR-policyer

När din Microsoft Defender ATP-prenumeration är integrerad med Intune kan du skapa och distribuera EDR-policyer. Det finns två olika typer av EDR-policyer du kan skapa. En policytyp för enheter du hanterar med Intune via MDM. En annan policytyp för enheter du hanterar med Configuration Manager.

Du väljer vilken typ av policy du skapar när du skapar en ny EDR-policy och väljer plattform för policyn.

Innan du kan distribuera policyer till enheter som hanteras av Configuration Manager ska du [konfigurera Configuration Manager med stöd för EDR-policyer](#set-up-configuration-manager-to-support-edr-policy) från administrationscentret för Microsoft Endpoint Manager.

### <a name="create-edr-policies"></a>Skapa EDR-policyer

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Endpoint Security** > **Slutpunktsidentifiering och svar** > **Skapa policy**.

3. Välj plattform och profil för policyn. Här går vi igenom dina alternativ:

   - Intune – Intune distribuerar policyn till enheter i dina Azure AD-grupper. När du skapar policyn väljer du:
     - Plattform: **Windows 10 och senare**
     - Profil: **Slutpunktsidentifiering och svar (MDM)**

   - Configuration Manager – Configuration Manager distribuerar policyn till enheter i dina Configuration Manager-samlingar. När du skapar policyn väljer du:
     - Plattform: **Windows 10 och Windows Server**
     - Profil: **Slutpunktsidentifiering och svar (ConfigMgr) (förhandsversion)**

4. Välj **Skapa**.

5. På sidan **Grundläggande inställningar** anger du ett namn och en beskrivning för profilen. Välj sedan **Nästa**.

6. På sidan **Konfigurationsinställningar** konfigurerar du de inställningar du vill hantera med den här profilen. Registreringspaketet ingår automatiskt och du kan inte konfigurera det.

   När du har konfigurerat inställningarna väljer du **Nästa**.

7. *Det här steget gäller bara för profilen **Slutpunktsidentifiering och svar**:*  

   På sidan **Omfångstaggar** väljer du **Välj omfångstaggar** för att öppna fönstret *Välj taggar* där du kan tilldela omfångstaggar till profilen.
  
   Fortsätt genom att välja **Nästa**.

8. På sidan **Tilldelningar** väljer du de grupper eller samlingar som ska få policyn. Valet beror på vilken plattform och profil du har valt:

   - För Intune väljer du grupper från Azure AD.
   - För Configuration Manager väljer du samlingar från Configuration Manager som du har synkroniserat med administrationscentret för Microsoft Endpoint Manager och aktiverat för Microsoft Defender ATP-policyn.

   Du kan välja att inte tilldela grupper eller samlingar just nu och i stället redigera policyn senare för att lägga till en tilldelning.

   När du är redo att fortsätta väljer du **Nästa**.

9. Välj **Skapa**på sidan **Granska + skapa** när du är klar.

   Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="edr-policy-reports"></a>Rapporter om EDR-policyer

Du kan visa information om de EDR-policyer du distribuerar i administrationscentret för Microsoft Endpoint Manager. Om du vill visa den här informationen går du till **Endpoint Security** > **Slutpunktsdistribution och svar** och väljer en policy som du vill visa efterlevnadsinformation om:

- För policyer som riktar sig mot plattformen **Windows 10 och senare** (Intune) ser du en översikt över efterlevnaden av policyn. Du kan också välja diagrammet och visa en lista med enheter som har tagit emot policyn och gå vidare till enskilda enheter för att visa mer information.

  I diagrammet **Enheter med ATP-sensor** visas endast enheter som registrerats till Defender ATP med profilen **Windows 10 och senare**. För att se till att du har full representation av dina enheter i det här diagrammet distribuerar du registreringsprofilen till alla dina enheter. Enheter som registrerar till Defender ATP med externa metoder som grupprincip eller PowerShell, räknas som **Enheter utan ATP-sensorn**.

- För policyer som riktar sig mot plattformen **Windows 10 och Windows Server** (Configuration Manager) ser du en översikt över efterlevnaden av policyn, men du kan inte visa mer detaljerad information. Vyn är begränsad eftersom administrationscentret tar emot begränsad statusinformation från Configuration Manager, som hanterar distributionen av policyn till Configuration Manager-enheterna.





[Visa inställningarna](endpoint-security-edr-profile-settings.md) du kan konfigurera för både plattformar och profiler.

## <a name="next-steps"></a>Nästa steg

- [Konfigurera Endpoint Security-policyer](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Läs mer om [Slutpunktsidentifiering och svar](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) i dokumentationen för Microsoft Defender ATP.
