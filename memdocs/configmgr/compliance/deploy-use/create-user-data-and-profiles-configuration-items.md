---
title: Skapa användardata och profilkonfigurationsobjekt
titleSuffix: Configuration Manager
description: Använd konfigurations objekt för data och profiler i Configuration Manager för att hantera mappomdirigering, offlinefiler och centrala profiler.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a99384772895ff2675ade671076163b74cecee2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075310"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Skapa konfigurations objekt för användar data och profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Konfigurations objekt för användar data och profiler i Configuration Manager innehåller inställningar som kan hantera mappomdirigering, offlinefiler och centrala profiler på datorer som kör Windows 8 och senare för användare i hierarkin. Du kan till exempel:  

- Omdirigera en användares dokumentmapp till en nätverks resurs.  

- Se till att angivna filer som lagras i nätverket är tillgängliga på en användares dator när nätverks anslutningen inte är tillgänglig.  

- Konfigurera vilka filer i en användares centrala profil som synkroniseras med en nätverks resurs när användaren loggar in och ut.  

  Till skillnad från andra konfigurations objekt i Configuration Manager lägger du inte till konfigurations objekt för användar data och profiler i en konfigurations bas linje som du sedan distribuerar. Du distribuerar i stället konfigurationsobjektet direkt i dialogrutan **Distribuera konfigurationsobjekt för användardata och profiler** .  

> [!IMPORTANT]  
>  Du kan bara distribuera konfigurationsobjekt för användardata och profiler till användarsamlingar.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Aktivera användardata och profiler för kompatibilitetsinställningar  
 Använd följande procedur när du ska konfigurera standardklientinställningen för kompatibilitetsinställningar för användardata och profiler som gäller för alla datorer i hierarkin. Om du vill att den här inställningen bara ska gälla för vissa datorer skapar du en anpassad klientinställning och kopplar den till en samling som innehåller de datorer som du vill använda kompatibilitetsinställningarna för användardata och profiler för. Mer information om hur du skapar anpassade enhets inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

1.  I Configuration Manager-konsolen klickar du på **Administration** > **klient inställningar** > **standardinställningar**.  

4.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

5.  Klicka på **Kompatibilitetsinställningar** i dialogrutan **Standardinställningar**.  

6.  Välj **Ja** i listrutan **Aktivera användardata och profiler**.  

7.  Stäng dialogrutan **Standardinställningar** genom att klicka på **OK** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Skapa ett konfigurations objekt för användar data och profiler  

1. I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** > **kompatibilitetsinställningar** > **användar data och profiler**.  

2. På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa konfigurationsobjekt för användardata och profiler**.  

3. På sidan **Allmänt** i **Guiden Skapa konfigurationsobjekt för användardata och profiler**anger du följande information:  

   -   **Namn:** Ange ett unikt namn på konfigurationsobjektet. Använd högst 256 tecken.  

   -   **Beskrivning:** Ange en beskrivning som ger en översikt över konfigurationsobjektet och annan relevant information som hjälper dig att identifiera den i Configuration Manager-konsolen. Använd högst 256 tecken.  

   -   **Mappomdirigering:** Markera den här kryssrutan om du vill ange inställningar för omdirigering av mappar för det här konfigurationsobjektet.  

   -   **Offlinefiler:** Markera den här kryssrutan om du vill ange inställningar för offlinefiler för det här konfigurationsobjektet.  

   -   **Centrala användarprofiler:** Markera den här kryssrutan om du vill ange inställningar för centrala användarprofiler för det här konfigurationsobjektet.  

4. På sidan **Mappomdirigering** i **Guiden Skapa konfigurationsobjekt för användardata och profiler**anger du hur mappomdirigering ska hanteras på klientdatorerna för de användare som får konfigurationsobjektet. Du kan konfigurera inställningar för valfri enhet som användaren loggar in på eller enbart för användarens primära enheter. Mer information om mappomdirigering finns i dokumentationen till Windows Server.  

   > [!NOTE]  
   >  Den här sidan visas bara om du har markerat **Mappomdirigering** på sidan **Allmänt** i guiden.  

5. På sidan **Offlinefiler** i **Guiden Skapa konfigurationsobjekt för användardata och profiler**kan du aktivera och inaktivera användning av offlinefiler för de användare som får det här konfigurationsobjektet och ställa in funktionssätt för offlinefilerna. Du kan också ange vilka offlinefiler som alltid ska vara tillgängliga på den dator som användaren loggar in på. Mer information om offlinefiler finns i dokumentationen till Windows Server.  

   > [!NOTE]  
   >  Den här sidan visas bara om du har markerat kryss rutan **offline-filer** på sidan **Allmänt** i guiden.  

6. På sidan **Centrala profiler** i **Guiden Skapa konfigurationsobjekt för användardata och profiler**kan du ange om centrala profiler ska vara tillgängliga på datorer som användarna loggar in på och även ange ytterligare information om hur profilerna fungerar. Mer information om centrala profiler finns i dokumentationen till Windows Server.  

   > [!NOTE]  
   >  Den här sidan visas bara om du har markerat kryss rutan **centrala användar profiler** på sidan **Allmänt** i guiden.  

7. Slutför guiden.  

   Det nya konfigurationsobjektet för användardata och profiler visas i noden **Användardata och profiler** på arbetsytan **Tillgångar och efterlevnad** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Distribuera ett konfigurations objekt för användar data och profiler  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** > **kompatibilitetsinställningar** > **användar data och profiler**.  

3.  Välj det konfigurationsobjekt för användardata och profiler som du vill distribuera. Gå sedan till fliken **Start** . I gruppen **Distribution** klickar du på **Distribuera**.  

4.  I dialogrutan **Distribuera konfigurationsobjekt för användardata och profiler** anger du följande information:  

    -   **Samling** – Klicka på **Bläddra** och välj den användarsamling där du vill distribuera konfigurationsobjektet.  

        > [!IMPORTANT]  
        >  Du kan bara distribuera konfigurationsobjekt för användardata och profiler till användarsamlingar.  

    -   **Reparera inkompatibla regler när stöd finns** – Aktivera det här alternativet om du vill att regler som bedöms som inkompatibla ska ändras automatiskt på klientdatorer.  

    -   **Tillåt reparation utanför underhållsfönstret** – Om en underhållsperiod har angetts för den samling som du distribuerar konfigurationsobjektet till, kan du aktivera det här alternativet och låta kompatibilitetsinställningarna ändra värdet utanför underhållsperioden. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

    -   **Generera en avisering** – Aktivera det här alternativet om du vill ange en avisering som skapas om konfigurationsobjektets kompatibilitet är lägre än en angiven procentandel vid en angiven tidpunkt. Du kan även ange om du vill att en avisering ska skickas till System Center Operations Manager.  

    -   **Schemalägg utvärdering av kompatibilitet för det här konfigurationsobjektet:** Anger schemat för hur det distribuerade konfigurationsobjektet ska utvärderas på klientdatorer. Det kan vara ett enkelt eller ett anpassat schema.  

5.  Klicka på **OK** . Dialogrutan **Distribuera konfigurationsobjekt för användardata och profiler** stängs, och distributionen skapas.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Övervaka konfigurationsobjekt för användardata och profiler  
 Du kan övervaka den här typen av konfigurations objekt på samma sätt som du övervakar andra kompatibilitetsinställningar.  

 Mer information finns i [så här övervakar du](../../compliance/deploy-use/monitor-compliance-settings.md)kompatibilitetsinställningar.  
