---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710890"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** . Klicka på **Konfigurera samhantering** i menyfliksområdet för att öppna **konfigurations guiden för samhantering**.

2. På sidan **prenumeration** i guiden väljer du **Logga**in. Logga in på din Intune-klient och välj sedan **Nästa**.  

3. På sidan **aktivering** väljer du **automatisk registrering i Intune** -inställning, antingen **pilot** eller **alla**. Om en enhet avregistreras av användaren, vid nästa utvärdering av principen, kommer den att registreras igen. <!--3330596--> 

    Den här åtgärden aktiverar automatisk klient registrering i Intune för befintliga Configuration Manager-klienter. När du väljer **pilot**registreras bara de Configuration Manager klienter som är medlemmar i pilot samlingen automatiskt i Intune. Med det här alternativet kan du aktivera samhantering på en delmängd av klienter för att först testa samhantering och distribuera samhantering med hjälp av en stegvis metod. 

    > [!Note]  
    > Från och med version 1806 är automatisk registrering inte omedelbart för alla klienter. Det här beteendet hjälper till att förbättra registreringen i stora miljöer. Configuration Manager slumpar registrering baserat på antalet klienter. Om din miljö till exempel har 100 000 klienter när du aktiverar den här inställningen sker registreringen över flera dagar.<!--1358003-->  

4. För Internetbaserade enheter som redan har registrerats i Intune kopierar du och sparar kommando raden på sidan för **aktivering** . Du kan använda den här kommando raden för att installera Configuration Manager-klienten som en app i Intune. Om du inte sparar den här kommando raden nu kan du när som helst granska samhanterings konfigurationen för att hämta den här kommando raden.

5. På sidan **arbets belastningar** för varje arbets belastning väljer du vilken enhets grupp som ska flyttas över för hantering med Intune. Mer information finns i [arbets belastningar](../workloads.md).  

    Om du bara vill aktivera samhantering behöver du inte byta arbets belastning nu. Du kan byta arbets belastning senare. Mer information finns i [så här växlar du arbets belastningar](../how-to-switch-workloads.md).  

    **Pilot Intune** -inställningen växlar den associerade arbets belastningen endast för enheterna i pilot samlingen. Inställningen **Intune** växlar den associerade arbets belastningen för alla samhanterade Windows 10-enheter.  

    > [!Important]
    > Innan du växlar över arbets belastningar måste du kontrol lera att du har konfigurerat och distribuerat motsvarande arbets belastning i Intune. Se till att arbets belastningarna alltid hanteras av ett av hanterings verktygen för dina enheter.  

6. Konfigurera följande inställningar på sidan **mellanlagring** :  

    - **Pilot**: pilot gruppen innehåller en eller flera samlingar som du väljer. Använd den här gruppen som en del av den stegvisa distributionen av samhantering. Börja med en liten test samling och Lägg sedan till fler samlingar i pilot gruppen när du distribuerar samhantering till fler användare och enheter. Du kan när som helst ändra samlingarna i gruppen pilot.  

    - **Produktion**: konfigurera **undantags gruppen** med en eller flera samlingar. Enheter som är medlemmar i någon av samlingarna i den här gruppen undantas från att använda samhantering.  

7. Slutför guiden för att aktivera samhantering.  
