---
title: Konfigurera klientinställningar
titleSuffix: Configuration Manager
description: Välj klient inställningar i Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c64895c7945b972821a1dee1702047e61b740026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713592"
---
# <a name="how-to-configure-client-settings-in-configuration-manager"></a>Konfigurera klient inställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du hanterar alla klient inställningar i Configuration Manager från **administrations** > **klient inställningar**. Ändra standardinställningarna om du vill ange inställningar för alla användare och enheter i hierarkin som inte har några anpassade inställningar. Om du vill tillämpa olika inställningar enbart på vissa användare eller enheter kan du skapa anpassade inställningar och distribuera dem till samlingar.  

Information om varje klient inställning finns i [om klient inställningar](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  Du kan även använda konfigurationsobjekt för att hantera klienter för att utvärdera, spåra och säkerställa konfigurationskompatibilitet för enheter. Mer information finns i [kontrol lera enheternas kompatibilitet med Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Konfigurera standard klient inställningar    

1. I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

2. På fliken **Start** väljer du **Egenskaper**.  

3. Visa och konfigurera klientinställningar för varje inställningsgrupp i navigeringsfönstret.  

   Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper. Information om hur du startar princip hämtning för en enskild klient finns i [Starta princip hämtning för en Configuration Manager-klient](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) i [Hantera klienter](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Skapa och distribuera anpassade klient inställningar  
När du distribuerar dessa anpassade inställningar, ersätter de standardklientinställningarna. Se innan du sätter igång till att du har en samling med de användare eller enheter som behöver ha dessa anpassade klientinställningar.  

1. I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar**.  

2. På fliken **Start** går du till gruppen **skapa** och väljer **skapa anpassade klient inställningar**och välj sedan något av följande:  

   -   **Skapa anpassade klientenhetsinställningar**  

   -   **Skapa anpassade klientanvändarinställningar**  

3. Ange ett unikt namn och en alternativ beskrivning.  

4. Markera en eller flera av kryss rutorna som visar en grupp med inställningar.  

5. Välj varje inställnings grupp i navigerings fönstret och konfigurera de tillgängliga inställningarna och klicka sedan på **OK**.   

6. Välj den anpassade klient inställning som du har skapat. På fliken **Start** i gruppen **klient inställningar** väljer du **distribuera**.  

7. I dialog rutan **Välj samling** väljer du lämplig samling och väljer sedan **OK**. Du kan verifiera den valda samlingen om du klickar på fliken **Distributioner** i detaljfönstret.  

8. Visa ordningen på den anpassade klient inställningen som du har skapat. Om du har flera anpassade klientinställningar används de efter deras ordningsnummer. Om inställningarna krockar med varandra används inställningen med det lägsta ordningsnumret först. Om du vill ändra ordnings numret går du till fliken **Start** , i gruppen **klient inställningar** väljer du **flytta objektet uppåt** eller **flytta objektet nedåt**.  

   Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper. Information om hur du startar princip hämtning för en enskild klient finns i [Starta princip hämtning för en Configuration Manager-klient](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) i [Hantera klienter](../../../core/clients/manage/manage-clients.md).  



##  <a name="view-client-settings"></a>Visa klient inställningar  
 När du distribuerar flera klient inställningar till samma enhet, användare eller användar grupp är prioriteringen och kombinationen av inställningar komplex. Så här visar du klient inställningarna:  

1.  I Configuration Manager-konsolen väljer du **till gångar och efterlevnad** > **enheter** > **användare** eller **användar samlingar**.  

3.  Välj en enhet, användare eller användargrupp och i gruppen **Klientinställningar** väljer du **Resultat av klientinställningar**.  

4.  Välj en klient inställning i den vänstra rutan och inställningarna visas. I den här vyn är inställningarna skrivskyddade. 

    > [!NOTE]  
    >  Om du vill visa klient inställningarna måste du ha Läs behörighet till klient inställningarna.  

    
