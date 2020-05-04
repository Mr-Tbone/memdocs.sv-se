---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710897"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** . Klicka på **Konfigurera samhantering** i menyfliksområdet för att öppna **konfigurations guiden för samhantering**.

2. Konfigurera följande inställningar på sidan **prenumeration** i guiden:

    - **Azure-miljön** som ska användas. Till exempel det offentliga Azure-molnet eller Azure amerikanska myndigheters molnet.<!--4075452-->  

    - Välj **Logga**in. Logga in som global administratör för Azure AD och välj sedan **Nästa**.  

        > [!TIP]
        > Du loggar in den här gången igen för den här guidens syfte. Autentiseringsuppgifterna lagras eller återanvänds inte någon annan stans.

3. På sidan **aktivering** väljer du följande inställningar:

   - **Automatisk registrering i Intune** – aktiverar automatisk klient registrering i Intune för befintliga Configuration Manager-klienter. Med det här alternativet kan du aktivera samhantering på en delmängd av klienter för att först testa samhantering och distribuera samhantering med hjälp av en stegvis metod. Om en enhet avregistreras av användaren, vid nästa utvärdering av principen, kommer den att registreras igen. <!--3330596-->

      - **Pilot** – endast de Configuration Manager klienter som är medlemmar i Intune-samlingen för **Automatisk** registrering registreras automatiskt i Intune.
      - **Alla** – aktivera automatisk registrering för alla Windows 10, version 1709 eller senare, klienter.

   - **Automatisk registrering av Intune** – den här samlingen ska innehålla alla klienter som du vill registrera för samhantering. Det är i stort sett en supermängd till alla andra mellanlagrings samlingar.

   ![Ange insamling av Auto-registrering för Intune ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Från och med version 1806 är automatisk registrering inte omedelbart för alla klienter. Det här beteendet hjälper till att förbättra registreringen i stora miljöer. Configuration Manager slumpar registrering baserat på antalet klienter. Om din miljö till exempel har 100 000 klienter när du aktiverar den här inställningen sker registreringen över flera dagar.<!--1358003-->  
      >
      > Från och med version 1906:
      >
      > - En ny samhanterad enhet registreras nu automatiskt i Microsoft Intune tjänst baserat på dess Azure Active Directory (Azure AD) *-token* . Användaren behöver inte vänta på att en användare loggar in på enheten för automatisk registrering för att starta. Den här ändringen bidrar till att minska antalet enheter med registrerings statusen *väntar på användar inloggning*.<!-- 4454491 --> För att det ska fungera måste enheten köra Windows 10, version 1803 eller senare. Mer information finns i [registrerings status för samhantering](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Om du redan har enheter som har registrerats för samhantering, registreras nya enheter omedelbart [när de uppfyller kraven.](../overview.md#prerequisites)<!--4321130-->

4. För Internetbaserade enheter som redan har registrerats i Intune kopierar du och sparar kommando raden på sidan för **aktivering** . Du använder den här kommando raden för att installera Configuration Manager klienten som en app i Intune för Internetbaserade enheter. Om du inte sparar den här kommando raden nu kan du när som helst granska samhanterings konfigurationen för att hämta den här kommando raden.

5. På sidan **arbets belastningar** för varje arbets belastning väljer du vilken enhets grupp som ska flyttas över för hantering med Intune. Mer information finns i [arbets belastningar](../workloads.md). Om du bara vill aktivera samhantering behöver du inte byta arbets belastning nu. Du kan byta arbets belastning senare. Mer information finns i [så här växlar du arbets belastningar](../how-to-switch-workloads.md).  

    - **Pilot Intune** – växlar den associerade arbets belastningen endast för de enheter i pilot samlingarna som du anger på sidan **mellanlagring** . Varje arbets belastning kan ha en annan pilot samling.
    - **Intune** – växlar den associerade arbets belastningen för alla samhanterade Windows 10-enheter.  

    > [!Important]
    > Innan du växlar över arbets belastningar måste du kontrol lera att du har konfigurerat och distribuerat motsvarande arbets belastning i Intune. Se till att arbets belastningarna alltid hanteras av ett av hanterings verktygen för dina enheter.  

6. På sidan **mellanlagring** anger du pilot samlingen för var och en av de arbets belastningar som är inställda på **pilot Intune**.

   ![Ange insamling av Auto-registrering för Intune ](../media/3555750-co-management-onboarding-staging.png)

7. Slutför guiden för att aktivera samhantering.
