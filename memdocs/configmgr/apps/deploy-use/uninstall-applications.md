---
title: Avinstallera program
titleSuffix: Configuration Manager
description: Avinstallera ett program med hjälp av Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075854"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Avinstallera program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Vidta följande åtgärder för att avinstallera ett program som du har distribuerat tidigare.

-   Ange kommando raden för att avinstallera distributions typ innehållet på sidan **innehåll** i guiden skapa distributions typ.  

-   Distribuera programmet genom att använda distributionsåtgärden **Avinstallera**.  

> [!IMPORTANT]  
> Vissa programtyper stöder inte avinstallation.  

 Den här listan innehåller mer information om hur program avinstallation fungerar:  

-   När du avinstallerar ett Configuration Manager-program (Configuration Manager) avinstalleras inte alla beroende program automatiskt.  

-   Om du distribuerar ett program som använder en åtgärd för att **Avinstallera** till en användare och programmet har installerats för alla användare av datorn, kan avinstallationen Miss Miss kan om användarens konto inte har behörighet att avinstallera programmet.  

-   Om du tar bort en användare eller en enhet från en samling som har ett program distribuerat till den, tas programmet inte bort automatiskt från enheten.  

-   En distribution med distributionssyftet **Avinstallera** kontrollerar inte kravreglerna. Om programmet är installerat på den dator som distributionen körs på, avinstalleras det.  

> [!IMPORTANT]  
> Om du vill distribuera programmet med åtgärden avinstallera måste du först ta bort alla befintliga program distributioner, simulerade distributioner eller aktivitetssekvensdistributioner som innehåller det här programmet. 

 Mer information om hur du skapar en distributions typ finns i [skapa program](../../apps/deploy-use/create-applications.md).  

 Mer information om hur du distribuerar ett program finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Avinstallera ett program  

1.  Konfigurera programmets distributionstyp med kommandoraden avinstallera genom att använda en av följande metoder:  

    -   På sidan **Allmänt** i guiden skapa distribution väljer du alternativet **identifiera information om den här distributions typen automatiskt från installationsfiler**. Om informationen är tillgänglig i installationsfilerna läggs kommandoraden avinstallera automatiskt till i distributionstypegenskaperna.  

    -   På sidan **innehåll** i guiden skapa distributions typ går du till fältet **Avinstallera program** och anger kommando raden för att avinstallera programmet.  

        > [!NOTE]  
        >  Sidan **innehåll** visas endast om du väljer alternativet **Ange distributions typs informationen manuellt** på sidan **Allmänt** i guiden skapa distributions typ.  

    -   På fliken **program** i ** <dialog rutan *namn på distributions typ*> egenskaper** anger du kommando raden för att avinstallera programmet i fältet **Avinstallera program** .  

2.  Distribuera programmet och välj sedan **avinstallationen** av distributions åtgärden på sidan **distributions inställningar** i guiden distribuera program vara.  

    > [!NOTE]  
    >  När du väljer distributionsåtgärden **Avinstallera**konfigureras distributionssyftet automatiskt som **Obligatoriskt**.  
