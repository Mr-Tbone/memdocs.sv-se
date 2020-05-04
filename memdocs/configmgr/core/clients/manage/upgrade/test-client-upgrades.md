---
title: Testa klient uppgraderingar för produktions samling
titleSuffix: Configuration Manager
description: Testa klient uppgraderingar i en för produktions samling i Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3098356eb96609867c0cc16b70d7b141e2a91c26
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715412"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-configuration-manager"></a>Testa klient uppgraderingar i en för produktions samling i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan testa en ny Configuration Manager klient version i en för produktions samling innan du uppgraderar resten av platsen med den.  När du gör det uppgraderas endast enheter som ingår i test samlingen. När du har haft möjlighet att testa klienten kan du uppgradera klienten, vilket gör den nya versionen av klient program varan tillgänglig för resten av platsen.

> [!NOTE]
> Om du vill befordra en test klient till produktion måste du vara inloggad som en användare med säkerhets rollen **Fullständig administratör** och säkerhets **omfattning.** Mer information finns i [grunderna i rollbaserad administration](../../../understand/fundamentals-of-role-based-administration.md). Du måste också vara inloggad på en server som är ansluten till den centrala administrations platsen eller en fristående primär plats på den översta nivån.

 Det finns tre grundläggande steg för att testa klienter i för produktion.  

1.  Konfigurera automatiska klient uppgraderingar att använda en för produktions samling.  

2.  Installera en Configuration Manager uppdatering som innehåller en ny version av klienten.  

3.  Marknadsför den nya klienten för produktion.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Konfigurera automatiska klient uppgraderingar att använda en för produktions samling  
> [!IMPORTANT]
> Klient distribution för för produktion stöds inte för arbets grupps datorer. De kan inte använda den autentisering som krävs för att distributions platsen ska få åtkomst till för produktions klient paketet.  De kommer att få den senaste klienten när den uppgraderas till produktions klienten.

1. [Konfigurera en samling](../collections/create-collections.md) som innehåller de datorer som du vill distribuera för produktions klienten till.   

2. I Configuration Manager-konsolen öppnar du **Administration** > **plats konfiguration** > **platser**och väljer **Inställningar för hierarki**.  

    På fliken **Klientuppgradering** i **Egenskaper för hierarkiinställningar**:  

   -   Välj **Uppgradera alla klienter i förproduktionssamlingen automatiskt med förproduktionsklienten**  

   -   Ange namnet på en samling som ska användas som en förproduktionssamling  

![Testa klient uppgraderingar](media/test-client-upgrades.png)

>[!NOTE]
>Om du vill ändra de här inställningarna måste ditt konto vara medlem i säkerhets rollen **Fullständig administratör** och säkerhets omfattningen **alla** .


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Så här installerar du en Configuration Manager-uppdatering som innehåller en ny version av klienten  

1.  Öppna **administrations** > **uppdateringar och underhåll**i Configuration Manager-konsolen, Välj en **tillgänglig** uppdatering och välj sedan **Installera uppdaterings paket**. (Före version 1702 har uppdateringar och underhåll under **administrations** > **Cloud Services**.)

     Mer information om hur du installerar uppdateringar finns i [uppdateringar för Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Under installationen av uppdateringen väljer du **testa i för produktions samlingen**på sidan **klient alternativ** i guiden.  

3.  Slutför resten av guiden och installera uppdateringspaketet.  

     När guiden slutförts börjar klienter i förproduktionssamlingen att distribuera den uppdaterade klienten. Du kan övervaka distributionen av uppgraderade klienter genom att gå till **övervakning** > av**klient status** > för**klient distribution av för produktion**. Mer information finns i [övervaka klient distributions status](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Distributions status på datorer som är värdar för plats system roller i en för produktions samling kan rapporteras som **icke-kompatibla** även när klienten har distribuerats. När du uppgraderar klienten till produktion rapporteras distributionens status korrekt.

##  <a name="to-promote-the-new-client-to-production"></a>Så här gör du den nya klienten tillgänglig för produktion  

1.  Öppna **administrations** > **uppdateringar och underhåll**i Configuration Manager-konsolen och välj **befordra för produktions klient**. (Före version 1702 har uppdateringar och underhåll under **administrations** > **Cloud Services**.)

    > [!TIP]
    > Knappen **Uppgradera en förproduktionsklient** är också tillgängliga när du övervakar klientdistribution i konsolen i **Övervakning** > **Klientstatus** > **Klientdistribution av förproduktion**.

2.  Granska klient versionerna i produktion och för produktion, kontrol lera att rätt för produktions samling har angetts och klicka sedan på **befordra**och sedan på **Ja**.  

3.  När dialog rutan stängs ersätter den uppdaterade klient versionen den klient version som används i hierarkin. Du kan sedan uppgradera klienterna för hela platsen. Mer information finns i [Uppgradera klienter för Windows-datorer](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) .  

>[!NOTE]
>Om du vill aktivera för produktions klienten, eller för att uppgradera en för produktions klient till en produktions klient, måste ditt konto vara medlem i en säkerhets roll som har **Läs** -och **ändrings** behörighet för objektet **uppdaterings paket** .
>Klient uppgraderingar följer alla Configuration Manager underhålls fönster som du har konfigurerat.
