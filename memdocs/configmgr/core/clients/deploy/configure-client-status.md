---
title: Konfigurera klient status
titleSuffix: Configuration Manager
description: Välj inställningar för klient status i Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384918"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Konfigurera klient status i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du kan övervaka Configuration Manager klienter och åtgärda problem konfigurerar du platsens klient status inställningar. De här inställningarna anger de parametrar som platsen använder för att markera klienter som inaktiva. Konfigurera också alternativ för att varna dig om klient aktiviteten sjunker under ett angivet tröskelvärde.

## <a name="configure-client-status"></a>Konfigurera klient status

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **klient status** . På fliken **Start** i menyfliksområdet i gruppen **klient status** väljer du **Inställningar för klient status**.

1. Konfigurera följande inställningar:

    > [!NOTE]
    > Om en klient inte uppfyller någon av inställningarna markerar platsen den som inaktiv.

    - **Klient princip begär Anden under följande dagar:** Ange antalet dagar sedan klienten begärde en princip från platsen. Standardvärdet är `7` dagar.

      Jämför det här värdet med inställningen för **avsöknings intervall för klient princip** i **klient princip** gruppen i klient inställningar. Standardvärdet är 60 minuter. Med andra ord bör en klient söka efter principer varje timme. Om den inte begär en princip efter en vecka markerar platsen den som inaktiv.

    - **Pulsslags identifiering under följande dagar:** Ange antalet dagar sedan klienten skickade en pulsslags identifierings post till platsen. Standardvärdet är `7` dagar.

      Jämför det här värdet med schemat för [identifierings metoden för pulsslag](../../servers/deploy/configure/about-discovery-methods.md). Som standard kör platsen pulsslags identifiering en gång i veckan.

    - **Maskin varu inventering under följande dagar:** Ange antalet dagar sedan klienten skickade en maskin varu inventerings post till platsen. Standardvärdet är `7` dagar.

      Jämför det här värdet med **schemaläggnings inställningen för maskin varu inventering** i **maskin varu inventerings** gruppen för klient inställningar. Standardvärdet är sju dagar.

    - **Program varu inventering under följande dagar:** Ange antalet dagar sedan klienten skickade en program varu inventerings post till platsen. Standardvärdet är `7` dagar.

      Jämför det här värdet med inställningen **Schemalägg program varu inventering och fil insamling** i **program varu inventerings** gruppen för klient inställningar. Standardvärdet är sju dagar.

    - **Status meddelanden under följande dagar:** Ange antalet dagar sedan klienten skickade status meddelanden till platsen. Standardvärdet är `7` dagar. Klienten kan skicka status meddelanden för olika typer av aktiviteter, till exempel köra en aktivitetssekvens. Platsen tar bort gamla status meddelanden som en del av underhålls aktiviteten, **ta bort föråldrade status meddelanden**.

1. Ange följande värde för att avgöra hur länge platsen behåller klient status historiken:

    - **Behåll klient status historik i följande antal dagar:** Som standard behåller platsen information om klient status i `31` dagar. Den här inställningen påverkar inte klient-eller plats beteendet. Det liknar en underhålls uppgift för klient status historik.

## <a name="configure-the-schedule"></a>Konfigurera schemat

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **klient status** . På fliken **Start** i menyfliksområdet i gruppen **klient status** väljer du **Schemalägg klient status uppdatera**.

1. Konfigurera intervallet som du vill att klient status ska uppdateras med.

    > [!NOTE]
    > När du ändrar schemat för klient status uppdateringar börjar det inte gälla förrän nästa schemalagda klient status uppdateras enligt föregående schema.

## <a name="configure-alerts"></a>Konfigurera varningar

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enhets samlingar** .

1. Välj den samling som du vill konfigurera aviseringar för. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.

    > [!NOTE]
    > Det går inte att konfigurera aviseringar för användar samlingar.

1. Växla till fliken **aviseringar** och välj **Lägg till**.

   > [!TIP]
   > Du kan bara visa fliken **aviseringar** om säkerhets rollen har behörighet för aviseringar.

    Välj de aviseringar som du vill att webbplatsen ska generera för tröskelvärden för klient status och välj **OK**.

1. I listan **villkor** på fliken **aviseringar** markerar du varje klient status avisering och anger följande information:

    - **Aviserings namn**: acceptera standard namnet eller ange ett nytt namn för aviseringen.

    - **Allvarlighets grad för avisering**: Välj den varnings nivå som visas i Configuration Manager-konsolen.

    - **Generera avisering**: Ange tröskel procent andelen för aviseringen.

## <a name="automatic-remediation-exclusion"></a>Undantag för automatisk reparation

1. Öppna Registereditorn på den klient dator där du vill inaktivera automatisk reparation.

    > [!WARNING]
    > Om du använder Registereditorn på ett felaktigt sätt kan det orsaka allvarliga problem som kräver att du installerar om Windows. Microsoft kan inte garantera att du kan lösa problem som orsakas av felaktig användning av Registereditorn. Använd den på egen risk.

1. Navigera till register nyckeln **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval**.

1. Ändra värdet för **NOTIFYONLY** -posten:

    - `TRUE`: Klienten åtgärdar inte automatiskt eventuella problem som hittas. Platsen meddelar fortfarande dig i arbets ytan **övervakning** om eventuella problem med den här klienten.

    - `FALSE`: Den här inställningen är standard. Klienten åtgärdar automatiskt problem när de hittar dem och platsen meddelar dig i arbets ytan **övervakning** .

När du installerar klienter kan du undanta dem från automatisk reparation med installations egenskapen **NOTIFYONLY** . Mer information finns i [om klient installations egenskaper](about-client-installation-properties.md).

## <a name="next-steps"></a>Nästa steg

[Övervaka klienter](../manage/monitor-clients.md)
