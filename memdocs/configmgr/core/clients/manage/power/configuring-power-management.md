---
title: Konfigurera energispar funktioner
titleSuffix: Configuration Manager
description: Konfigurera energispar funktioner i Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715244"
---
# <a name="configure-power-management-in-configuration-manager"></a>Konfigurera energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln förklaras hur du konfigurerar energispar funktioner i Configuration Manager.

## <a name="enable-and-configure-client-settings"></a>Aktivera och konfigurera klient inställningar

Den här proceduren konfigurerar *standard klient inställningarna* för energispar funktioner. Den gäller för alla datorer i hierarkin.

Om du bara vill tillämpa inställningarna på vissa datorer skapar du en *anpassad enhets klient inställning*. Tilldela den sedan till en samling som innehåller datorerna för energispar funktioner. Mer information finns i [så här konfigurerar du klient inställningar](../../deploy/configure-client-settings.md).  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , väljer noden **klient inställningar** och väljer sedan **standard klient inställningar**.

1. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

1. Välj **hanterings grupp för energispar funktioner** .  

1. Aktivera klient inställningen för att **tillåta energispar funktioner för enheter**.

1. Konfigurera ytterligare klient inställningar som du behöver. Mer information finns i [om klient inställningar-energispar funktioner](../../deploy/about-client-settings.md#power-management).  

Klienter konfigurerar de här inställningarna nästa gång de laddar ned klient principen. Information om hur du startar princip hämtning för en enskild klient finns i [Hantera klienter](../manage-clients.md#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Uteslut datorer

Du kan förhindra att samlingar av datorer tar emot inställningar för energisparfunktioner. Om en dator är *medlem i en* samling som du undantar från inställningarna för energispar funktioner tillämpar inte datorn inställningar för energispar funktioner. Detta gäller även om det är medlem i en annan samling som använder inställningar för energispar funktioner.  

Du kanske vill utesluta datorer från energispar funktioner av följande orsaker:  

- Av företagsskäl måste vissa datorer vara påslagna hela tiden.  

- Du har en kontroll uppsättning av datorer där du inte vill använda inställningar för energispar funktioner.  

- Några av datorerna kan inte hantera inställningar för energisparfunktioner.  

- Du vill inte använda energisparfunktioner för datorer som kör Windows Server.  

> [!NOTE]  
> Om du konfigurerar klient inställningen att **tillåta att användare undantar sina enheter från energispar funktioner**kan användarna undanta sina egna datorer från energispar funktioner med hjälp av Software Center.  

Om du vill ta reda på vilka datorer som undantas från energispar funktioner kan du köra rapport **datorerna som uteslutits**. Mer information om den här rapporten finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> Om du undantar en dator från energispar funktionerna återställs alla energi inställningar till sina ursprungliga värden. Du kan inte återställa enskilda energiinställningar till ursprungsvärdena.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Så här undantar du en samling datorer från energispar funktioner  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enhets samlingar** .  

1. Välj den samling som du vill undanta från energispar funktioner. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

1. Växla till fliken **energispar funktioner** och välj **Använd inte inställningar för energispar funktioner på datorer i den här samlingen**.  

## <a name="next-steps"></a>Nästa steg

[Skapa och använda energischeman](create-and-apply-power-plans.md)

[Övervaka och planera för energisparfunktioner](monitor-and-plan-for-power-management.md)
