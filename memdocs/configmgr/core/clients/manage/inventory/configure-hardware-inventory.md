---
title: Konfigurera maskinvaruinventering
titleSuffix: Configuration Manager
description: Konfigurera maskin varu inventering för alla klienter eller för en samling i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714439"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Så här konfigurerar du maskin varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här proceduren konfigurerar standardklientinställningarna för maskinvaruinventering och gäller för alla klienter i hierarkin. Om du vill att dessa inställningar endast ska tillämpas på vissa klienter skapar du en anpassad enhetsklientinställning och kopplar den till en samling som innehåller de enheter som du vill inventera. Se [Konfigurera klient inställningar](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Om en klientenhet tar emot inställningar för maskinvaruinventering från flera uppsättningar med klientinställningar sammanfogas maskinvarulagerklasserna från varje uppsättning inställningar när klienten rapporterar maskinvaruinventering. Om du inte kontrollerar en klass i en anpassad klient inställning med en högre prioritet inaktive ras inte klienten från att inventera den klassen. 

Om du vill inaktivera en viss maskin varu inventerings klass på en majoritet av system förutom några behöver klassen vara avmarkerad i standard klient inställningarna. Skapa sedan en anpassad klient inställning för att aktivera klassen och distribuera den till mål systemen.


### <a name="to-configure-hardware-inventory"></a>Så här konfigurerar du maskinvaruinventering  

1.  I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

4.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

5.  Välj **maskin varu inventering**i dialog rutan **standardinställningar** .  

6.  Konfigurera följande i listan **Enhetsinställningar** :  

    -   **Aktivera maskin varu inventering på klienter** – Välj **Ja**.  

    -   **Schema för maskin varu inventering** – Klicka på **Schemalägg** för att ange intervallet då klienterna samlar in maskin varu inventering.  

7.  Konfigurera andra [klient inställningar för maskin varu inventering](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) som du behöver.  

Klientenheterna konfigureras med dessa inställningar när de laddar ned klientprincipen. Information om hur du startar princip hämtning för en enskild klient finns i [Hantera klienter](../../../../core/clients/manage/manage-clients.md).  
