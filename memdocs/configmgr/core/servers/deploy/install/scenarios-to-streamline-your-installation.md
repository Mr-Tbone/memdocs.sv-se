---
title: Installationsscenarier
titleSuffix: Configuration Manager
description: Lär dig hur du installerar en ny Configuration Manager-hierarki när du uppdaterar eller uppgraderar en-plats.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718100"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Scenarier för att effektivisera installationen av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med versionen av uppdaterings versioner för Configuration Manager aktuella grenen finns det nya scenarier för att effektivisera installationen av en ny hierarki till en uppdaterings version (t. ex. uppdatering 1610) och att uppgradera från Microsoft System Center 2012 Configuration Manager.

Följande är exempel på scenarier som stöds:  

**Installera en ny Configuration Manager aktuella Branch-hierarki** som kör en uppdaterings version.  

-   Installera endast platsen på den översta nivån och installera sedan omedelbart en uppdatering för att göra platsen aktuell med den uppdaterings version som du kommer att använda. Sedan kan du installera ytterligare platser direkt till den uppdaterade versionen.  
-   I det här scenariot hoppar du över processen att installera ytterligare platser på en bas linje nivå och uppdaterar dem sedan till den uppdaterings version som du vill använda.  
-   I det här scenariot hoppar du över processen att installera klienter till en bas linje version och installerar sedan om dem när du uppdaterar till en senare version.  

**Uppgradera en Microsoft System Center 2012 Configuration Manager** -infrastruktur till en uppdaterings version av Configuration Manager.  

-   Uppgradera den centrala administrations platsen och varje primär plats till en bas linje version manuellt (till exempel version 1606) innan du installerar en uppdaterings version (till exempel version 1610).  
-   Uppgradera inte sekundära platser från Microsoft System Center 2012 Configuration Manager förrän dina primära platser kör den uppdaterings version som du kommer att använda.  
-   Uppgradera inte klienter från Microsoft System Center 2012 Configuration Manager förrän dina primära platser kör den uppdaterings version som du kommer att använda.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Scenario: installera en ny hierarki till en uppdaterad version  
I det här exempel scenariot installerar du den första platsen i en hierarki med hjälp av en bas linje version av Configuration Manager, till exempel version 1610. Installera sedan 1610-uppdateringen innan du distribuerar ytterligare platser eller klienter.  

-   Eftersom du planerar att använda en uppdaterings version (t. ex. version 1610) och inte är kvar på en bas linje version (t. ex. version 1606) behöver du inte installera ytterligare platser och sedan uppgradera dem. Detta gäller även för klienter.  
-   Installera inte sekundära platser med version 1606 och uppgradera dem sedan till version 1610. Installera i stället sekundära platser efter att dina primära platser kör version 1610.  

Följ den här ordningen:  

1. **Installera en plats på den översta nivån för den nya hierarkin** med hjälp av bas linje mediet.  

   -   Du kan endast använda bas linje medier för att installera den första platsen i en ny hierarki.  
   -   Du kan till exempel installera en plats på den översta nivån med hjälp av bas linje versionen av 1606. Mer information finns i [använda installations guiden för att installera-platser](use-the-setup-wizard-to-install-sites.md).  

   Efter det här steget Kör platsen på den högsta nivån version 1606.  

2. **Använd uppdateringar i konsolen för att uppdatera platsen på den högsta nivån till en senare version.**  

   -   Innan du installerar underordnade platser eller klienter måste du uppdatera platsen på den högsta nivån till den uppdaterings version som du planerar att använda.  
   -   Du kan till exempel uppdatera platsen på den högsta nivån som kör version 1606 till version 1610. Mer information finns i [uppdateringar för Configuration Manager](../../../../core/servers/manage/updates.md).  

   Efter det här steget Kör platsen på den högsta nivån version 1610.  

3. **Installera nya underordnade primära platser under en central administrationswebbplats.**  

   - Använd installationsmediet på cd-skivan Senaste mappen på servern för den centrala administrationswebbplatsen för att installera underordnade primära platser. Mer information finns [på CD-skivan. Den senaste mappen för Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Den här källmediet krävs för att säkerställa att nya underordnade primära platser matchar versionen av den centrala administrationswebbplatsen.  

   Efter det här steget Kör dina nya underordnade primära platser version 1610.  

4. **På varje primär plats använder du alternativet i konsolen för att installera nya sekundära platser.**  

   -   Eftersom du inte har installerat sekundära platser när de primära platserna var i version 1606 behöver du inte uppgradera sekundära platser.  
   -   Installera i stället nya sekundära platser som kör version 1610. Mer information finns i [Installera en sekundär plats](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) i artikeln [Använda installationsguiden för att installera platser](use-the-setup-wizard-to-install-sites.md) .  

   Efter det här steget installeras nya sekundära platser och kör version 1610.  

5. **Installera nya klienter på den primära platsen.**  

   -   Eftersom du inte har installerat klienter medan de primära platserna var i version 1606 behöver du inte uppgradera klienter från version 1606 till version 1610.  
   -   Installera i stället nya klienter som kör version 1610. Mer information finns i [Distribuera klienter](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Efter det här steget installeras nya klienter som kör version 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Scenario: uppgradera System Center 2012 Configuration Manager till en uppdaterad version av Configuration Manager, aktuell gren  

I det här exempel scenariot uppgraderar du System Center 2012 Configuration Manager-infrastrukturen till en uppdaterad version av Configuration Manager aktuella grenen, till exempel version 1610.  

-   Den centrala administrations platsen och varje primär plats måste uppgraderas till bas linje version 1606 innan du installerar uppdateringen för version 1610.  
-   Sekundära platser och klienter uppgraderar eller installerar inte version 1606. I stället flyttas de direkt från System Center 2012 Configuration Manager till Configuration Manager nuvarande gren version 1610.  

Följ den här ordningen:  

1. **Uppgradera den översta System Center 2012 Configuration Manager-platsen** till en bas linje version av den aktuella grenen genom att använda käll medier för Configuration Manager (till exempel version 1606). Mer information finns i [Uppgradera till Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Precis som med traditionella uppgraderings scenarier uppgraderar du alltid platsen på den översta nivån i en hierarki först och uppgraderar sedan underordnade platser.  

   Efter det här steget Kör platsen på den högsta nivån version 1606.  

2. **Uppgradera varje underordnad primär plats i hierarkin** till samma baslinjeversion.  

   -   När du uppgraderar från Microsoft System Center 2012 Configuration Manager måste du manuellt uppgradera varje primär plats till en bas linje version av den aktuella grenen.  
   -   Du kommer inte att uppgradera sekundära platser just nu.  

   Efter det här steget Kör varje primär plats version 1606.  

3. **Ange underhålls perioder på underordnade primära platser.** När du har uppgraderat alla dina primära platser till bas linje versionen planerar du att konfigurera underhålls perioder för att styra när platserna installerar infrastruktur uppdateringar. Mer information finns i [använda underhålls](../../../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  (Underhålls fönster kallas för *service fönster* i version 1606.)  

   -   En underordnad primär plats installerar automatiskt samma uppdateringar som du installerar på en central administrationswebbplats.  
   -   Sekundära platser installerar installerar inte automatiskt nya versioner. Du måste uppgradera dem manuellt inifrån-konsolen.  

   När det här steget är klart och du installerar uppdateringar på den centrala administrationswebbplatsen installerar underordnade primära platser endast uppdateringen när så tillåts enligt deras underhållsperiod.  

4. **Installera uppdaterings versionen på platsen på den högsta nivån.** Den här uppdateringen uppdaterar platsen på den högsta nivån. När en central administrations plats installerar uppdaterings versionen installerar varje underordnad primär plats uppdateringen automatiskt om inte installationen blockeras av en underhålls period.  

   -   Du kan till exempel uppdatera platsen på den högsta nivån från version 1606 till version 1610. Mer information finns i [uppdateringar för Configuration Manager](../../../../core/servers/manage/updates.md).  

   Efter det här steget Kör den centrala administrations platsen och varje primär plats version 1610.  

5. **Uppgradera sekundära platser.** När en primär plats installerar uppdateringen och kör version 1610 använder du alternativet i konsolen för att uppgradera sekundära platser.  

   -   Detta uppgraderar sekundära platser direkt från Microsoft System Center 2012 Configuration Manager till den uppdaterings version som du installerade på den primära platsen.  
   -   Information om hur du uppgraderar en sekundär plats finns i [Uppgradera platser](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) i avsnittet [Uppgradera till Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) .  

6. **Uppgradera klienter.** Uppgradera klienterna med hjälp av informationen i [Uppgradera klienter för Windows-datorer](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   Detta uppgraderar klienter direkt från Microsoft System Center 2012 Configuration Manager till den uppdaterings version som du installerade på den primära platsen.  

   Efter det här steget uppgraderas klienter till version 1610 utan att först uppgradera till version 1606.
